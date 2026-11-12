# Gemara

- Policy, Evaluation, Enforcement, and Audit

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

