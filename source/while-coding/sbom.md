# SBOM

### Reference:

### SBOM types

https://www.cisa.gov/sites/default/files/2023-04/sbom-types-document-508c.pdf

### SBOM use

https://www.cisa.gov/sites/default/files/2024-07/SBOM%20FAQ%202024.pdf

### SBOM data field definitions

https://www.ntia.gov/files/ntia/publications/framingsbom_20191112.pdf



### path to generate an SBOM

- Understand the types and decide which one is needed
- Decide how many levels of depth is required
- where would you publish? or will it be distributed on-demand
- sign an sbom

## GitHub dependency tracking and SBOM

GitHub can create dependency graph and SBOM for each repository. Go to repository > Insights > dependency graph to enable it for the first time. If it is already enabled, you'll see a page like this listing `declared dependencies` (in pom.xml) and a prompt to enable `automatic dependency submission`:

![image](https://github.com/user-attachments/assets/3441f3a6-15c4-4bde-ac84-2ac4930c03b4)

`Ecosystem` means that different package managers available in your repo, i.e maven, node, etc. Each of these package managers have typically a file that lists all the dependencies, for pom.xml for maven. GitHub automatically identifies these files for supported [package ecosystems](https://docs.github.com/en/code-security/supply-chain-security/understanding-your-software-supply-chain/dependency-graph-supported-package-ecosystems#supported-package-ecosystems) and lists the dependencies. 

Analysing transitive dependencies:

Github by default, only analyses the `declared dependencies`. Exported SBOM will also only contain `declared dependencies`. But if you enable `automatic dependency submission`, then github will go and find out all the transitive dependencies too. To enable `` GitHub doesn't support analysis of transitive dependencies on all the package ecosystems. See the listing in the link above. 

To turn on the automatic dependency reporting, go to `repository settings > code security`. As soon as you do that, you'll see a new github action job being triggered to analyse your project. See this job running under `actions` tab. In sometime you'll see the dependency graph has lot more dependencies due to addition of transitive dependencies.







