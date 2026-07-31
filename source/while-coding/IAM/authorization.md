RFC that is basis of authz: https://datatracker.ietf.org/doc/html/rfc2904

## Data level entitlements:

Good artcles:


https://enterprise-knowledge.com/inside-the-unified-entitlements-architecture/#:~:text=modify%20queries%20in%2Dflight%20to%20add%20entitlement%2Daware%20filters

Typical Interaction Flow (UML Sequence Pattern)
User/application initiates data access request.

The application authenticates (via OAuth2/SAML) and sends the request with user identity and attributes.

Entitlement Integration Core looks up roles/permissions for the unified user.

Policy Engine evaluates requested action against current policies.

Query Federation Layer rewrites/modifies data query to restrict results to entitled data.

The system retrieves filtered data and logs the access decision with context for auditing.

Systems (databases, data lakes, etc.) provide just the subset of data aligned to granted entitlements.​


## Authorization in AI-Agentic systems

Ref: https://www.reva.ai/solution-guide/intent-and-behavior-based-access-control-ibac-the-next-evolution-of-authorization-for-the-agentic-enterprise

### Why Traditional Authorization Models Break Down

For decades, enterprise authorization has focused on determining whether a particular identity should be allowed to perform a specific action against a protected resource.

Role-Based Access Control (RBAC), Attribute-Based Access Control (ABAC), Relationship-Based Access Control (ReBAC), and Policy-Based Access Control (PBAC) all represent important advances in authorization architecture. Modern policy engines such as Cedar, OPA, and Zanzibar-inspired systems have enabled organizations to centralize authorization decisions and implement fine-grained runtime controls.

Despite these advances, traditional authorization models rely on assumptions that become increasingly fragile in agentic environments.

The first assumption is that the principal performing an action remains stable throughout the transaction. The second assumption is that workflows are predictable and largely deterministic. The third assumption is that evaluating authorization at a specific point in time provides a reasonable approximation of whether the resulting action should occur.

Agentic systems violate all three assumptions. A user requesting a customer analysis may unknowingly trigger interactions across CRM systems, contract repositories, support ticketing platforms, financial systems, and external data sources. Multiple agents may participate in the workflow, each acting under its own identity and permissions. New actions emerge dynamically as the workflow evolves.

Every individual action may satisfy existing authorization policies. But, the overall outcome may still be inappropriate.

This challenge becomes particularly visible through the classic confused deputy problem. In traditional systems, a confused deputy is a privileged intermediary manipulated into exercising authority on behalf of another party. Agentic AI effectively industrializes this pattern. Agents often require broad permissions to perform useful work and continuously reinterpret instructions based on newly acquired information. The result is a highly privileged intermediary capable of executing actions that remain technically authorized but operationally inappropriate.

### The Two Decays: Identity Decay and Intent Decay
The fundamental authorization challenge of agentic systems can be understood through two interconnected processes: Identity Decay and Intent Decay. Together, these represent the primary mechanisms through which trust degrades across autonomous workflows.

Identity Decay occurs when the relationship between an executed action and the human authority that originally authorized it becomes progressively weaker through delegation. A human delegates work to an orchestrator. The orchestrator delegates work to a specialized agent. The specialized agent invokes tools using service identities. Each handoff introduces additional separation between the action and its originating authority.

Eventually, authorization systems observe only a workload identity or service account performing an operation. The original user, their permissions, and the context under which authority was granted become increasingly opaque.

Intent Decay follows a parallel path. Every hop in an agentic workflow involves interpretation. User objectives become plans. Plans become subtasks. Tool outputs become new inputs. Retrieved documents influence reasoning. Memory systems provide context. Each step may be individually reasonable while collectively moving the workflow further away from the objective originally authorized. Intent rarely fails catastrophically. Instead, it drifts gradually.

The authorization problem therefore shifts from evaluating individual requests to evaluating the trajectory of an entire workflow.

### Why Existing Approaches Fall Short

The market has largely responded to agentic security challenges through two independent approaches.

The first approach extends traditional authorization through increasingly fine-grained policy enforcement. PBAC platforms externalize authorization logic and evaluate policies dynamically at runtime. These systems provide determinism, auditability, and governance.

However, policies remain fundamentally tied to identities and actions. They answer whether an action is permitted. They do not evaluate whether the action remains aligned with the purpose that originally justified it. As Intent Decay increases, policy engines become increasingly blind to workflow trajectory.

The second approach focuses on intent evaluation. Emerging AI security platforms use machine learning and large language models to evaluate user intent and identify potentially risky actions. These systems provide valuable signals. However, they remain probabilistic.

A model may conclude that an action appears suspicious or aligned with intent, but enterprises cannot rely exclusively on probabilistic systems to make authorization decisions. Models can misclassify context, produce inconsistent outcomes, and be manipulated by adversarial inputs.

The challenge is not that either approach is wrong. The challenge is that each solves only part of the problem.

Policies provide deterministic enforcement but lack understanding of intent. Intent evaluation provides contextual understanding but lacks deterministic guarantees. Agentic environments require both.

### Possible solution (by Reva)

The first component is identity continuity. Human users, agents, workloads, services, and tools must possess verifiable identities that persist throughout execution. Emerging standards such as SPIFFE workload identities and transaction-token architectures provide the foundation for establishing chain-of-custody across delegation boundaries.

The second component is continuous intent evaluation. Rather than evaluating authorization exclusively at session establishment or credential issuance, intent must be reassessed at every execution hop. This evaluation combines semantic similarity analysis, contextual reasoning, workflow state, and execution history to determine whether actions remain aligned with authorized objectives.

The third component is behavioral analysis. Human and non-human identities establish behavioral baselines over time. Deviations from expected operating patterns become risk signals that influence authorization decisions.

### NOtes

- Understand how SPIFFE and transaction tokens help
- The industry moved from access control lists to role-based access control, from roles to attributes, from attributes to policy-driven authorization.
- identity based Vs capability based systems
  - Identity based: For example, an online registration for an event where you have registered by giving just your name. Now when you reach the event, the person at the entry checks if your name is on the list of registered users and then asks you to show an govt. id proof.
  - Capability based: For example, an online registration for an event where you have registered and you got a QR code. Like booking a movie ticket. You just have to show this QR code at the entrance to get into the event. No identity needed at the event. This QR is capability. If someone else has the QR, then they have the capability and they can go to the event.
 
## Capability-Based vs. Identity-Based Access Control

### 1. Overview & Core Characteristics

```
[ Identity-Based (ACL/RBAC) ]           [ Capability-Based (Tokens/Handles) ]
  "Who are you?"                           "Do you hold a valid key?"
  • Checks caller identity                 • Checks token/key possession
  • Ambient authority (fixed roles)        • Explicit authority (scoped handles)

```

* **Identity-Based Security (ACLs / RBAC / ABAC):**
* **Core Premise:** Access decisions depend on **who** is making the request (User ID, Role, Department).
* **Mechanism:** The system verifies the identity of the caller and looks up their permissions in a central database or Access Control List (ACL).
* **Authority Model:** Features **ambient authority**—a service or user carries broad, persistent permissions whenever they interact with resources.


* **Capability-Based Security (Tokens / Handles):**
* **Core Premise:** Access decisions depend on **what key/token** the caller holds, regardless of their identity.
* **Mechanism:** The system checks an unforgeable, cryptographically signed reference or bearer token (e.g., shareable Google Doc links, file descriptors, OAuth tokens).
* **Authority Model:** Features **explicit authority**—permissions are attached directly to the token presented for that specific action.



---

### 2. Comparative Matrix

| Feature / Dimension | Identity-Based Systems | Capability-Based Systems |
| --- | --- | --- |
| **Primary Check** | Caller's Identity ($Who$) | Token/Ticket Possession ($Key$) |
| **Authority** | **Ambient** (Persistent system roles) | **Explicit** (Scoped per request/task) |
| **Granularity** | Coarse to fine (risks role explosion) | Highly fine-grained & dynamic |
| **Confused Deputy Risk** | High (vulnerable to privilege misuse) | Very Low (immune by structure) |
| **Revocation** | **Easy** (Disable user centrally) | **Hard** (Tokens persist until expiration) |
| **Auditability** | **Easy** (Inspect who has access) | **Hard** (Tokens can pass offline) |

---

### 3. Pros and Cons

#### Identity-Based Systems

* **Pros:**
* **Centralized Governance:** Simple to revoke access globally by disabling an employee's single account.
* **Clear Auditability:** Easy to list all users who currently have access to a specific resource.
* **Standard Infrastructure:** Supported natively by almost all enterprise Identity Providers (Okta, Entra ID).


* **Cons:**
* **Role Explosion:** Dynamic policies require creating thousands of hyper-specific roles.
* **Vulnerable to Confused Deputy:** High-privilege services can easily be tricked into abusing their ambient authority.



#### Capability-Based Systems

* **Pros:**
* **Default Least Privilege:** Tokens can be issued with narrow scopes and short time limits (e.g., read-only for 5 minutes).
* **Decentralized Delegation:** Services can downscope and forward capability tokens locally without hitting a central auth server.
* **Prevents Ambient Authority Abuse:** Eliminates implicit, broad service permissions.


* **Cons:**
* **The Bearer Token Problem:** Anyone who steals or intercepts the token gains its permissions until it expires.
* **Difficult Revocation:** Hard to cancel individual tokens across distributed microservices before they expire without complex blacklists.



---

### 4. The Confused Deputy Scenario

The **Confused Deputy Problem** occurs when an attacker tricks a highly privileged intermediary (e.g., an AI agent or microservice) into performing an unauthorized action on their behalf.

```
--- IDENTITY-BASED (Vulnerable) ---
Attacker (Low Privilege) ──(Prompt Injection)──> AI Agent (High Ambient Privilege)
                                                     │
                                                     ▼
                                            Database Executes
                                   ("Agent has ADMIN role -> APPROVED")


--- CAPABILITY-BASED (Protected) ---
Attacker (Low Privilege) ──(Prompt Injection)──> AI Agent
                                                     │
                                                     ▼ Must forward Token
                                            Database Blocks
                                   ("Token attached lacks DELETE scope -> DENIED")

```

* **Why Identity Systems Fail Here:** The downstream resource checks the **intermediary agent's identity**. Because the agent has broad system privileges, the malicious request executes.
* **Why Capability Systems Succeed Here:** The downstream resource checks the **token presented**. Because the attacker could only pass a low-privilege capability token, the agent lacks the key to execute the malicious action.

---

### 5. Architectural Solution: Hybrid Approach

Modern enterprise architectures (such as Zero Trust and Agentic Frameworks) combine both models to get the benefits of identity governance alongside capability delegation:

1. **Identity at the Boundary:** Users authenticate via **Identity-Based Systems** (SSO / OAuth) at the system edge.
2. **Capabilities at the Core:** The auth server issues a short-lived, scoped **Capability Token** (via OAuth 2.0 Token Exchange / RFC 8693) that captures both the **Original User Identity** (Subject) and the **Intermediary Agent** (Actor).
3. **Dual Verification:** Downstream APIs verify **both** that the original user has permission *and* that the capability token explicitly allows that specific tool call or operation.
