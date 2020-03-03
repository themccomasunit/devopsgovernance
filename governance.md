[[_TOC_]]

# Goals

Our initial focus was to design a model flexible enough that it could easily be extended and adopted by organizations struggling to maintain compliance and audit controls as their software delivery speed increased. We wanted to create a reference architecture that enables an organization to create trust within the process of delivering soft-ware and services. As organizations further automate the continuous delivery of software and services, they also need to ensure there are common validations and trust mechanisms throughout the process. Ultimately, a DevOps automated governance process can give organizations the assurance that the delivery of their software and services are trusted.

The paper is organized into the following sections:

- Definitions and assumptions

- Reference architecture

- Recording attestations

- Summary and next steps

**_Disclaimer_**

The specific purpose of this paper is to introduce a reference architecture for the purposes of automated governance. This paper represents the combined knowledge of the authors&#39; experiences in what should make a good start to create a DevOps automated governance process. We believe that this reference architecture will be a useful starting point for many organizations; however, it is probably not efficient for enterprise scale. It&#39;s the authors&#39; expectation and hope that the DevOps community will engage in ongoing improvement through rigorous validation and continuous feedback. Furthermore, this paper is not intended to cover a comprehensive discussion regarding policy in the delivery pipeline. Though some of the control points described in this paper reference policy, we leave the instrumentation of that policy up to the reader.

# **Definitions and Assumptions**

The following definitions and assumptions are used as the basis for this paper and can be modified to comply with each organization&#39;s preferred terminology.

**_Governance, Risk, and Compliance_**

The complexity of most modern organizations makes it very difficult for one team or even one person to understand a singular, comprehensive view of organizational governance, risk, and compliance. As a result, most organizations typically apply governance, risk, and compliance (GRC) in an uncoordinated and nonaligned fashion.

In _Measuring and Managing Information Risk: A FAIR Approach_, Jack Freund and

Jack Jones describe a more specific overview of GRC as follows:

- **Governance:**&quot;Ultimately, leadership is expected to cost-effectively govern the organization&#39;s risk landscape. Accomplishing this requires setting and communicating expectations, overseeing and facilitating the achievement and maintenance of those expectations, and managing conditions that don&#39;t align with their expectations. GRC solutions are supposed to assist with this by providing a way to report where these expectations are and are not being met, within a meaningful business context.&quot;
- **Risk:**&quot;This objective is all about making better-informed risk decisions, which boils down to three things: (1) identifying &#39;risks,&#39; (2) effectively rating and prioritizing &#39;risks,&#39; and (3) making decisions about how to mitigate &#39;risks&#39; that are significant enough to warrant mitigation.&quot;

- **Compliance:**&quot;Of the three objectives, compliance management is the simplest at least on the surface. On the surface, compliance is simply a matter of identifying the relevant expectations (e.g., requirements defined by Basel, Payment Card Industry (PCI), SOX, etc.), documenting and reporting on how the organization is (or is not) complying with those expectations, and tracking and reporting on activities to close any gaps.&quot;

When thinking about a &quot;DevOps Automated Governance&quot; model, we need to look specifically at _risk_ as a probability or threat of damage, loss, or other negative occurrence that can be caused by external or internal vulnerabilities, and that may be avoided through preemptive action. Risk may manifest as direct or indirect losses. We then apply _governance_ to understand and control risk.

Governance uses _controls_ to mitigate specific risks. Controls can be classified as:

- **Detective:** the control indicates when a risk has already manifested.

- **Corrective:** the control repairs the process to compensate for a risk.

- **Preventive:** the control makes the risk less likely to manifest.

A governance process applies a variety of controls to diminish, mitigate, or respond to various risks. The governance process must both collect evidence that the controls are applied correctly and convey the results of the controls. Output from the controls can be collected in the form of _attestations_, which are witnessed declarations of evidence. Of course, attestations must be recorded in a tamper-resistant mechanism.

A key category of risk is the potential loss due to noncompliance with regulations or laws. Internal and external auditors attempt to verify compliance or detect noncompliance with these laws and regulations. Some examples of questions to be answered by various kinds of audits include:

- Are the company&#39;s financial records accurate?

- Does this piece of automotive software meet safety standards?

- Are the reported results of a drug trial what patients actually experienced?

Companies must periodically present evidence to these auditors that demonstrates compliance. A lack of evidence will be interpreted as noncompliance. Organizations therefore create governance mechanisms to ensure that the necessary evidence exists.

Every audit, for every purpose, requires data that is produced, managed, and reported by software. That means every audit eventually confronts the question of the integrity of that software.

**_Common Terminology_**

Throughout this paper, we will be using specific terms to describe certain aspects related to the DevOps automated governance reference architecture. Since the IT industry tends to overload a lot of this common terminology, we decided to use a common set of definitions for the purposes of this paper, listed below:

- **Delivery Pipeline:** This is the set of stages that describes how software will flow from post ideation to final production delivery. We use this phrase for all references related to industry terms, including but not limited to ARO, continuous delivery and release automation, continuous integration and continuous delivery, orchestration pipeline, release coordination, release management, and software development life cycle. We also decided to use a common set of stages to describe the Delivery Pipeline as seen in Figure 1.

- **Artifact:** An artifact is a deployable component of an application. In this paper, we define an artifact as either an archive file, a virtual machine image, or a container image. It is important to note that different stages of the delivery pipeline might mutate an artifact. For example, in the build stage, an input artifact might come from the dependency management stage. In the package stage, the output artifact might be an immutable packaged version of all the things needed to deploy and run the software in an environment.

--INSERT FIGURE 1--

**Figure 1: Delivery Pipeline**


**_Creating Better Pipelines_**

In May of 2018, Capital One wrote the blog post &quot;Focusing on the DevOps Pipeline&quot; explaining what it means to &quot;deliver high quality working software faster.&quot;4 They describe their policy as such:5

- _High quality_ meaning no security flaws, in compliance, minimum defects, etc.

- _Working_ meaning end to end it really works for all parties, that it&#39;s been tested,and all dependencies are satisfied.
- _Faster_ meaning as soon as possible without sacrificing quality.

The blog post also describes the concepts of &quot;gates,&quot; or guiding design principles, later described as &quot;control points:&quot; At Capital One, they designed pipelines using what they call the 16 Gates. These guiding design principles are as follows:

- Source code version control

- Optimum branching strategy

- Static analysis

- Greater than 80% code coverage

- Vulnerability scan

- Open source scan

- Artifact version control

- Auto provisioning

- Immutable servers

- Integration testing

- Performance testing

- Build deploy testing automated for every commit

- Automated rollback

- Automated change order

- Zero downtime release

- Feature toggle

The design ensures that every time software is pushed through the pipeline these control points will be evidenced.

Control points are a form of both metadata and evidence for actions taken during the development, production, and promotion processes. These control points should be defined at every phase of continuous integration and preserved in logs from the build or logs from how an artifact was built. Ultimately, this kind of automated pipeline metadata in the form of control points allows organizations to move to a decentralized form of decision-making, thus moving away from centralized forms commonly used in most enterprises.

**_DevOps Automated Governance_**

DevOps practices increase the tempo of software delivery. This creates tension with governance programs that rely on the manual review of artifacts, documents, and scans. If we can push a change to production every few minutes, no manual process can keep up. So, just as we have automated testing and deployment processes, we must also seek to automate the governance processes. (And just as automated testing and deployment processes reduce variation and manual error, we should also expect automated governance to enjoy the same benefits.)

Many tools have emerged to address pieces of the governance process. We can regard these individual actions as individual controls. To be integrated into an auto-mated governance process, the output from a control must be recorded as an attestation to confirm the control was applied and describe what the control did. Some examples of attestations collected from controls would include statements such as:

- Control: Unit tests

_Attestation: &quot;All tests executed and passed.&quot;_

- Control: Clean dependencies

_Attestation: &quot;All dependencies in this build satisfy local licensing policies.&quot;_

- Control: Clean dependencies

_Attestation: &quot;All dependencies in this build are free of known security defects.&quot;_

A single control may record more than one attestation. These attestations begin as ordinary tool outputs but need to be collected in a way that auditors can later verify the origin and integrity of the attestation. (An example of a mechanism to collect such attestations is the open-source tool Grafeas, discussed in the next section.)

# **Reference Architecture**

Our reference architecture maps a delivery pipeline to specific controls that will produce evidence for collection. This reference architecture offers a starting point for a DevOps automated governance process. Implementers will add to this architecture and adapt it to their particular tool set and delivery pipeline.

**_Evidence and Automated Traceability_**

In 2017, Google introduced an open-source initiative called Grafeas (the Greek word for &quot;scribe&quot;) to help organizations define a uniform way to audit and govern a modern delivery pipeline. Grafeas supplies a simple reference architecture for a set of APIs to gather metadata (i.e., control points) in a common model. Another open-source initiative designed for a similar purpose is Capital One&#39;s Hygieia.

Consider an example of a control that Grafeas or Hygieia could accept, such as &quot;clean dependencies.&quot; It may be applied by a tool such as Sonatype Nexus. Just applying the tool to keep the dependencies clean, however, is not enough to qualify as auto-mated governance. The missing part is evidence that the control was applied at a point in time to a set of inputs. Figure 2 shows how an attestation may be constructed from a set of inputs that connect the output of a control together with the inputs (including implicit inputs, like configuration).

--INSERT FIGURE 2--

**Figure 2: Constructing an Attestation**

Hashing and message authentication codes provide tamper resistance to the attestation. This attestation can be recorded immutably. A series of attestations can be connected to reconstruct the flow of a change through the delivery pipeline in much the same way a call tree can be reconstructed from individual spans.

_The Model_



The model first describes a typical software delivery pipeline. For each stage the model identifies a set of inputs, outputs, actors, and the actions that can occur at that stage.  Next, the model identifies a set of risks that can be attributed to the stage. Finally, based on the identified risks, a set of controls are chosen to mitigate the risks and attest to the input, output, actors, and actions involved. Figure 3 shows the general process of the governance model.

--INSERT FIGURE--


**Figure 3: Basic Governance Model**



To avoid repetition in every stage, the model factors out a set of common actors and controls that appear in all stages.

Common controls:



- access control

- audit trail/log

- source control

- usage policies Common Actors:
- auditor; risk/compliance office

- the system itself

- tool administrators


_Delivery Pipeline_


Currently, software is delivered via an automated and controlled process called a &quot;pipe-line.&quot; (Figure 1, which you can find earlier in this paper, depicts a general reference for a pipeline.) A typical pipeline is a set of pre-composed stages that integrate with many tools and platforms to automatically send tested changes to production. The pipeline is the heart of an end-to-end delivery life cycle.

Typical pipeline stages and related artifacts are listed below:

- **Source code repository:** A version control tool that hosts all assets related to anapplication&#39;s software and services. Organizations which are mature in DevOps practices use version control for application, infrastructure (as code), tests, and all configurations. (Note that these may not all reside in a single source tree. Application code and production configuration are typically separated according to access rights.) Every change in any code is version controlled. Typically, Git is used to manage this repository.
- **Build:** In this stage, source code is compiled (when a compiled language is used), unit-tested, scanned, and linted for quality and security.
- **Dependency management:** This stage is where external libraries and/or base images (e.g., virtual machines or containers) are stored and from which they are consumed internally. This is the entry point for outside code.
- **Package:** In this stage, the deployable artifact is composed from source code and external dependencies. The artifact may be an archive file, a virtual machine image, or a container image. The resulting package is uploaded to a binary artifact repository.
- **Artifact repository:** This is a version control tool that hosts all packaged artifacts produced via the build and packaging stages. Artifacts in this repository should be immutable.
- **Non-prod deploy:** In this stage the artifact is deployed to one or more non-production environments where various tests are applied. There can be one or more of these stages depending upon the testing needs.
- **Prod deploy:** This is the final stage of a typical pipeline where the tested and approved artifact is finally deployed to the production environment. The actions in this stage can use a variety of roll out and exposure strategies to make the artifact available for use.


# Stage: Source Code Repository


Figure 4 shows a generalized overview of what an automated governance model might look like during the source code repository stage.

--INSERT FIGURE--

**Figure 4: Governance during the Source Code Repository Stage**


The primary actors behind automated tools are the code author and the review-er(s). The actions that instigate the checks associated with this pipeline stage are:

- **Commits:** Triggering precommit hooks, unit tests, and dependency management.
- **Pull requests/merge requests:** Triggering static code analysis, unit tests,and code review.

Input

- **Request for change:** A change in source code is initiated by a request for change; a request for change can be a new feature request, a bug fix request, or a request for refactoring or redesign.

Output

- **New version:** A new version of the code base. In Git terms, it is the new SHA.

Actors

- **Code author:** The person who is making the actual code change.

- **Code reviewer:** The person reviewing code changes.

- **Repository admin:** Also known as the owner(s) of the code repository, this person is also responsible for merging the code change to the main code branch.

Actions

- **Code commit:** The actual code change pushed to a temporary place (such as a fork or a branch).
- **Code review:** Peer reviewing code changes.

- **Change request:** A request to merge the changed code to the main branch. In GitHub, this is called a pull request.

| **Risks**                                                                                                                                                                                                                                           | **Pipeline Controls**                                                                                                                                                                                                              |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Unapproved changes:** Unapproved and unreviewed changes may cause degraded and/or unwanted behavior of the service.                                                                                                                               | **Peer-based code review** (e.g., via GitHub Pull Requests) has been shown to have the greatest impact on code quality.                                                                                                   |
| **Untested changes:** Code changes that are not tested may cause degraded and/ or unwanted behavior of the service.                                                                                                                                 | **Unit test coverage** (e.g., via SonarQube) is typically tracked, as untested functionality tees up significant risk when refactoring, optimizing, or altering API usage.                                                |
| **Unapproved third-party dependency:** Unapproved dependencies can introduce legal and security vulnerabilities in the software.                                                                                                                    | **Clean dependencies** (e.g., via Sonatype Nexus) refers to a check that opensource dependencies satisfy enterprise-level licensing guidelines and are free of known vulnerabilities.                                     |
| **Sensitive information leakage:** Accidentally including sensitive information (e.g., credentials, non-public customer information, system account details, etc.) in the source code can result in legal risk, security incidents, or data breach. | **Information leakage analysis** (e.g., via GitHub pre-commit hooks to grep for sensitive tokens) checks that passwords, access tokens, and other types of sensitive information are not being checked into a repository. |
| **Low quality code sent to production:** Even though new code functions as expected, low quality code may cause operational issues, technical debts in terms of code manageability, extensibility, complexity, etc.                                 | **Static code analysis** (e.g., via MuseDev) involves statically scanning for performance, reliability, and security issues as part of the merge decision for new code.        |


# Stage: Build



Figure 5 shows a generalized overview of what an automated governance model might look like during the build stage.

--INSERT FIGURE--

_**Figure 5: Governance during the Build Stage**_

Input

- **New version of code:** Software is rebuilt on demand or automatically when the source code version is changed.
- **Dependencies:** In many situations, when dependency versions change, soft-ware needs to be rebuilt.
- **Build definition:** Build definition, also known as build script, contains the codified build steps.

Output

- **Artifacts:** The main components of the deployment package that are sent to production

Actors

- **System:** Usually the build stage is triggered by a change in the source code. There is no manual intervention needed in this case.

Actions

- **Build:** The only action in this stage is execution of the build definition.

| **Risks**                                                                                                                                                    | **Pipeline Controls**                                                                                                                                                                                                                                                           |
|----------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Inaccurate, unapproved build configuration:** An inaccurate, unapproved build configuration may produce incorrect build artifacts.                         | **Build configuration in source control and peer reviewed:** As a basic DevOps practice of having “everything as code,” build configurations should be source controlled and peer reviewed just as the application code.                                               |
| **Missing, modified, inconsistent build information:** The build artifact might not be traceable, authentic, or reproducible.                                | **Immutable build and build output:** To ensure that a build cannot be modified after the fact, every build and the output of the build should be immutable.  If any build fails for some reason or the build output is unreliable, a fresh build should be initiated. |
| **Unapproved third-party dependency:** Inclusion of unapproved third-party dependencies in the build stage may result in legal and security vulnerabilities. | **Upstream approved dependency management system:** To ensure that every dependency downloaded is approved for use, the build system should be restricted to use only on an approved dependency management system.                                                     |
| **Build output is untested:** The build output, when deployed to production, may not function as expected.                                                   | **Unit test:** Every build should include unit test execution and should complete successfully only if the unit test pass rate and coverage meet predefined criteria.                                                                                                  |
| **Build output has security vulnerability:** The build output may contain a security vulnerability.                                                          | **Linting:** Every build should scan the source code for code quality and should complete successfully only if the analysis result meets predefined criteria.                                                                                                          |

# Stage: Dependency Management



Figure 6 shows a generalized overview of what an automated governance model might look like during the dependency management stage.

--INSERT FILE--


_**Figure 6: Governance during the Dependency Management Stage**_

Input

- **External artifacts:** These are dependencies that have been downloaded from external repositories.
- **Internal shared artifacts:** Many dependencies are produced internally and shared among others internally.
- **Enterprise usage policies:** Many enterprises maintain specific usage policies for specific types of applications. For example, the enterprise might have a policy that software distributed to customers may not use dependencies with &quot;copy-left&quot; licenses.

Output

- **Artifact:** Artifact that was requested by the build system.

Actors

- **Legal:** Enterprise legal teams create policies based on legal requirements.

- **Information security:** Security teams create policies based on security
- **Architects:** Architects create policies based on architectural requirements that include the health of the dependencies (e.g., age, popularity, activity status, etc.).

- **Developers/engineers:** Developers and engineers are the consumers and creators of dependencies.
- **System:** Systems, such as build systems, download dependencies.

Actions

- **Legal scan:** Dependencies are scanned for legal vulnerabilities.

- **Security scan:** Dependencies are scanned for security vulnerabilities.

- **Manage usage policies:** Legal, security, and architecture teams create dependency usage policies.

| **Risks**                                                                                                                                                                                                                           | **Pipeline Controls**                                                                                                                                                                    |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Unknown and potentially vulnerable dependencies are in use:** One of the biggest risks in software development is the risk of unknowns. This includes the risk of using unknown dependencies that can cause damage in many forms. | **Download only from approved external sources:** Every enterprise should create a list of trusted sources of their dependency needs.                                           |
| **Dependencies may not have proper licensing:** Using incorrectly licensed dependencies can lead to legal issues.                                                                                                                   | **License check:** Dependencies that are downloadable from the dependency management system should have licenses that satisfy enterprise legal requirements and usage policies. |
| **Dependencies may have security vulnerabilities:** Using dependencies with security vulnerabilities is a huge risk across every enterprise.                                                                                        | **Security check:** Dependencies that are downloadable from the dependency management system should meet enterprise security requirements and satisfy usage policies.           |
| **Dependencies may have low quality:** Using low-quality dependencies leads to low-quality software.                                                                                                                                | **Dependency quality check:** Dependencies that are downloadable from the dependency management system should meet architecture standards and should satisfy usage policies.    |
| **Unapproved versions are in use:** Using unapproved versions of dependencies may result in security or legal issues. This may also cause systems in production to behave unexpectedly.                                             | **Approved versions:** Only approved versions of dependencies are made available.                                                                                               |

# Stage: Package

Figure 7 shows a generalized overview of what an automated governance model might look like during the package stage.

--INSERT FIGURE--


**Figure 7: Governance during the Package Stage**


Input

- **Artifacts:** The build artifacts that need to be packaged.

- **Dependency:** Dependencies that are not packaged in build artifacts

- **Configuration:** Configurations that are required to run the software in an environment

• **Runtime:** Any runtime that should be packaged for deployment. This may include base images, virtual machines, etc.

Output

- **Artifact:** At this stage, the artifact is a packaged version of all the elements needed to deploy and run the software in an environment.

Actors

- **Engineers:** Developers, operations admin, and system admin who contribute to the packaging process.
- **System:** The automated way in which the packaging step is executed

Actions

- **Package:** The automated process that creates a deployable artifact.

- **Scan:** The process to scan the deployable artifact to detect legal and security

| **Risks**                                                                                                                                                                                                                                   | **Pipeline Controls**                                                                                                                                                                                                                                                                                                                                                                     |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Unapproved, potentially vulnerable third-party dependencies are packaged in the deployable artifact:** Third-party dependencies downloaded during the packaging process may contain vulnerabilities that cause legal and security issues. | **Packaging only from trusted dependency sources:** Packaging system should download dependencies only from trusted dependency sources.                                                                                                                                                                                                                                          |
| **Components with vulnerabilities are packaged in the deployable artifact:** Internal components produced by the build’s vulnerabilities may cause security issues.                                                                         | **Vulnerability scanning:** Even trusted dependency management sources may contain dependencies with vulnerabilities. New vulnerabilities are discovered every day. The packaging system should execute a vulnerability scan just like the build system against the latest vulnerability data to detect vulnerabilities that were potentially undetected during the build stage. |
| **Software configuration contains vulnerabilities:** Even though the actual software may not have vulnerabilities, configurations can contain data that do not meet security standards. These may cause security issues.                    | **Digital signing:** The packaging system should digitally sign the deployable artifact to ensure authenticity.                                                                                                                                                                                                                                                                  |
| **Untraceable software changes:** Packaged artifacts containing changes that cannot be traced back to source code or approved dependencies may cause unpredictable behavior in the software.                                                | **Artifact versioning and metadata:** Every artifact produced by the packaging system should be immutable and versioned with an approved versioning scheme. The packaging system also should add metadata to the deployable artifact.                                                                                                                                            |
| **Unreliable metadata:** Unreliable or missing artifact metadata may cause confusion and at times can cause incorrect software to be deployed in production.                                                                                |                                                                                                                                                                                                                                                                                                                                                                              |

# Stage: Artifact Repository



Figure 8 shows a generalized overview of what an automated governance model might look like during the artifact repository stage.

--INSERT FIGURE--

**Figure 8: Governance during the Artifact Repository Stage**

Input

- **Artifact:** The artifact uploaded by the packaging system and downloaded during the deployment stage.
- **Metadata:** The metadata to add to the artifact.

- **Usage policy:** Enterprise policy on the upload and download of artifacts.

Output

- **Artifact:** The artifact downloaded by the deployment system.

Actors

- **Engineers:** Developers, operations admin, and system admin who contribute to the packaging process.
- **System:** The automated way in which the packaging step is executed.

Actions

- **Upload:** Uploading of artifacts by packaging system.

- **Download:** Downloading of artifacts by deployment system.

| **Risks**                                                                                                                                                                            | **Pipeline Controls**                                                                                                                                                                                                                                          |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Untrusted packaging store:** An unknown or untrusted packaging store can upload vulnerable and/or unapproved artifacts.                                                            | **Only allow upload from trusted packaging source:** Configure the artifact repository to accept upload requests only from known and trusted packaging sources. Many enterprises restrict individual users from uploading to the artifact repository. |
| **Artifact modified after packaging and before deployment:** If an artifact can be modified before deployment, there will be no assurance of the integrity of what will be deployed. | **Immutable artifact:** No artifact in the repository can be overwritten; only a newer version of the same artifact can be uploaded.                                                                                                                  |
| **Loss of previously deployed artifact:** Most enterprises need to archive older versions of software to meet legal and regulatory requirements                                      | **Retention policy:** The artifact repository should implement a retention policy for all released artifacts.                                                                                                                                         |

# Stage: Non-Prod Deploy



Figure 9 shows a generalized overview of what an automated governance model might look like during the non-prod deploy stage.

--INSERT FIGURE--

**Figure 9: Governance during the Non-Prod Deploy Stage**

Input

- **Artifact:** The artifact that will be deployed.

- **Environment configuration:** Any environment configuration that was not or cannot be packaged.
- **Test data:** Any test data set needed to execute tests in the non-production
- **Test configuration:** Any configuration needed to execute test cases in the non-production environment.
- **Executable tests:** Tests that can be executed in the non-production environment

Output

- **Trusted release candidate:** A successful completion of this stage produces are lease candidate that can be trusted, provided all controls in previous stages were in place and followed.

Actors

- **Engineers:** The developers, operations admin, and system admin who contribute to the packaging process.
- **System:** The system executes the packaging step in an automated way.

- **Product owners, business partners:** Product owners involved in testing functionalities in the non-production environment.
- **Information security:** Information security team may run security related tests in non-production environment

Actions

- **Deployment:** The process that deploys an artifact.

- **Run tests:** Various types of tests executed in the non-production environment

| **Risks**                                                                                                                                                                                                                                                                | **Pipeline Controls**                                                                                                                                                                                                                                                                                                                                                                                                        |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Deployment of artifact from untrusted sources:** There is the risk of testing the wrong software before producing a release candidate.                                                                                                                                 | **Fetch artifact only from trusted source:** The non-production deployment stage should fetch deployable artifacts only from trusted sources (such as the enterprise’s artifact repository).                                                                                                                                                                                                                        |
| **Non-production systems with unapproved network configuration:** With an unapproved network configuration, there is the risk of executing tests with unpredictable results or untrusted results.                                                                        | **Whitelist of allowed connectivity:** The connections allowed in the nonproduction deployment stage should be reviewed and kept up-to-date. Preapproved connections on the whitelist should not be allowed.                                                                                                                                                                                                        |
| **Non-production systems with production data:** In many enterprises, non-production systems should never have production data due to legal and privacy risks.                                                                                                           | **Whitelist of allowed data:** The non-production deployment stage should have access to only a set of whitelisted test data. This data should not contain any real customer data or sensitive information.                                                                                                                                                                                                         |
| **Promotion to non-production systems did not have quality gates:** Without a set of checks, or quality gates, there is the risk of producing a release candidate that has low quality, and can potentially produce unpredictable results in the production environment. | **Quality gate evaluation:** Non-production deployment should be executed only if it meets a set of predefined criteria (e.g., 100% test pass rate with 80% coverage, no new high severity security vulnerability, etc.). The quality gate also should consider the drift and difference between production and non-production environments; the non-production environment should mimic the production environment. |

_Stage: Prod Deploy_



Figure 10 shows a generalized overview of what an automated governance model might look like during the prod deploy stage.

--INSERT FIGURE--

**Figure 10: Governance during the Prod Deploy Stage**

Input

- **Artifact:** The artifact that will be deployed.

- **Environment configuration:** Any environment configuration that was not or cannot be packaged.

- **Deployment strategy:** A deployment strategy that is scripted and/or

Output

- **Service availability:** Availability of service with expected behavior.

Actors

- **Engineers:** The developers, operations admin, and system admin who contribute to the deployment process.
- **System:** The system executes the deployment stage in an automated way.

- **Product owners, business partners:** The product owners involved in making decisions of production release readiness and testing out functionalities in the production environment.
- **Information security:** The information security team runs security related checks in production environment.
- **Customers/users:** Who uses the service.

Actions

- **Production deployment:** Execution of the deployment process.

| **Risks**                                                                                                                                                                                                                                                                | **Pipeline Controls**                                                                                                                                                                                                                                                                                                                                                                                                        |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Deployment from untrusted sources.                                             | **Fetch artifact only from trusted source:** The production deployment stage should fetch deployable artifacts from only trusted sources (such as the artifact repository).                                         |
| Production systems have unapproved configuration.                              | **Only use approved configurations:** The production system should use an approved set of configurations, such as network connectivity, encryption, tokenization, secrets management, etc.                          |
| Production systems lack vulnerability detection mechanism.                     | **Security monitoring:** The production system should have intrusion detection, threat monitors, and other approved security mechanisms. It should also have approved monitoring, logging, and alerting mechanisms. |
| Low quality software deployed to production.                                   | **Change management:** The production system should have an automated change management mechanism.                                                                                                                  |
| Lack of ability to detect and resolve production issues.                       | **Access control:** The production system should have a strict access control mechanism. By default, no one should have access to production systems except by means of a break-glass mechanism.                    |
| Unauthorized changes to production systems.                                    | **Deployment strategy enforced:** Production deployment should enforce deployment strategy (e.g., deploy only during a specified time window, use blue-green deployment, use canary deployments, etc.).             |
| Unauthorized access to production systems.                                     |                                                                                                                                                                                                                 |
| Lack of strategy around production system changes causing unexpected behavior. |                                                                                                                                                                                                                 |

# **Recording Attestations**



_Example with Universal Metadata API_



In practice, each automated governance solution will be contextual to each organization and will require different considerations and controls. For example, organizations that require compliance with self-identifying risk control self-assessments might need extensive design for functional and non-functional test acceptance. When digesting some of the intense complications driven from compliance, audit, and risk, each organization must do their due diligence in creating a solution that is personalized to their needs.

In this example, we assume the software delivery pipeline uses the following practices: