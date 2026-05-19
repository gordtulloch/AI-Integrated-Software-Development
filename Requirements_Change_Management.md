# Managing Requirements Change in AI-Integrated Software Development: A Process Framework for Post-Generation Change Documentation, Integration, Implementation, and Deployment

**Gordon Tulloch**
Director of Information & Communications Technologies
Sunrise School Division

---

*Abstract* — Requirements change is not an exception in software development — it is an expected and inevitable property of systems that exist in evolving organisational, technological, and regulatory environments. In AI-integrated development workflows governed by formal specification hierarchies, requirements change after code generation presents a distinctive challenge: the tight coupling between the Project Scope Document, Software Requirements Specification, Software Design Description, Traceability Matrix, test suite, and generated codebase means that a change originating in any layer propagates consequences through all others. Without a disciplined change management process, the specification-code consistency that is the primary quality assurance mechanism of specification-driven AI development is rapidly eroded. This paper proposes a structured Requirements Change Management (RCM) process designed specifically for AI-integrated development environments operating within the workflow described in Tulloch (2025). The process addresses four sequential stages — change documentation, impact analysis, implementation, and deployment — and integrates AI-assisted tooling at each stage while preserving human expert authority over change authorisation and verification decisions. The paper identifies four categories of requirements change (corrective, adaptive, perfective, and preventive), characterises the response appropriate to each, and describes the artifact lifecycle implications of change propagation through the specification hierarchy. The framework treats the Traceability Matrix as the central instrument of change impact analysis and the Change Log as the institutional record of change rationale.

**Keywords:** requirements change management, change impact analysis, traceability, AI-assisted development, software maintenance, specification-driven development, ripple effect, change propagation

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Background and Related Work](#2-background-and-related-work)
3. [A Taxonomy of Requirements Change](#3-a-taxonomy-of-requirements-change)
4. [The Specification Hierarchy and Change Propagation](#4-the-specification-hierarchy-and-change-propagation)
5. [Stage 1 — Change Identification and Documentation](#5-stage-1--change-identification-and-documentation)
6. [Stage 2 — Change Impact Analysis](#6-stage-2--change-impact-analysis)
7. [Stage 3 — Change Implementation](#7-stage-3--change-implementation)
8. [Stage 4 — Verification and Deployment](#8-stage-4--verification-and-deployment)
9. [The Change Control Board](#9-the-change-control-board)
10. [AI Assistance in the Change Management Process](#10-ai-assistance-in-the-change-management-process)
11. [Change Management in Lightweight Workflow Variants](#11-change-management-in-lightweight-workflow-variants)
12. [Discussion](#12-discussion)
13. [Conclusion](#13-conclusion)
14. [References](#14-references)
15. [Appendix B — Change Management Templates and Prompt Structures](#appendix-b--change-management-templates-and-prompt-structures)

---

## 1. Introduction

The specification-driven AI development workflow described in Tulloch (2025) is premised on a hierarchy of formally specified, traceable artifacts that collectively define what a system must do, how it is designed to do it, and how its correctness is verified. This hierarchy — Project Scope Document (PSD), Software Requirements Specification (SRS), Software Design Description (SDD), Traceability Matrix (TM), test suite, and generated codebase — derives its quality assurance value from its internal consistency. Each artifact is correct relative to the ones above it; the system as a whole is correct if the chain of consistency holds from the PSD to the deployed code.

Requirements change after code generation breaks this chain. A new stakeholder requirement, a regulatory update, a discovered defect, or a change in the operational environment may necessitate a revision to any point in the hierarchy, with consequences that propagate — sometimes unpredictably — through all downstream artifacts. Even a small software change can ripple through to cause a large unintended impact elsewhere in the system, making it difficult to identify all affected functionalities. In a specification-driven AI development context, this ripple effect has two dimensions: the functional dimension familiar from traditional software maintenance, and a *specification consistency dimension* unique to AI-assisted workflows, in which an inconsistency between the specification and the codebase undermines the team's ability to use AI generation for future changes.

This paper proposes a four-stage Requirements Change Management (RCM) process designed for AI-integrated development environments. The process covers change documentation, impact analysis, implementation, and deployment, and is designed to preserve the specification-code consistency that is the foundation of the workflow's quality assurance properties. It treats requirements change not as a workflow failure but as a normal, planned activity for which systematic tooling and process discipline are required.

The paper makes the following contributions:

1. A taxonomy of requirements change types applicable to AI-integrated development, with characterisation of the response appropriate to each type.
2. A description of how change propagates through the specification hierarchy defined in Tulloch (2025), identifying the scope of artifact updates required for each change category.
3. A four-stage RCM process that integrates AI-assisted tooling while preserving human authority over change authorisation and verification.
4. Templates for the Change Request Form, Impact Analysis Report, and Change Log entry.
5. Guidance on scaling the change management process for lightweight workflow variants appropriate to smaller projects or more volatile domains.

---

## 2. Background and Related Work

### 2.1 The Inevitability of Requirements Change

Requirements change is one of the most extensively documented phenomena in software engineering. Changes to software requirements are inevitable during the development process. Despite many software engineering advances over several decades, requirements changes are a source of project risk, particularly when businesses and technologies are evolving rapidly. The International Requirements Engineering Board and ISO 29148 both treat requirements change management as a mandatory component of any complete requirements engineering process (Bühne & Herrmann, 2022).

Empirical studies of maintenance effort have consistently found that the majority of software maintenance work is not defect correction but requirements evolution. The foundational Lientz and Swanson (1980) study of 487 organisations found that over half of all maintenance effort was devoted to perfective maintenance — the addition or modification of features in response to evolving user needs — with adaptive and corrective maintenance accounting for most of the remainder. More recent studies have confirmed that this distribution persists in contemporary software organisations, with requirements-driven change consistently representing the dominant maintenance category (Chapin et al., 2001).

### 2.2 Requirements Change Management Frameworks

According to the International Requirements Engineering Board and ISO 29148, the requirements change management process includes important activities such as change identification, change impact analysis, change authorisation, change implementation, and change verification. The literature on requirements change management (RCM) has produced several process frameworks addressing these activities, ranging from the lightweight change control processes associated with agile development to the formal change control boards and configuration management systems of plan-driven approaches.

A key motive of research in this area is to develop requirement change management processes that help practitioners assess and manage their RCM activities. Critical success factors identified across the literature include adequate traceability and monitoring of RCM activities, and collaboration and communication among project stakeholders. The framework proposed in this paper draws on these foundations while extending them to address the specific challenges of AI-integrated development.

### 2.3 Change Impact Analysis and Traceability

Change impact analysis (CIA) is the activity of determining the consequences of a proposed change before it is implemented. Software change impact analysis is the activity of the software maintenance process that determines possible effects of proposed software changes. A change has not only impact on the source code, but also on other related software artefacts such as requirements, design, and test. For this reason, impact analysis can be efficiently supported through traceability information.

The role of traceability in supporting impact analysis is well established. Software traceability and its subsequent impact analysis help relate the consequences or ripple-effects of a proposed change across different levels of software models, integrating the high level with the low level software models that involve the requirements, test cases, design and code. The Traceability Matrix defined in Tulloch (2025) is, by design, the primary instrument for this analysis in the proposed workflow.

### 2.4 LLM-Assisted Change Impact Analysis

A significant recent development is the application of LLMs to requirements change impact analysis specifically. Accurate impact assessment is essential not only for minimising unintended side effects but also for supporting cost estimation, prioritisation, and strategic decision-making in software maintenance and evolution. Throughout the software development lifecycle, requirements are often subject to rapid changes, and LLM-driven approaches offer cost-effective mechanisms for identifying affected requirements and artifacts. This emerging body of work provides direct support for the AI-assisted impact analysis component of the process proposed in this paper.

---

## 3. A Taxonomy of Requirements Change

Not all requirements changes are equivalent in their origin, their urgency, or their implications for the specification hierarchy. The classical Lientz-Swanson taxonomy of software maintenance, as updated by ISO/IEC 14764 (2006), provides a practical classification scheme for requirements changes that is directly applicable to AI-integrated development contexts.

### 3.1 Corrective Changes

A corrective change addresses a defect: a discrepancy between the system's specified behaviour and its actual behaviour. In specification-driven AI development, corrective changes may originate in three locations. A *specification defect* exists when the SRS contains an incorrect, ambiguous, or contradictory requirement that was never correctly implemented. An *implementation defect* exists when the specification is correct but the generated code fails to satisfy it. A *test defect* exists when the test cases fail to detect an implementation defect that is later discovered in production.

The response to each defect location differs. Specification defects require updates to the SRS and potentially the SDD before code correction, using the full specification update process. Implementation defects may be corrected at the code level without specification changes, but must be verified against the existing specification and documented in the Change Log. Test defects require test case revision before implementation correction.

**Urgency:** Typically high. Corrective changes address failures affecting current users or system integrity.

**Specification hierarchy impact:** Varies by defect location; ranges from test-only updates to full specification-to-code propagation.

### 3.2 Adaptive Changes

An adaptive change responds to a change in the system's external environment: a new operating system version, a changed external API, an updated regulatory requirement, a new integration partner, or a change in the infrastructure on which the system runs. The system's specified behaviour may remain entirely correct — the change is required not because the system is wrong but because the world around it has changed.

Adaptive changes are among the most disruptive to the specification hierarchy because they may require substantive updates to the Technical Constraints section of the PSD, the interface requirements in the SRS, the deployment and integration architecture in the SDD, and significant portions of the integration-layer code. Regulatory adaptive changes (new data privacy laws, revised accessibility standards, updated security baselines) frequently propagate to constraint and compliance requirements (CR-XXX identifiers in the SRS) and may require audit documentation updates.

**Urgency:** Variable; externally imposed deadlines (regulatory compliance dates, API deprecation timelines) determine urgency.

**Specification hierarchy impact:** Typically moderate to high; integration and deployment layers most commonly affected.

### 3.3 Perfective Changes

A perfective change introduces new capabilities or improves existing ones in response to evolving stakeholder needs, competitive pressure, or user feedback. Perfective changes represent the majority of post-deployment requirements work — Lientz and Swanson's foundational study found that perfective maintenance, representing new functional or non-functional requirements, accounted for the largest share of maintenance effort by a substantial margin.

In AI-integrated development, perfective changes are the category for which the workflow's specification-first discipline provides the greatest long-term benefit. A well-maintained specification hierarchy makes it possible to evaluate a proposed perfective change against the existing system design before any implementation occurs, identifying conflicts and dependencies that would otherwise only emerge during coding. The AI can then be leveraged to generate specification updates and implementation code for the new capability in exactly the same way as in the original development workflow.

**Urgency:** Typically low to medium; driven by product roadmap and stakeholder priorities rather than operational failures.

**Specification hierarchy impact:** Highest of all change types; new capabilities require new SRS requirements, SDD design elements, TM entries, test cases, and generated code.

### 3.4 Preventive Changes

A preventive change improves the internal quality of the system — its maintainability, performance, security posture, or testability — without altering its external behaviour. Refactoring, dependency updates, performance optimisation, and security hardening that does not change specified behaviour are all preventive changes.

In AI-integrated development, preventive changes are particularly important because AI-generated code has documented tendencies toward higher cyclomatic complexity and lower modularity than human-written code (Sonar, 2025; ScienceDirect, 2026). Periodic preventive maintenance to address these structural issues is recommended as a planned activity, not a reactive response.

Preventive changes present a subtle but important traceability challenge: because they do not alter specified behaviour, they may not require SRS updates. However, they may require SDD updates (when the internal design changes) and always require test re-execution to verify that behaviour has not inadvertently changed. The TM status must be updated to reflect re-verification.

**Urgency:** Low; should be scheduled as a planned activity rather than a reactive one.

**Specification hierarchy impact:** Typically SDD and test verification only; SRS unchanged.

---

## 4. The Specification Hierarchy and Change Propagation

### 4.1 The Consistency Dependency Chain

The specification hierarchy defined in Tulloch (2025) is a directed dependency chain: the SRS is consistent with the PSD; the SDD is consistent with the SRS; the TM maps SRS to SDD and test cases; the test suite implements the TM test case specifications; and the codebase is consistent with the SDD interfaces and satisfies the test suite. This chain can be represented as:

```
PSD → SRS → SDD → TM → Test Suite → Codebase
```

A requirements change introduced at any point in this chain propagates consequences downstream. Critically, a change also has *upstream implications*: if a change cannot be derived from or reconciled with the PSD, then the PSD must also be updated. The direction and extent of propagation depends on where the change originates and what change type it represents.

### 4.2 Propagation Patterns by Change Origin

**PSD-originating changes** (new objectives, revised stakeholder constraints, updated out-of-scope boundaries) propagate through the entire chain. All five downstream documents may require updates. This is the highest-cost change pattern and should trigger a formal change control review before any work begins.

**SRS-originating changes** (new requirements, revised acceptance criteria, deprecated requirements) propagate from the SRS downward through the SDD, TM, test suite, and codebase. The PSD should be reviewed to confirm the change is consistent with the stated objectives; if it is not, a PSD update is required first.

**SDD-originating changes** (architectural revisions, component interface changes, design pattern updates not driven by new requirements) propagate to the TM, test suite, and codebase. The SRS should be reviewed to confirm no requirement is violated.

**Test-originating changes** (revised test cases, added edge-case coverage) propagate to the TM and may require implementation changes. Specification documents are typically unaffected unless the test revision reveals a specification gap.

**Code-originating changes** (hotfixes, performance patches, dependency updates) that alter specified behaviour must be propagated *upstream* — the relevant SRS requirements and SDD design elements must be updated. Code changes that do not alter specified behaviour (preventive maintenance) require only TM re-verification.

### 4.3 The Orphaning Risk

A critical property of the specification hierarchy in AI-integrated development is that any change that is implemented in the codebase without a corresponding update to the upstream specification creates an *orphaned implementation*: code that has no traceable requirement. A small change can trigger high evolution because of the ripple effect identified during impact analysis. This depends on traceability information, which is the connection between software development artifacts. Orphaned implementations progressively degrade the specification hierarchy's integrity and, more practically, undermine the team's ability to use AI generation for future work — an AI generating code against a stale specification will produce output inconsistent with the actual system state.

The TM is the primary detection mechanism for orphaned implementations. Any code component that cannot be traced to a current TM entry should be treated as a change management failure requiring remediation, not a normal state of the codebase.

---

## 5. Stage 1 — Change Identification and Documentation

### 5.1 Change Sources

Requirements changes in deployed systems originate from multiple sources, each with different characteristics and urgency profiles:

- **User feedback and defect reports:** Typically corrective changes; high urgency; often discovered through support channels, monitoring systems, or user acceptance testing
- **Regulatory and compliance updates:** Adaptive changes; urgency determined by compliance deadlines; often discovered through regulatory monitoring
- **Stakeholder evolution:** Perfective changes; medium urgency; originate in product management, governance, or executive direction
- **Technical debt and quality observations:** Preventive changes; low urgency; identified through code quality analysis, security scanning, or architectural review
- **Integration partner changes:** Adaptive changes; urgency determined by partner timelines; discovered through API change notifications or integration monitoring
- **Implementation-driven discovery:** As described in Tulloch (2025, §4.5), requirements that only become articulable through interaction with the working system; may be corrective or perfective depending on whether the gap represents a defect or an unmet need

### 5.2 The Change Request Form

Every proposed requirement change, regardless of origin or apparent size, must be documented in a Change Request Form (CRF) before any analysis, authorisation, or implementation work begins. The CRF is the formal entry point to the change management process and serves as the permanent record of the change's origin and initial characterisation.

A complete CRF contains:

- **CRF Identifier (CRF-XXX):** Unique identifier, assigned sequentially
- **Date Submitted and Submitter:** Provenance of the request
- **Change Type:** Corrective / Adaptive / Perfective / Preventive (from Section 3)
- **Change Summary:** A concise description of the proposed change in plain language, written from the perspective of the desired outcome, not the suspected implementation
- **Originating Evidence:** The defect report, regulatory reference, stakeholder directive, or technical observation that motivates the change
- **Affected System Areas (preliminary):** The submitter's initial estimate of which system areas are affected — this is a preliminary assessment, not an impact analysis
- **Urgency Classification:** Critical (system unavailable or compliance breach imminent) / High (significant user impact or regulatory deadline within 30 days) / Medium (moderate impact, no immediate deadline) / Low (quality improvement, no operational impact)
- **Proposed Disposition:** Accept and implement / Accept and defer / Reject with rationale / Refer for further investigation

The CRF must be submitted and assigned an identifier before any informal discussion of implementation approaches begins. This requirement prevents the common anti-pattern of "shadow changes" — implementation work that begins before formal documentation and results in code changes that are never properly traced to requirements.

### 5.3 Change Request Triage

Upon receipt, each CRF undergoes a triage step that confirms the change type classification, validates the urgency rating, and assigns the request to the appropriate review path. Critical and High urgency changes are escalated immediately to a named change authority (see Section 9). Medium and Low urgency changes are batched for regular change review cycles.

Triage also determines whether the change is *in scope* for the current system baseline. Proposed changes that represent significant new capabilities not derivable from the PSD's stated objectives may be better handled as new projects with a fresh PSD rather than as changes to the existing one. This determination protects the integrity of the current project's specification hierarchy by preventing scope creep from being absorbed through the change management process rather than through proper project governance.

---

## 6. Stage 2 — Change Impact Analysis

### 6.1 Purpose and Scope

Change impact analysis (CIA) is the systematic determination of which artifacts in the specification hierarchy must be updated to implement a proposed change, and what the cost and risk of those updates are. The purpose of CIA is not to approve or reject changes — that is the function of the Change Control Board described in Section 9 — but to provide the information needed to make that decision with full awareness of consequences.

Impact analysis requires identifying all the files, models, and documents that might have to be modified if the team incorporates the requested change, as well as the tasks required to implement the change and an estimate of the effort needed to complete those tasks. Traceability data that links the affected requirement to downstream deliverables helps greatly with this analysis.

### 6.2 The Traceability Matrix as the Primary CIA Instrument

The TM defined in Tulloch (2025, §5.3) is the primary instrument for systematic change impact analysis. For each proposed change, the CIA analyst works through the TM in the following sequence:

**Step 1 — Identify directly affected requirements.** For the proposed change, identify all SRS requirements (FR-XXX, NFR-XXX, IR-XXX, DR-XXX, CR-XXX) that are directly modified, deprecated, or added by the change.

**Step 2 — Identify affected design elements.** For each directly affected requirement, identify all SDD design elements (DE-XXX) linked in the TM. These are the components whose implementation will require revision.

**Step 3 — Identify affected test cases.** For each directly affected requirement and each affected design element, identify all linked test cases (TC-XXX). These tests will require revision, re-execution, or both.

**Step 4 — Identify secondary effects.** Examine the SDD interface specifications for all identified design elements. Components that consume the interfaces of affected design elements are candidates for secondary impact — they may not require code changes, but their test cases must be re-executed to verify that the interface changes have not broken their behaviour.

**Step 5 — Identify documentation impacts.** Identify which sections of the API documentation, deployment guide, operations runbook, and user documentation reference the affected areas. These documents will require updates.

**Step 6 — Assess PSD consistency.** Determine whether the proposed change is consistent with the PSD's stated objectives, in-scope features, and out-of-scope exclusions. If it is not, the PSD must be updated, which triggers a broader specification review.

### 6.3 The Impact Analysis Report

The output of Stage 2 is a structured Impact Analysis Report (IAR) that documents the findings of Steps 1-6. The IAR contains:

- **CRF Reference:** The change request this analysis addresses
- **Requirements Impact:** List of SRS requirement identifiers to be added, modified, or deprecated
- **Design Impact:** List of SDD design element identifiers to be updated
- **Test Impact:** List of test cases to be revised and test cases to be re-executed without revision
- **Documentation Impact:** List of documentation sections requiring updates
- **PSD Consistency Assessment:** Confirmed consistent / Requires PSD update (with description of required change)
- **Estimated Effort:** An effort estimate for each impacted artifact category
- **Risk Assessment:** Identification of high-risk propagation paths, particularly secondary effects on components not directly modified
- **Recommended Implementation Sequence:** The order in which artifact updates should be made, following the dependency structure of the specification hierarchy

The IAR is submitted to the Change Control Board together with the CRF as the basis for change authorisation.

### 6.4 AI-Assisted Impact Analysis

As noted in Section 2.4, emerging research supports the use of LLMs to assist with requirements change impact analysis. The AI can be instructed to analyse the TM against the proposed change, identify potentially affected requirements and design elements, and flag secondary effects that a human analyst might miss. This AI-assisted analysis serves the same triage function described in Tulloch (2025, §11.1.2): it reduces human analytical effort by performing a first-pass scan, but does not substitute for human expert review of the IAR before it is submitted for authorisation.

The AI impact analysis prompt should provide the full TM, the SRS requirements in the affected area, the relevant SDD interface specifications, and a precise description of the proposed change. The output should be explicitly framed as a preliminary identification requiring human validation.

---

## 7. Stage 3 — Change Implementation

### 7.1 Implementation Sequencing

Authorised changes are implemented following the dependency order of the specification hierarchy: from the top of the chain downward. This sequencing principle is not merely procedural — it is the mechanism that prevents the specification and code from diverging during the change process itself.

The correct sequence for a change affecting the full specification hierarchy is:

1. Update the PSD (if required)
2. Update the affected SRS requirements
3. Update the affected SDD design elements and interface specifications
4. Update the TM to reflect new or modified requirement-design-test linkages, marking affected rows as "In Progress"
5. Update or add test cases
6. Generate updated or new code components using the updated SDD as context
7. Execute the updated test suite
8. Update documentation
9. Update the TM status to "Verified" for all affected rows
10. Record the complete change in the Change Log

Implementing steps out of this order — particularly generating code before updating the SRS and SDD — is the most common source of specification drift in post-deployment change management, and must be enforced as a process constraint.

### 7.2 AI-Assisted Specification Updates

The AI generation capabilities described in Tulloch (2025) apply equally to specification updates as to initial generation. For each specification document that requires updating, the team should provide the AI with the current version of the document, the CRF, the IAR, and explicit instructions about which sections require revision. The AI should be instructed to produce targeted updates rather than regenerating entire documents — regeneration risks overwriting portions of the specification that are correct and stable.

The prompt structure for specification updates follows a consistent four-part pattern analogous to the code generation prompt structure: context (what document is being updated and why), specification (the CRF and IAR findings), constraints (what must not change), and instruction (the specific update requested).

### 7.3 AI-Assisted Code Generation for Changes

Code generation for authorised changes follows the same component-by-component approach described in Tulloch (2025, §8.1), with one additional constraint: the generation prompt must explicitly reference both the *new* specification state and the *existing* code components that the changed component must integrate with. This dual-context requirement is more demanding than initial generation because the AI must produce code that is correct with respect to the new specification while remaining compatible with the unchanged portions of the codebase.

Where a change affects an interface shared by multiple components, the interface specification update must be completed and reviewed before any dependent component code is generated. Generating interface-consuming code against an in-progress interface specification is a common source of integration failures in change implementations.

### 7.4 Regression Scope

Every change implementation must be accompanied by a defined regression scope: the set of test cases, beyond those directly associated with the changed requirements, that must be executed to verify that the change has not introduced unintended side effects. The regression scope is derived from the secondary effects identified in the IAR (Section 6.2, Step 4) and should include:

- All test cases for requirements directly affected by the change
- All test cases for requirements whose implementing design elements share interfaces with changed design elements
- A representative sample of integration tests for subsystems that interact with changed components
- The full suite of non-functional requirement tests (performance, security, accessibility) where the change could plausibly affect system-level behaviour

---

## 8. Stage 4 — Verification and Deployment

### 8.1 Change Verification

Change verification confirms that the implemented change satisfies its stated intent, does not violate any unchanged requirements, and has not introduced regressions in the system. Verification is a human-led activity; AI-assisted test execution and static analysis provide supporting evidence, but the verification decision is made by a qualified human reviewer.

Verification proceeds in three steps. First, *requirements verification* confirms that each modified or added SRS requirement has a corresponding passing test case and a correct TM entry. Second, *regression verification* confirms that all test cases in the defined regression scope pass. Third, *documentation verification* confirms that all identified documentation updates have been completed and are consistent with the implemented change.

A change that fails verification at any step is not deployed. It returns to Stage 3 with a documented description of the verification failure, which is treated as a new defect to be resolved within the scope of the current change.

### 8.2 The Deployment Decision

Deployment authorisation is distinct from change authorisation. Change authorisation (from the Change Control Board, Section 9) approves the change for implementation. Deployment authorisation approves the verified change for release to the production environment. These are separate decisions because the risks associated with production deployment — including timing, operational continuity, user communication, and rollback planning — are different from the risks of implementation.

The deployment decision should consider: the urgency of the change (a Critical corrective change warrants immediate deployment; a Low preventive change may be batched with other low-urgency changes into a scheduled release); the operational impact of the deployment (does it require downtime, user notification, or database migration?); the rollback plan if the deployment produces unexpected results; and the communication plan for affected users.

### 8.3 Deployment Types and Their Specification Implications

Different deployment types have different implications for the specification hierarchy.

**Hotfix deployment** addresses a Critical or High urgency corrective change. The deployment window is compressed; thorough regression testing may not be feasible before deployment. In this case, the team must document the reduced regression scope in the Change Log and schedule a full regression cycle for the earliest subsequent deployment. Specification documents are updated before the hotfix is deployed; there is no acceptable hotfix process in which code is deployed against an outdated specification.

**Scheduled release deployment** bundles multiple authorised, verified changes into a single release. Each change must be verified independently before release bundling. The TM must be updated to reflect the combined effect of all changes in the release before the release is deployed.

**Database migration deployment** accompanies changes that modify the data architecture. These deployments carry additional risk because data schema changes are frequently irreversible. The SDD data architecture section must be updated and reviewed before migration scripts are generated, and the migration must be tested against a production-equivalent data sample before live deployment.

### 8.4 Post-Deployment Monitoring

Every deployment should be accompanied by a defined monitoring period during which operational metrics are observed for anomalies attributable to the change. The duration and intensity of this monitoring period should be proportional to the complexity and risk profile of the change. Anomalies observed during the monitoring period are treated as new corrective change requests and enter Stage 1 of the RCM process.

---

## 9. The Change Control Board

### 9.1 Purpose and Composition

The Change Control Board (CCB) is the governance body responsible for authorising or rejecting proposed changes on the basis of the CRF and IAR. In small teams, the CCB may consist of a single named individual with designated authority. In larger teams or organisations with compliance obligations, the CCB should include a technical representative (who can assess feasibility and impact), a business representative (who can assess value and priority), and a quality assurance representative (who can assess risk and regression implications).

The CCB does not design solutions. Its role is to evaluate whether a proposed change should proceed, whether the proposed scope of implementation is appropriate, and whether the urgency classification is correct. Detailed implementation decisions are made by the engineering team in Stage 3.

### 9.2 CCB Decisions

The CCB may make four types of decisions in response to a submitted CRF and IAR:

**Approve for immediate implementation:** The change is authorised and enters Stage 3 without delay. Appropriate for Critical and High urgency changes.

**Approve for scheduled implementation:** The change is authorised but deferred to a scheduled release cycle. Appropriate for Medium and Low urgency changes.

**Reject:** The proposed change is not approved, with documented rationale. The CRF is archived; no implementation work proceeds. Rejection is appropriate when the proposed change conflicts with stated PSD objectives, when the impact analysis reveals unacceptable risk, or when the proposed change is outside the scope of the current system baseline.

**Return for further analysis:** The CRF and IAR are returned to the submitter for additional information or revised impact analysis. Appropriate when the proposed change is incompletely described or when the IAR is incomplete.

### 9.3 Emergency Change Process

Critical urgency changes — those addressing active system failures, security breaches, or immediate compliance violations — may bypass the standard CCB review cycle under an emergency change process. The emergency process permits Stage 3 implementation to begin before formal CCB review, subject to the following constraints: a named individual with CCB authority must verbally or electronically authorise the emergency change; the CRF must be submitted within one hour of work beginning; and a retrospective CCB review must be completed within one business day of the change's deployment.

Emergency changes carry elevated risk of specification drift because the compressed timeline creates pressure to skip specification updates. This pressure must be explicitly resisted: the specification documents must be updated as part of the emergency implementation, not deferred to a subsequent cycle. A specification that is out of sync with the deployed system is a defect in its own right.

---

## 10. AI Assistance in the Change Management Process

### 10.1 Appropriate Applications

AI assistance is applicable and beneficial at several points in the four-stage RCM process:

**Change Request Form completion assistance:** The AI can help submitters write clear, complete CRFs by prompting for missing information (originating evidence, urgency classification, affected system areas) when a draft CRF is submitted.

**Impact analysis pre-screening:** As described in Section 6.4, the AI can perform a preliminary pass over the TM to identify potentially affected requirements and design elements, reducing the analytical burden on human reviewers.

**Specification update generation:** The AI can generate proposed updates to SRS requirements, SDD sections, and TM entries based on the CRF, IAR, and current specification versions, subject to human review before acceptance.

**Code generation for authorised changes:** The AI generates updated or new code components using the updated specification as context, following the same prompt structure as initial generation.

**Test case update generation:** The AI can generate revised or new test cases for modified requirements, subject to human review against the acceptance criteria in the updated SRS.

**Documentation update generation:** The AI can generate draft updates to API documentation, deployment guides, and user documentation based on the specification changes, subject to human editorial review.

### 10.2 Boundaries on AI Authority

Consistent with the verification limitations identified in Tulloch (2025, §11.1.2) and the findings of Endres et al. (2025), AI assistance in the RCM process must be bounded by clear human authority constraints:

- **AI must not authorise changes.** Change authorisation is a human governance decision that requires business context, risk judgement, and accountability that AI systems cannot provide.
- **AI-generated impact analyses are preliminary assessments, not authoritative IAR conclusions.** All AI-generated impact assessments require human expert review before submission to the CCB.
- **AI must not approve specification updates.** Proposed specification updates generated by AI are drafts; a qualified human reviewer must approve each update before it is incorporated into the authoritative specification.
- **AI verification of specification compliance remains unreliable.** As documented by Endres et al. (2025), LLMs have systematic difficulty verifying whether code satisfies natural language specifications. Verification decisions remain human responsibilities.

### 10.3 The Prompt Management Consideration

The prompts used for AI assistance in the change management process are engineering artifacts subject to the same version control and documentation requirements as the specification documents themselves. As the change management process matures, prompt templates for CRF assistance, impact analysis, and specification update generation should be refined, versioned, and stored alongside the project's other prompt infrastructure as described in Tulloch (2025, §12.2).

---

## 11. Change Management in Lightweight Workflow Variants

As discussed in Tulloch (2025, §3), the full specification-driven workflow is most appropriate for complex, compliance-oriented, or long-lifecycle projects. Smaller projects or those in more volatile domains may operate with a lightweight specification hierarchy — a shorter PSD, a combined requirements-and-design document, and a simplified TM. The change management process should be scaled accordingly.

For lightweight workflow variants, a simplified RCM process retains the essential elements — change documentation, impact assessment, implementation sequencing, and verification — while reducing the overhead of formal CCB governance and multi-document impact analysis:

- The CRF is simplified to a short structured form (change description, type, urgency, and affected areas)
- Impact analysis is conducted informally against the simplified specification documents, documented in a paragraph rather than a full IAR
- Change authorisation is granted by a single named individual rather than a board
- The Change Log entry is the primary formal record of each change, capturing the change description, rationale, affected artifacts, and verification outcome

The one element that should not be simplified regardless of project scale is the requirement to update specification documents before implementing code changes. Even on solo projects with minimal documentation, a brief note in the Change Log recording what changed, why, and what was updated is sufficient to prevent the specification drift that otherwise accumulates rapidly in AI-assisted development.

---

## 12. Discussion

### 12.1 The Relationship Between Change Management and Workflow Integrity

The change management process described in this paper is not a separate workflow bolted onto the AI-integrated development framework of Tulloch (2025). It is the mechanism by which that framework's core quality property — specification-code consistency — is preserved over the operational lifetime of the system. A development team that maintains rigorous specification discipline during initial development but abandons it when handling post-deployment changes will find that the specification hierarchy rapidly becomes a historical artifact rather than a living engineering resource. The investment in initial specification quality is only recovered if the specification remains authoritative throughout the system's lifecycle.

This observation has a direct implication for project planning. Change management process design should not be deferred to after deployment. The CCB structure, the CRF and IAR templates, the Change Log format, and the AI-assisted analysis prompts should all be defined during Phase 1 of the development workflow, before any code is generated. A project that reaches deployment without a defined change management process will respond to its first requirement change with improvised, undocumented practices that become the de facto process going forward.

### 12.2 The Compounding Value of Traceability

The change management process described in this paper depends critically on the Traceability Matrix being maintained with fidelity throughout the system's lifecycle. A change has not only impact on the source code, but also on other related software artefacts such as requirements, design, and test, and impact analysis can be efficiently supported through traceability information. A TM that is outdated, incomplete, or inconsistent degrades the reliability of impact analysis, increases the risk of orphaned implementations, and reduces the team's ability to use AI generation productively.

Teams should treat TM maintenance as an operational discipline with the same standing as codebase maintenance. A monthly or per-release TM reconciliation — verifying that every implementation can be traced to a current requirement and every current requirement is traced to verified code — is a low-cost investment that compounds in value over the system's lifetime as the number of changes accumulates.

### 12.3 Limitations and Future Directions

The process framework proposed in this paper, like the development workflow it extends, has not been empirically validated through controlled study. The stage structure, the CRF and IAR artifact designs, the CCB governance model, and the AI assistance boundaries are grounded in established requirements change management literature and the architectural logic of the specification-driven workflow, but their comparative effectiveness against alternative approaches has not been measured.

Future work should develop empirical measures for change management process effectiveness in AI-integrated development contexts — specifically, metrics for specification drift rate, change-induced defect density, and the proportion of post-deployment defects attributable to inadequate impact analysis. The application of LLM-assisted impact analysis tools, such as those described by the emerging 2025 literature, deserves systematic evaluation in practice rather than theoretical endorsement.

---

## 13. Conclusion

Requirements change after code generation is not an edge case in the lifecycle of an AI-integrated software system — it is the dominant activity from the point of initial deployment onward. The specification-driven workflow provides a strong foundation for managing change systematically, precisely because its specification hierarchy provides the traceability infrastructure that change impact analysis requires. But that infrastructure must be actively maintained through a disciplined change management process, or its value erodes with each undocumented modification.

The four-stage RCM process proposed in this paper — change documentation, impact analysis, implementation, and deployment — is designed to preserve the specification-code consistency that is the central quality assurance property of AI-integrated development. It treats the Traceability Matrix as the primary impact analysis instrument, the Change Log as the institutional record of change rationale, and the specification hierarchy as the authoritative source of truth that must be updated before code before any production change is deployed.

The most important practical insight from this framework is that change management discipline is not a process overhead imposed on a working system — it is the mechanism by which the system continues to work correctly, and continues to be improvable by AI, over the course of its operational lifetime. A specification hierarchy that drifts from the deployed system is worse than no specification at all: it creates a false sense of documented understanding while actively misleading future developers and AI generation sessions about the actual state of the system.

---

## 14. References

Bühne, S., & Herrmann, A. (2022). *Requirements change management process.* International Requirements Engineering Board (IREB).

Chapin, N., Hale, J. E., Khan, K. M., Ramil, J. F., & Tan, W.-G. (2001). Types of software evolution and software maintenance. *Journal of Software Maintenance: Research and Practice, 13*(1), 3–30.

Chikofsky, E. J., & Cross, J. H. (1990). Reverse engineering and design recovery: A taxonomy. *IEEE Software, 7*(1), 13–17.

Endres, M., Chong, K., Bhatt, N., & Abdelfattah, A. S. (2025). Uncovering systematic failures of LLMs in verifying code against natural language specifications. *arXiv:2502.11513*.

IEEE Computer Society. (2006). *ISO/IEC 14764: Software engineering — Software life cycle processes — Maintenance.* IEEE.

Inayat, I., Salim, S. S., Marczak, S., Daneva, M., & Shamshirband, S. (2015). A systematic literature review on agile requirements engineering practices and challenges. *Computers in Human Behavior, 51*, 915–929.

ISO/IEC/IEEE. (2018). *Systems and software engineering — Life cycle processes — Requirements engineering* (ISO/IEC/IEEE 29148:2018). ISO.

Jayatilleke, S., & Lai, R. (2018). A systematic review of requirements change management. *Information and Software Technology, 93*, 163–185.

Jha, N., & Babajide Mustapha, B. (2025). LLM-driven cost-effective requirements change impact analysis. *arXiv:2511.00262*.

Lientz, B. P., & Swanson, E. B. (1980). *Software maintenance management: A study of the maintenance of computer application software in 487 data processing organizations.* Addison-Wesley.

Mohan, K., Xu, P., Cao, L., & Ramesh, B. (2008). Improving change management in software development: Integrating traceability and software configuration management. *Decision Support Systems, 45*(4), 922–936.

Nuseibeh, B., & Easterbrook, S. (2000). Requirements engineering: A roadmap. *Proceedings of the Conference on the Future of Software Engineering (ICSE 2000)*, 35–46.

Paetsch, F., Eberlein, A., & Maurer, F. (2003). Requirements engineering and agile software development. *Proceedings of the 12th IEEE International Workshops on Enabling Technologies*, 308–313.

Rolland, C., Salinesi, C., & Etien, A. (2004). Eliciting gaps in requirements change. *Requirements Engineering, 9*(1), 1–15.

Schmidt, D. C. (2006). Model-driven engineering. *Computer, 39*(2), 25–31.

ScienceDirect. (2026). Quality assurance of LLM-generated code: Addressing non-functional quality characteristics. *Journal of Systems and Software*.

Sonar. (2025). *The inevitable rise of poor code quality in AI-accelerated codebases.* SonarSource.

Torchiano, M., Tomassetti, F., Ricca, F., Tiso, A., & Reggio, G. (2012). Benefits from modelling and MDD adoption. *Proceedings of the Second Edition of the International Workshop on Experiences and Empirical Studies in Software Modelling*.

Tulloch, G. (2025). AI-integrated software development: A specification-driven framework for AI-assisted code generation. Sunrise School Division.

Zowghi, D., & Nurmuliani, N. (2002). A study of the impact of requirements volatility on software project performance. *Proceedings of the 9th Asia-Pacific Software Engineering Conference (APSEC 2002)*, 3–11.

---

## Appendix B — Change Management Templates and Prompt Structures

### B.1 Change Request Form Template

```
# Change Request Form
CRF Identifier: CRF-XXX
Date Submitted: [YYYY-MM-DD]
Submitted By: [Name / Role]

## Change Summary
[1–3 sentences describing the proposed change in plain language,
written from the perspective of the desired outcome.]

## Change Type
[ ] Corrective — addresses a defect in specified or actual behaviour
[ ] Adaptive  — responds to a change in the external environment
[ ] Perfective — introduces new or improved capabilities
[ ] Preventive — improves internal quality without changing behaviour

## Originating Evidence
[Reference to defect report, regulatory document, stakeholder directive,
or technical observation that motivates this change. Attach if available.]

## Affected System Areas (Preliminary)
[The submitter's initial estimate — not an impact analysis.
List known affected features, components, or requirements by name/ID.]

## Urgency
[ ] Critical — system unavailable or compliance breach imminent
[ ] High    — significant user impact or deadline within 30 days
[ ] Medium  — moderate impact, no immediate operational deadline
[ ] Low     — quality improvement, no operational impact

## Proposed Disposition
[ ] Accept and implement immediately
[ ] Accept and defer to scheduled release
[ ] Reject (provide rationale below)
[ ] Return for further analysis

## Rationale (if Reject or Return)
[Required if Reject or Return is selected above.]
```

---

### B.2 Impact Analysis Report Template

```
# Impact Analysis Report
IAR Identifier: IAR-XXX
CRF Reference: CRF-XXX
Date Completed: [YYYY-MM-DD]
Analyst: [Name]

## Requirements Impact
| Requirement ID | Action Required     | Description of Change        |
|----------------|---------------------|------------------------------|
| FR-XXX         | Modify / Add / Dep. | [Brief description]          |

## Design Impact
| Design Element | Action Required     | Description of Change        |
|----------------|---------------------|------------------------------|
| DE-XXX         | Modify / Add        | [Brief description]          |

## Test Impact
| Test Case ID | Action Required          | Reason                    |
|--------------|--------------------------|---------------------------|
| TC-XXX       | Revise / Re-execute only | [Brief description]       |

## Documentation Impact
| Document         | Section    | Action Required             |
|------------------|------------|-----------------------------|
| API Docs         | [Section]  | Update / Add                |
| Deployment Guide | [Section]  | Update                      |

## PSD Consistency Assessment
[ ] Confirmed consistent with current PSD
[ ] Requires PSD update — description: [...]

## Effort Estimate
| Artifact Category    | Estimated Effort |
|----------------------|-----------------|
| Specification updates | [X hours/days]  |
| Test updates          | [X hours/days]  |
| Code changes          | [X hours/days]  |
| Documentation updates | [X hours/days]  |
| **Total**             | **[X hours]**   |

## Risk Assessment
[Identify high-risk propagation paths, secondary effects,
or interface changes that may affect multiple consumers.]

## Recommended Implementation Sequence
1. [First artifact to update]
2. [Second artifact to update]
...
```

---

### B.3 Change Log Entry Template

```
# Change Log Entry
CL Identifier: CL-XXX
Date: [YYYY-MM-DD]
CRF Reference: CRF-XXX
Authorised By: [Name / Role]
Implemented By: [Name]
Deployed: [YYYY-MM-DD] / Pending

## Change Summary
[Brief description of what changed.]

## Change Type
[Corrective / Adaptive / Perfective / Preventive]

## Rationale
[Why this change was made — business or technical justification.]

## Artifacts Updated
- PSD: [Version / Sections / No change]
- SRS: [Requirements added/modified/deprecated — list identifiers]
- SDD: [Design elements added/modified — list identifiers]
- TM: [Rows added/modified — list requirement IDs]
- Test Suite: [Test cases added/revised/re-executed]
- Code: [Components modified]
- Documentation: [Sections updated]

## Verification Summary
[Pass / Fail — brief description of verification outcome.
If fail, reference the remediation CRF.]

## Notes
[Any exceptions, deferred items, technical debt introduced,
or observations for future reference.]
```

---

### B.4 AI-Assisted Impact Analysis Prompt Template

```
You are a senior software quality assurance engineer specialising in
requirements change impact analysis.

The following materials are provided:
1. The current Traceability Matrix [attached]
2. The current SRS requirements for the affected area [attached]
3. The current SDD interface specifications for potentially affected
   components [attached]
4. The Change Request Form for the proposed change [attached]

Your task:
1. Identify all SRS requirements (FR-XXX, NFR-XXX, IR-XXX, DR-XXX, CR-XXX)
   that are directly affected by the proposed change. For each, state
   whether it must be modified, deprecated, or whether a new requirement
   must be added.

2. For each directly affected requirement, identify the SDD design
   elements (DE-XXX) linked in the TM that will require implementation
   changes.

3. For each affected design element, identify components in the SDD that
   consume its interfaces and may be subject to secondary effects.

4. Identify all test cases (TC-XXX) that must be revised and all test
   cases that must be re-executed without revision.

5. Identify sections of API documentation, deployment guide, and user
   documentation that reference the affected areas.

6. Assess whether the proposed change is consistent with the PSD's stated
   objectives and in-scope features. If not, identify what PSD update
   is required.

Output your findings as a structured preliminary Impact Analysis Report
using the IAR template format.

IMPORTANT: This output is a preliminary assessment for human review.
Flag any findings where you are uncertain and recommend human expert
verification of those specific items.
```

---

### B.5 AI-Assisted Specification Update Prompt Template

```
You are a senior requirements engineer.

The following materials are provided:
1. The current [SRS / SDD / TM] — the document to be updated [attached]
2. The authorised Change Request Form [CRF-XXX, attached]
3. The approved Impact Analysis Report [IAR-XXX, attached]
4. The current PSD for context [attached]

Your task:
Generate targeted updates to the [SRS / SDD / TM] to implement the
authorised change described in CRF-XXX.

Constraints:
- Modify ONLY the sections and requirements identified in IAR-XXX.
- Do not alter any requirement, design element, or TM entry outside
  the scope defined in the IAR.
- Preserve all existing requirement identifiers for modified requirements;
  do not renumber or reassign identifiers.
- Assign new identifiers to any new requirements or design elements,
  continuing from the highest existing identifier in each sequence.
- For deprecated requirements, mark them as [DEPRECATED — CL-XXX] rather
  than deleting them.
- Flag any case where the proposed update creates a conflict with an
  existing requirement not in scope of this change.

Output the updated sections in full, clearly marking each changed
element with [MODIFIED], [ADDED], or [DEPRECATED] for human reviewer
identification.
```

---

*© 2025 Gordon Tulloch — Sunrise School Division. This paper may be reproduced for educational and non-commercial purposes with attribution.*
