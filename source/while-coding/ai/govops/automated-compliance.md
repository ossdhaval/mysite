# Automated compliance

The sequence:

- compliance standards (SOC2, GDPR, etc) publish their controls in OSCAL catalog.json format. NIST already does. GDPR and SOC2 has community versions, or can be hand written. An OSCAL catalog.json only contains control definitions, IDs, and requirement prose.
- Take this catalog.json and convert it into gemara `controls.yaml` using conversion tools. 
  - Gemara CLI / SDK (gemara Go library & CLI): Includes conversion utilities (oscal-to-gemara / importers) that parse an official NIST OSCAL catalog JSON and output baseline Gemara Control YAML files—preserving the NIST control IDs (e.g., SI-7, CM-2), titles, and requirement statements automatically.
  - OSCAL Compass Trestle (trestle): If your compliance team gives you the full 1,000+ control NIST SP 800-53 catalog, and you only need to pick a few then use trestle author profile-generate or trestle split first to filter down to only the 10 controls you care about before converting them to Gemara YAML.
  - capability, policy, control, threat yaml files
- You write your Gemara Capability, Threat, and Policy YAML files in Git and use `reference-id` pointers to wire them to those imported controls.
- Use gemara files to monitor the process and see if there are any compliance issues
- Auto-generate OSCAL files (catalog.json, assessment-plan.json, and assessment-results.json) and use them to share information across tools. Catalog.json comes from gemara's controls.json, The other two as mentioned below.
  - Stage 1: Generating the OSCAL Assessment Plan (complyctl plan): You do not write assessment-plan.json manually; complyctl compiles it by merging your Gemara Policy with your Control Catalog.
    - Reads Policy Scope & Imports: complyctl opens your Gemara policy.yaml, reads which control catalogs are imported (imports.catalogs), and checks which controls are actually in scope (scope.in / tailored requirements).
    - Extracts Assessment Methods: It looks at the adherence.assessment-plans block in your Gemara policy to see how each control should be evaluated (for example, executor: ampel-plugin).
    - Compiles assessment-plan.json: Using OSCAL schema builders, it translates those Gemara entries into standard OSCAL constructs:
      - Gemara requirement-id entries become OSCAL reviewed-controls.control-selections.
      - Gemara evaluation-methods become OSCAL tasks and activities, complete with fresh UUIDs and href links pointing back to the catalog.
  - Stage 2: Generating the OSCAL Assessment Results (complyctl scan): Once assessment-plan.json exists, complyctl acts as a coordinator between the plan, your evaluator plugin (like Ampel), and the final OSCAL output.
    - Prepares Plugin Instructions (complyctl generate): complyctl reads assessment-plan.json and generates a plugin-specific configuration file telling Ampel which checks to run and which artifacts/evidence to inspect.
    - Runs the Evaluator (complyctl scan): complyctl invokes the Ampel provider plugin over gRPC/CLI. Ampel evaluates the raw evidence (e.g., verifying the Cosign signature on your container image) and returns raw pass/fail verdicts to complyctl.
    - Normalizes Findings via C2P / Trestle: Raw tool output from Ampel is not valid OSCAL. complyctl uses normalization logic (the same pattern as OSCAL Compass's Compliance-to-Policy / C2P) to map Ampel's pass/fail output into OSCAL structures:
      - Ampel's raw verification log + timestamp becomes an OSCAL observation (with a new uuid).
      - The pass/fail verdict becomes an OSCAL finding (status.state: "satisfied" or "not-satisfied"), linked to that observation's UUID and tagged with the original control-id from the plan.
    - Writes assessment-results.json: complyctl wraps those observations and findings inside an OSCAL assessment-results envelope, sets import-ap to point to ./assessment-plan.json, and writes the final JSON file to disk.


- Policy, Evaluation, Enforcement, and Audit


## Example of how OSCAL and Gemara are related

It starts will your org deciding which are compliance rules applicable to it. 

For our use case, the org enforcing that every production container image is signed before deployment. 
For this compliance rule, the org builds a OSCAL catalog. That describes the compliance item.

`catalog.json`

```json
{
  "catalog": {
    "uuid": "11111111-1111-4111-8111-111111111111",
    "metadata": {
      "title": "Container Security Baseline Catalog",
      "last-modified": "2026-11-13T10:00:00Z",
      "version": "1.0.0",
      "oscal-version": "1.1.2"
    },
    "controls": [
      {
        "id": "ctrl-signed-images",
        "title": "Require Signed Production Container Images",
        "parts": [
          {
            "id": "ctrl-signed-images_smt",
            "name": "statement",
            "prose": "All container images deployed to production environments must carry a valid cryptographic signature."
          }
        ]
      }
    ]
  }
}
```

Then they build an assessment plan. `assessment-plan.json`.

```json
{
  "assessment-plan": {
    "uuid": "22222222-2222-4222-8222-222222222222",
    "metadata": {
      "title": "Production Image Signature Assessment Plan",
      "last-modified": "2026-11-13T10:15:00Z",
      "version": "1.0.0",
      "oscal-version": "1.1.2"
    },
    "import-ssp": {
      "href": "./system-security-plan.json"
    },
    "reviewed-controls": {
      "control-selections": [
        {
          "include-controls": [
            {
              "control-id": "ctrl-signed-images"
            }
          ]
        }
      ]
    },
    "tasks": [
      {
        "uuid": "33333333-3333-4333-8333-333333333333",
        "type": "action",
        "title": "Verify cryptographic signature on production container images"
      }
    ]
  }
}
```

`control-id` connects the plan with the actual compliance item.

Then org runs some technical tool(via Ampel or complyctl) that helps acertain that only signed images were deployed. That tool has to produce results in OSCAL result format as below.

```
{
  "assessment-results": {
    "uuid": "44444444-4444-4444-8444-444444444444",
    "metadata": {
      "title": "Production Image Signature Scan Results",
      "last-modified": "2026-11-13T10:30:00Z",
      "version": "1.0.0",
      "oscal-version": "1.1.2"
    },
    "import-ap": {
      "href": "./assessment-plan.json"
    },
    "results": [
      {
        "uuid": "55555555-5555-4555-8555-555555555555",
        "title": "Automated Container Signature Verification Run",
        "start": "2026-11-13T10:29:50Z",
        "end": "2026-11-13T10:30:00Z",
        "reviewed-controls": {
          "control-selections": [
            {
              "include-controls": [
                {
                  "control-id": "ctrl-signed-images"
                }
              ]
            }
          ]
        },
        "observations": [
          {
            "uuid": "66666666-6666-4666-8666-666666666666",
            "description": "Ampel verified Cosign signature on ghcr.io/org/payment-service:v1.4.2",
            "methods": ["TEST-AUTOMATED"],
            "collected": "2026-11-13T10:29:55Z"
          }
        ],
        "findings": [
          {
            "uuid": "77777777-7777-4777-8777-777777777777",
            "title": "Signature Check Passed",
            "description": "Production image carries a valid signature from the release pipeline.",
            "target": {
              "type": "objective-id",
              "target-id": "ctrl-signed-images",
              "status": {
                "state": "satisfied"
              }
            },
            "related-observations": [
              {
                "observation-uuid": "66666666-6666-4666-8666-666666666666"
              }
            ]
          }
        ]
      }
    ]
  }
}
```

- How the Traceability Chain Works Here
  - Result → Observation: The finding (7777...) points to observation-uuid: 6666..., proving why it passed (Ampel checked the Cosign signature at 10:29:55Z).
  - Result → Control: The finding's target-id points to ctrl-signed-images, linking the technical evidence back to the exact rule in catalog.json.
  - Result → Plan: import-ap links the outcome back to assessment-plan.json, showing it was executed under an approved assessment scope.

Three OSCAL documents act as a linked pipeline. Every OSCAL file relies on uuid values and href pointers to connect what you require (Catalog), how you plan to test it (Assessment Plan), and what actually happened (Assessment Results).

Now, why do we need Gemara ?

Looking at those three OSCAL JSON files, you might wonder why you even need Gemara if OSCAL already tracks controls, plans, and results.

The gap is that OSCAL is built for compliance reporting, not day-to-day engineering governance. It is a heavy, verbose interchange format designed for GRC tools and auditors. It lacks clean, developer-friendly abstractions for modeling why a rule exists or how an organization actually operates.

Gemara fills four gaps:

- Accountability
  - Gemara adds a Policy layer that captures governance metadata: who is responsible (Platform Team), who is accountable (VP of Engineering), which technologies are in scope (Payment Service), and what the organization's risk appetite is. In the OSCAL catalog.json above, these information is missing. This information is critical if organizational usage.
- Threat-to-Capability Context (Connecting Rules to Real System Actions)
  - In assessment-plan.json, the task says "Verify cryptographic signature on production container images," but OSCAL doesn't model the attack vector or the exact API/system behavior being guarded.
  - What Gemara adds: Explicit, structured links between Controls, Threats (`unsigned-code-execution`), and Capabilities (`image-deploy`). When a check fails in production, Gemara tells the engineer which specific system action is exposed and which threat just became active—not just a dry compliance ID.
- YAML Vs UUID based JSON
  - Gemara adds Clean, human-readable YAML (backed by strict CUE schemas) that developers can review in a Git pull request just like Kubernetes manifests or Terraform files. Tools like complyctl can then translate Gemara models into OSCAL when an auditor or GRC platform needs it.
- Reusability Across Frameworks
  - If tomorrow your company needs to satisfy SOC 2, ISO 27001, and the EU AI Act, raw OSCAL often forces you to duplicate assessment plans across separate catalogs. What Gemara adds: A decoupled middle layer. You map your Capabilities and Threats once to your actual engineering systems, and multiple external compliance catalogs can point to the same underlying Gemara controls without rewriting your technical checks.


## why we need Gemara

Automated governance: 

Below is from: [CNCF automated governance maturity model](https://tag-security.cncf.io/community/resources/automated-governance-maturity-model/#automated-governance-maturity-model).

Automated governance involves leveraging technology, automation, and data-driven systems to ensure that an organization operates efficiently, complies with regulations, and achieves strategic objectives.

Automated governance in cloud-native security ensures consistent enforcement of security and compliance policies at scale, reducing human error and improving efficiency. By leveraging Policy-as-Code (PaC), security teams can automate policy enforcement in CI/CD pipelines, Kubernetes clusters, and cloud environments, ensuring continuous compliance with frameworks like NIST 800-53, PCI-DSS, and SOC 2. It enhances risk mitigation, auditability, and incident response by providing real-time drift detection and security posture management. With tools like OPA, Kyverno, CSPM, and CIEM, organizations can secure cloud-native workloads without slowing down development, making automated governance a critical component of DevSecOps and cloud security strategies.


NOTE: 
The [policy section](https://tag-security.cncf.io/community/resources/automated-governance-maturity-model/#policy), point number 9, makes a case for Cedar policy store authzen draft. The point says `Policies are automatically distributed to relevant tooling across the organization, such as policy engines or assessment tools.`. Cedar doesn't have a way to distribute policy(with its context) across tools.


An evaluation should target a specific application or service, and be composed of multiple assessments. Each assessment may have multiple steps corresponding to an assessment requirement in a control that is deemed applicable according to organizational policy. A finding is any result that fails or requires manual review.

- DevOps scenarios where policy/compliance are important:
  - Developers(using k8s manifest) should not be able to request PODs with more than 8 GB RAM
  - Developers must use a specific version of nginx (or from a set of approved versions) for creating kubernetes pods
  - Developers must mention the name of the team in the manifest yaml.
  - When a database container is requested, it must be requested with encryption `on`.
 
## Standard definitions for GRC

These definitions are from: [Institute of internal auditors](https://www.theiia.org/globalassets/site/resources/statements-of-position/tlm_assurance_advice_support_effective_gov_en.pdf)

- governance – The combination of processes and structures implemented by the
board to inform, direct, manage, and monitor the activities of the organization toward
the achievement of its objectives
- control – Any action taken by management, the board, and other parties to manage
risk and increase the likelihood that established objectives and goals will be
achieved
- assurance – Statement intended to increase the level of stakeholders’ confidence
about an organization’s governance, risk management, compliance, and control
processes.


- Provenance is “the chronology of the origin, development, ownership, location, and changes to a system or system component and associated data. It may also include personnel and processes used to interact with or make modifications to the system, component, or associated data”

- Important foundational documents that requires GRC in software development:
  - [Secure Software Development Framework (SSDF)](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-218.pdf)
  - [DoD Enterprise DevSecOps Reference Design](https://dodcio.defense.gov/Portals/0/Documents/DoD%20Enterprise%20DevSecOps%20Reference%20Design%20v1.0_Public%20Release.pdf)
- NIST controls: https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf

### NIST controls

Excerpt to understand `requirement` vs `control`:

```
It is important to understand the relationship between requirements and controls. For federal
information security and privacy policies, the term requirement is generally used to refer to
information security and privacy obligations imposed on organizations. For example, [OMB A130] imposes information security and privacy requirements with which federal agencies must
comply when managing information resources. The term requirement can also be used in a
broader sense to refer to an expression of stakeholder protection needs for a particular system
or organization. Stakeholder protection needs and the corresponding security and privacy
requirements may be derived from many sources (e.g., laws, executive orders, directives,
regulations, policies, standards, mission and business needs, or risk assessments). The term
requirement, as used in this guideline, includes both legal and policy requirements, as well as an
expression of the broader set of stakeholder protection needs that may be derived from other
sources.

Controls can be viewed as descriptions of the safeguards and protection capabilities appropriate
for achieving the particular security and privacy objectives of the organization and reflecting the
protection needs of organizational stakeholders. Controls are selected and implemented by the
organization in order to satisfy the system requirements. Controls can include administrative,
technical, and physical aspects. In some cases, the selection and implementation of a control
may necessitate additional specification by the organization in the form of derived requirements
or instantiated control parameter values. The derived requirements and control parameter
values may be necessary to provide the appropriate level of implementation detail for particular
controls within the SDLC.
```

