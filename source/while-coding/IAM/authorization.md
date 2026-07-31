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
