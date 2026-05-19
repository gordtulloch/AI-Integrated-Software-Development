# AI-Integrated Software Development: A Specification-Driven Framework for AI-Assisted Code Generation

**Gordon Tulloch**
Director of Information & Communications Technologies
Sunrise School Division

---

*Abstract* — The emergence of large language model (LLM)-based code generation tools presents both a significant opportunity and a methodological challenge for software development teams. While these tools are capable of producing syntactically correct and functionally plausible code at remarkable speed, their output quality is tightly bounded by the precision and completeness of the instructions they receive. This paper proposes a structured, document-driven workflow for AI-integrated software development that systematizes the use of AI code generation within a framework grounded in established software engineering principles. The workflow proceeds through six ordered phases: scope definition, specification generation, iterative refinement, test planning, code generation, and documentation and delivery. At each phase, a defined set of artifacts is produced, reviewed against formal quality criteria, and used as context for subsequent AI interactions. The paper describes each artifact in detail, provides rationale for its inclusion, and identifies common failure modes that arise when the artifact is absent or inadequate. The resulting framework is intended to be practical and accessible to development teams of varying sizes and experience levels who wish to adopt AI-assisted development without sacrificing correctness, maintainability, or auditability.

**Keywords:** artificial intelligence, software engineering, code generation, requirements engineering, software specification, large language models, traceability, test-driven development

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Background and Related Work](#2-background-and-related-work)
3. [Phase 1 — The Project Scope Document](#3-phase-1--the-project-scope-document)
4. [Phase 2 — AI-Generated Specification Documents](#4-phase-2--ai-generated-specification-documents)
   - 4.1 [The Software Requirements Specification](#41-the-software-requirements-specification)
   - 4.2 [The Software Design Description](#42-the-software-design-description)
   - 4.3 [The Traceability Matrix](#43-the-traceability-matrix)
5. [Phase 3 — Iterative Refinement](#5-phase-3--iterative-refinement)
6. [Phase 4 — Test Planning](#6-phase-4--test-planning)
7. [Phase 5 — Code Generation](#7-phase-5--code-generation)
8. [Phase 6 — Documentation and Delivery](#8-phase-6--documentation-and-delivery)
9. [Change Management and Version Control](#9-change-management-and-version-control)
10. [Best Practices and Common Pitfalls](#10-best-practices-and-common-pitfalls)
11. [Tools and Technology Considerations](#11-tools-and-technology-considerations)
12. [Discussion](#12-discussion)
13. [Conclusion](#13-conclusion)
14. [References](#14-references)
15. [Appendix A — Document Templates and Prompt Structures](#appendix-a--document-templates-and-prompt-structures)

---

## 1. Introduction

The rapid advancement of large language models (LLMs) has produced a new class of software engineering tool: the AI code generator. Systems such as those built on transformer-based architectures trained on large corpora of public source code can now produce working application code, unit tests, database schemas, and API definitions from natural language descriptions. This capability has attracted substantial interest from both industry practitioners and academic researchers, with early evidence suggesting meaningful productivity gains in certain well-defined coding tasks (Chen et al., 2021; Ziegler et al., 2022).

However, the practical deployment of AI code generation in production software projects has revealed a persistent and underappreciated problem. The quality, correctness, and maintainability of AI-generated code are highly sensitive to the quality of the instructions provided. Vague, incomplete, or internally inconsistent specifications produce code that may compile and appear functional in isolation while failing at the system level, violating unstated requirements, or encoding subtle architectural decisions that are inconsistent across separately generated components. This phenomenon — which might be termed *specification-sensitivity* — means that the discipline of requirements and design specification is more important in AI-assisted development than in traditional development, not less.

This paper addresses the specification-sensitivity problem by proposing a comprehensive, phased workflow for AI-integrated software development. The workflow is grounded in established software engineering standards, particularly the IEEE standards for requirements specifications (IEEE Std 830-1998) and software design descriptions (IEEE Std 1016-2009), while adapting those standards to the specific demands of AI-mediated development. The central argument is that AI code generation tools function as force multipliers: they amplify both the precision of well-formed specifications and the imprecision of poorly formed ones. A disciplined specification-first approach is therefore not merely good practice — it is the primary mechanism by which AI-assisted development teams can reliably produce correct and maintainable software.

The paper makes the following contributions:

1. A six-phase workflow for AI-integrated software development that systematizes the use of AI generation tools within a document-driven engineering process.
2. A detailed description of each workflow artifact — its purpose, structure, and quality criteria — with emphasis on artifacts that are frequently omitted or underspecified in practice.
3. An analysis of common failure modes in AI-assisted development workflows, with remediation guidance for each.
4. Practical prompt templates for using AI to generate specification documents from upstream inputs.

The remainder of the paper is organized as follows. Section 2 reviews relevant background literature. Sections 3 through 8 describe each phase of the workflow in detail. Section 9 addresses change management. Section 10 discusses best practices and pitfalls. Section 11 reviews tooling considerations. Section 12 offers a broader discussion of implications, and Section 13 concludes. Appendix A provides document templates and prompt structures.

---

## 2. Background and Related Work

### 2.1 AI-Assisted Code Generation

The application of machine learning to source code has a substantial research history, including early work on statistical language models for code completion (Hindle et al., 2012) and the subsequent development of neural program synthesis systems (Balog et al., 2017). The introduction of large-scale transformer models pretrained on source code, exemplified by systems such as Codex (Chen et al., 2021), GitHub Copilot, and subsequent general-purpose LLMs with strong coding capabilities, represented a qualitative advance in the practicality and generality of AI code generation.

Empirical studies of these systems have reported significant productivity improvements in controlled settings. Peng et al. (2023) found that developers using AI coding assistants completed a defined coding task approximately 55% faster than a control group. However, the same studies have consistently noted that the quality of AI-generated code — including its correctness, security, and maintainability — depends strongly on the task definition and the contextual information available to the model.

### 2.2 Specification-Driven Development

The importance of formal specification documents in software engineering is well established in the literature. Boehm (1981) demonstrated that defects introduced during requirements specification are an order of magnitude more expensive to correct after deployment than during the specification phase itself — a finding that has been replicated in numerous subsequent studies. The IEEE software requirements specification standard (IEEE Std 830-1998) and its successor (ISO/IEC/IEEE 29148:2018) provide widely adopted frameworks for producing complete, verifiable, and unambiguous requirements documents.

Model-driven architecture (MDA), as defined by the Object Management Group, represents a related tradition in which formal models serve as the primary artifact from which code is generated (Kleppe et al., 2003). The workflow proposed in this paper shares MDA's emphasis on specification as the locus of intellectual work but relaxes the requirement for formal machine-interpretable models in favor of structured natural language documents that can serve simultaneously as human-readable engineering artifacts and as AI generation prompts.

### 2.3 AI and Requirements Engineering

A growing body of work has examined the intersection of AI and requirements engineering specifically. Arora et al. (2019) demonstrated that NLP techniques could be applied to automatically detect ambiguity and incompleteness in natural language requirements specifications. Ferrari et al. (2018) investigated the use of AI to classify and structure requirements from informal project documentation. The present work extends this tradition by treating AI not merely as a passive analyzer of requirements but as an active generator of specification documents from higher-level inputs.

---

## 3. Phase 1 — The Project Scope Document

### 3.1 Definition and Purpose

The Project Scope Document (PSD) is the foundational artifact of the proposed workflow. It represents the human team's authoritative statement of what the system must accomplish, who it serves, and what constraints apply. In the context of AI-assisted development, the PSD serves a dual function: it is simultaneously a traditional project management artifact — aligned with the scope management processes defined in the PMBOK Guide (PMI, 2021) — and a structured prompt that will be submitted to an AI system to initiate the generation of all downstream specification documents.

This dual function has important implications for how the PSD must be written. It must satisfy the human engineering team's need for clarity and consensus, and it must also provide the AI with sufficient context, precision, and structural organization to generate accurate and complete downstream documents. A PSD that is adequate for human purposes but ambiguous or incomplete from the AI's perspective will produce downstream documents that require extensive iteration to correct.

### 3.2 Rationale

The rationale for investing in a formal PSD, rather than proceeding directly to requirements elicitation or code generation, rests on three foundations.

First, the process of writing the PSD forces stakeholder alignment. Disagreements about scope, objectives, and constraints that are not surfaced and resolved at this stage will propagate through every subsequent artifact and ultimately into the codebase itself, where they are far more expensive to resolve.

Second, LLMs perform significantly better when provided with rich, structured contextual information. A model that understands the domain, the intended users, the business goals, and the technical constraints will generate more relevant and accurate requirements than one given only a brief description. This is consistent with the broader literature on prompt engineering, which consistently identifies context richness as a primary determinant of LLM output quality (Brown et al., 2020; Wei et al., 2022).

Third, the PSD establishes a stable reference point for the iterative refinement process described in Section 5. When downstream documents are found to be incomplete or incorrect, the team must determine whether the problem is a specification gap in the PSD or a generation error by the AI. Without a stable PSD, this diagnosis is impossible.

### 3.3 Required Sections

A well-formed PSD for AI-assisted development contains the following eight sections:

**3.3.1 Project Overview.** A concise description of the system to be built, the domain it operates in, and the primary problem it solves. This section should be written as if explaining the project to a knowledgeable colleague who is unfamiliar with the specific organizational context.

**3.3.2 Objectives and Success Criteria.** A numbered list of specific, measurable objectives for the project, accompanied by the criteria that will be used to determine whether each objective has been achieved. Vague formulations such as "improve user experience" should be replaced with specific, verifiable targets such as "reduces average task completion time from twelve steps to four steps as measured by usability testing."

**3.3.3 Stakeholders and User Personas.** A description of who will use the system, their technical sophistication, their goals, and their pain points. This section should identify primary users, secondary users, and any administrative or operational roles. The AI uses this information to make contextually appropriate decisions about interface complexity, error messaging vocabulary, and access control granularity.

**3.3.4 In-Scope Features and Capabilities.** An explicit enumeration of what the system must do. This is not a full requirements list but a high-level feature catalog. Each item should be described in sufficient detail that the AI can infer the type and approximate scope of the requirements it will generate from it.

**3.3.5 Out-of-Scope Exclusions.** An explicit list of things the system will not do in the current iteration. This section is as important as the in-scope list. Without it, the AI will make assumptions about scope boundaries that are likely to produce requirements and design elements for unintended features, creating both unnecessary work and a misleading false sense of completeness.

**3.3.6 Technical Constraints and Environment.** The programming languages, frameworks, platforms, databases, and infrastructure the system must use or integrate with. This section should also specify any performance requirements, security standards, regulatory compliance requirements, or accessibility standards that apply as hard constraints rather than preferences.

**3.3.7 Assumptions and Dependencies.** A list of assumptions the team is making about the environment, users, or other systems, as well as dependencies on external services, APIs, or other software components. These inform the AI about what it may treat as given versus what it must design for.

**3.3.8 AI Instruction Directives.** A section unique to AI-assisted workflows that provides explicit meta-instructions to the AI about how to interpret the document. This may include instructions about the desired output document format, required level of detail, naming conventions, preferred architectural patterns, and which downstream documents to generate. The inclusion of explicit AI directives is strongly recommended; without them, the AI will make implicit assumptions about output format and scope that may not align with team conventions.

### 3.4 Writing the PSD as an Effective AI Prompt

Because the PSD will be submitted to an AI to generate downstream documents, its stylistic properties matter as much as its content. Several principles guide effective PSD authorship for AI consumption.

*Explicitness over implication.* Never assume the AI will infer an unstated requirement from context. If the system must support 10,000 concurrent users, state it. If user passwords must be hashed using a specific algorithm, state it. LLMs will generate plausible defaults when information is absent, and those defaults may not match the team's requirements.

*Terminological consistency.* Inconsistent terminology causes the AI to treat synonymous concepts as distinct, producing redundant or contradictory requirements. If the main data entity is called a "record" in the project overview, it should be called a "record" throughout the entire document.

*Structural separation of concerns.* Use the document's section structure to clearly delineate what is a business goal, what is a functional requirement, what is a technical constraint, and what is an assumption. These categories have different implications for how the AI should treat them in downstream documents.

*Concrete examples.* Describing expected inputs and outputs, even briefly, substantially improves the AI's ability to generate accurate requirements and test cases. An example is worth several paragraphs of abstract description.

---

## 4. Phase 2 — AI-Generated Specification Documents

With a complete and reviewed PSD, the team submits it to the AI to generate three interconnected specification documents: the Software Requirements Specification (SRS), the Software Design Description (SDD), and the Traceability Matrix (TM). These three documents form the engineering backbone of the project, translating high-level goals into verifiable, implementable, and traceable engineering artifacts.

### 4.1 The Software Requirements Specification

#### 4.1.1 Definition and Purpose

The Software Requirements Specification (SRS) is a comprehensive document that enumerates every requirement the system must satisfy. Conforming to the structure defined in IEEE Std 830-1998 and its successor ISO/IEC/IEEE 29148:2018, the SRS transforms the high-level goals articulated in the PSD into precise, verifiable statements that can be directly tested and traced to design and implementation elements. The SRS is the primary contract between the stakeholders who define what the system must do and the engineers — human and AI — who will build it.

#### 4.1.2 Rationale

The SRS serves several critical functions in an AI-assisted development workflow. It forces the AI to make explicit every implicit assumption about system behavior, surfacing gaps and conflicts that might otherwise remain latent until testing or deployment. It provides a stable, formal reference against which generated code can be evaluated for correctness. And it establishes the controlled vocabulary that all subsequent documents and generation prompts will reference.

Without a formal SRS, AI-generated code reflects the model's interpolation of unstated requirements. The resulting system may appear functional, but it cannot be demonstrated to be correct because no formal definition of correctness exists against which to evaluate it. This is a fundamental auditability and maintainability problem, particularly in organizational contexts with compliance, security, or regulatory obligations.

#### 4.1.3 Required Content

A complete SRS generated from the PSD should contain the following elements:

- **Introduction:** Document purpose, intended audience, scope, and applicable definitions
- **System Overview:** Context diagram and high-level system description
- **Functional Requirements (FR-XXX):** Each with a unique identifier, precise description, priority classification (High/Medium/Low), preconditions, and formal acceptance criteria
- **Non-Functional Requirements (NFR-XXX):** Covering performance, scalability, security, usability, reliability, availability, and maintainability, each with quantitative acceptance criteria wherever possible
- **Interface Requirements (IR-XXX):** User interfaces, external APIs, hardware interfaces, and communication protocols
- **Data Requirements (DR-XXX):** Data models, retention policies, privacy requirements, and integrity constraints
- **Constraint and Compliance Requirements (CR-XXX):** Regulatory, legal, and standards compliance obligations
- **Glossary:** Definitions of all domain-specific and project-specific terms used in the document

#### 4.1.4 Requirement Quality Criteria

Each requirement in the SRS must satisfy the SMART criteria as adapted for software requirements engineering: **S**pecific (unambiguous — admits only one interpretation), **M**easurable (verifiable — can be tested and pass or fail), **A**chievable (feasible within the stated technical constraints), **R**elevant (necessary — traces to a stated objective in the PSD), and **T**raceable (linkable — has a unique identifier and can be referenced from design and test documents). Requirements that fail any of these criteria should be revised before the document is accepted and before Phase 3 iteration commences.

### 4.2 The Software Design Description

#### 4.2.1 Definition and Purpose

The Software Design Description (SDD) translates the requirements in the SRS into a concrete architectural and component-level design for the system. Where the SRS defines what the system must do, the SDD defines how it will do it. The SDD is the structural blueprint from which implementation code will be generated, and it is the primary mechanism for ensuring architectural consistency across all code generation sessions.

#### 4.2.2 Rationale

Generating code directly from requirements, without an intervening design document, is one of the most commonly observed and consequential mistakes in AI-assisted development practice. The problem is architectural incoherence: when each code generation session operates without an explicit design context, the AI makes independent architectural decisions for each component. These decisions may be individually reasonable but collectively inconsistent — producing a codebase with incompatible interface patterns, redundant abstractions, inconsistent error handling, and data flow problems that are only discovered during integration.

The SDD addresses this problem by forcing all architectural decisions to be made explicitly and coherently before any code is generated. It provides each code generation session with the structural context needed to produce a component that is correctly positioned within the larger system. This is directly analogous to the role of an architect's drawings in construction: without them, each subcontractor builds to their own interpretation of the requirements, and the resulting structure may not assemble correctly.

#### 4.2.3 Required Content

A complete SDD conforming to IEEE Std 1016-2009 should contain:

- **System Architecture Overview:** Top-level decomposition into subsystems or architectural layers, with explicit rationale for the chosen architectural pattern (layered, microservices, event-driven, etc.)
- **Component Descriptions:** For each component: its responsibilities, its public interface (with fully typed inputs and outputs), its internal dependencies, and its error handling and logging behavior
- **Data Architecture:** Entity-relationship models, database schemas, data flow diagrams, and state models for stateful entities
- **Integration Architecture:** Inter-component communication patterns, internal API contracts, event schemas, and message formats
- **Security Architecture:** Authentication and authorization models, data encryption strategies at rest and in transit, input validation patterns, and audit logging specifications
- **Deployment Architecture:** Infrastructure topology, containerization strategy, configuration management approach, and environment-specific behavior
- **Technology Decision Record:** A structured log of key technology choices with the rationale for each, enabling future maintainers to understand why the system was designed as it was

#### 4.2.4 Interface Specification Standards

Interface specifications in the SDD must be complete enough to enable independent generation of any two interacting components. At minimum, each interface specification must include the operation name, all parameters with types, the return type, all possible error conditions and their representations, and any relevant preconditions or postconditions. Underspecified interfaces are among the most common sources of integration failures in AI-generated codebases.

### 4.3 The Traceability Matrix

#### 4.3.1 Definition and Purpose

The Traceability Matrix (TM) is a structured artifact that maps every requirement in the SRS to the SDD design elements that implement it and to the test cases that verify it. It functions as a formal proof of completeness: a demonstration that the system as designed and as tested is complete with respect to the system as specified.

#### 4.3.2 Rationale

In AI-assisted development, the TM serves a verification function that is more important than in traditional development, for reasons specific to how LLMs generate content. Because AI systems produce large volumes of content rapidly, it is possible for a requirement to be omitted from the design without any human reviewer noticing during document review. Similarly, the AI may generate design elements or test cases that have no corresponding requirement — evidence of scope creep that occurred implicitly during the generation process. The TM makes both of these failure modes immediately visible.

The TM also functions as a forcing function during document generation. When the AI is instructed to generate the TM, it must explicitly account for every requirement. Requirements that cannot be traced to a design element reveal gaps in the SDD. Requirements with no associated test cases reveal gaps in the test plan. This property makes the TM one of the highest-leverage quality assurance artifacts in the entire workflow: a single document that simultaneously validates the completeness of the SRS, the SDD, and the test specification.

#### 4.3.3 Structure

The TM is structured as a table with the following columns:

| Column | Description |
|--------|-------------|
| Requirement ID | Unique identifier from the SRS (e.g., FR-001) |
| Requirement Summary | Brief description of the requirement |
| Design Element | SDD component(s) implementing this requirement |
| Test Case ID(s) | Test case(s) verifying this requirement |
| Implementation Status | Not Started / In Progress / Complete / Verified |
| Notes | Exceptions, deferrals, or clarifications |

The TM should be maintained as a living document throughout the project lifecycle and updated whenever any of the three documents it traces — the SRS, the SDD, or the test specification — are modified.

---

## 5. Phase 3 — Iterative Refinement

### 5.1 Overview

A single-pass generation of the SRS, SDD, and TM from the PSD will rarely produce documents of sufficient quality to proceed directly to code generation. Phase 3 is a structured iterative process that brings the specification documents to the required quality level before implementation begins. The investment in this phase is repaid many times over in reduced rework during code generation and testing.

### 5.2 The Iteration Loop

The iteration loop follows a consistent four-step pattern. First, the team reviews the generated documents against the quality criteria defined in Section 4. Second, deficiencies are identified and categorized as either *PSD gaps* — the original scope document was incomplete or ambiguous — or *generation errors* — the AI misinterpreted or omitted something that was adequately specified in the PSD. Third, PSD gaps require the PSD to be updated, and the affected downstream documents are regenerated; generation errors can often be corrected by submitting targeted clarification prompts to the AI without full regeneration. Fourth, all changes are recorded in the Change Log (see Section 9).

This distinction between PSD gaps and generation errors is not merely administrative. It determines the remediation strategy and the scope of downstream impact. A PSD gap may require changes to multiple sections of the SRS and SDD. A generation error in a specific requirement may require only a targeted update to that requirement and its dependent TM entries.

### 5.3 Document Review Checklists

The following review criteria are applied to each generated document before it is accepted.

**SRS Review Criteria:**

- Every feature enumerated in the PSD in-scope section has at least one corresponding functional requirement
- Every item in the PSD out-of-scope section is absent from the SRS
- All non-functional requirements have quantitative, measurable acceptance criteria
- No two requirements contradict each other
- All domain terms are defined in the glossary
- Every requirement has a unique identifier conforming to the project's naming convention

**SDD Review Criteria:**

- Every functional requirement has at least one corresponding design element
- Component interfaces are fully specified — no untyped parameters, no implicit return behaviors
- The data model is complete and consistent with all data-related requirements
- Security requirements are explicitly reflected in the security architecture section
- The deployment architecture is consistent with the technical constraints in the PSD
- All technology decisions are documented with rationale

**Traceability Matrix Review Criteria:**

- Every SRS requirement appears in the TM with at least one design element reference and at least one test case reference
- No orphan design elements exist (design elements not traceable to any requirement)
- No orphan test cases exist (test cases not traceable to any requirement)
- The status column accurately reflects the current implementation state

### 5.4 Iteration Termination Criteria

Iteration terminates when all three review checklists are fully satisfied and all identified issues have been resolved and recorded in the Change Log. The temptation to proceed to code generation before this condition is met — particularly when timelines are constrained — is one of the most significant risks in AI-assisted development workflows. Specification gaps that are allowed to persist into the code generation phase will produce defects that are far more expensive to correct than the time that would have been spent resolving them in the specification phase.

---

## 6. Phase 4 — Test Planning

### 6.1 The Role of Test Planning in AI-Assisted Development

Test planning must precede code generation. This is a normative claim, not merely a practical recommendation, and it derives from the fundamental epistemological problem of AI code generation: if tests are written after the fact, they test what the code does rather than what it should do. In traditional development, this is a well-recognized anti-pattern. In AI-assisted development, it is particularly acute because the AI can generate code that is internally self-consistent while being inconsistent with the actual requirements, and post-hoc tests written by the same AI system against the same code will tend to validate that self-consistency rather than reveal the divergence.

By contrast, tests generated from the SRS requirements before code generation provide an objective, requirement-grounded verification instrument that is independent of the implementation.

### 6.2 The Test Plan Document

The Test Plan defines the overall testing strategy for the project. It is a management-level document that establishes the framework within which individual test cases are specified and executed. A complete Test Plan includes:

- Testing objectives and scope
- Testing levels to be performed: unit, integration, system, and user acceptance testing
- Testing approach and methodologies for each level
- Test environment requirements and configuration
- Entry and exit criteria for each testing phase
- Defect severity classifications and management process
- Test reporting requirements and reporting cadence
- Roles and responsibilities for test activities

### 6.3 Test Case Specification

Individual test cases are generated from the SRS requirements and must be linked to their source requirements in the TM before code generation begins. Each test case must specify: a unique identifier (TC-XXX), the requirement ID(s) it verifies, any necessary preconditions, the sequence of test steps, the expected result of each step, and the pass/fail acceptance criteria.

In AI-assisted development, test cases serve a dual purpose. They are used post-generation to verify the correctness of generated code, but they are also submitted to the AI as part of the code generation prompt to constrain the AI's interpretation of the required behavior. A well-specified test case is among the most precise instructions that can be provided to an AI code generator: it specifies not just what the code should do in general terms, but what specific output it must produce for specific inputs.

### 6.4 AI-Generated Test Scaffolding

Once test cases are specified and reviewed, the AI is instructed to generate test scaffolding: the code structure, mock objects, test fixtures, test data factories, and testing utilities required to execute the test cases. This scaffolding is generated and verified before implementation code is generated, establishing the failing ("red") state of the test-driven development cycle. This approach ensures that the relationship between tests and implementation is one of verification rather than rationalization.

---

## 7. Phase 5 — Code Generation

### 7.1 Code Generation Strategy

#### 7.1.1 Component-by-Component Generation

Large applications must not be generated in a single prompting session. Single-session generation of substantial codebases consistently produces architecturally incoherent output, even when a detailed SDD is provided as context. The recommended strategy is component-by-component generation following the dependency order established in the SDD: foundational layers (data models, shared utilities, type definitions) are generated first, followed by business logic components, followed by interface and integration components.

This ordering ensures that each component is generated with full awareness of the interfaces it depends upon, and that the AI does not need to speculate about the structure of components that have not yet been generated.

#### 7.1.2 Generation Prompt Structure

Each code generation prompt should follow a consistent four-part structure:

1. **Context:** The component being generated, its responsibilities as described in the SDD, and its position in the system architecture
2. **Specifications:** The relevant functional requirements from the SRS that this component must satisfy, the interface specification from the SDD, and the test cases it must pass
3. **Conventions:** Coding style, error handling patterns, logging standards, and any component-specific constraints
4. **Instruction:** The explicit generation request

This structure prevents the AI from making implicit assumptions about any aspect of the generated component and ensures that each generation session produces output that is consistent with both the specification and the broader codebase.

### 7.2 Code Review and Validation

AI-generated code must be reviewed before integration into the codebase. This review encompasses four dimensions. *Correctness* verifies that the code satisfies its specified requirements and passes its test cases. *Consistency* verifies that the code follows the patterns established in previously generated components. *Security* verifies that the code handles untrusted input safely, manages credentials appropriately, and avoids the most common vulnerability classes. *Maintainability* verifies that the code is readable and appropriately documented.

Automated static analysis, security scanning, and code quality tools should be applied to all generated code. Many common AI code generation deficiencies — including hard-coded credentials, injection vulnerabilities, unhandled exception paths, and missing null checks — are reliably detectable by standard static analysis tools. Automated scanning should be a non-negotiable step in the code integration process, not an optional enhancement.

### 7.3 Test Execution and Failure Analysis

After each component is generated, the relevant test cases are executed immediately. Test failures must be categorized before remediation begins. A *code generation error* indicates that the AI produced code that is incorrect with respect to the specification, and the remedy is to revise the generation prompt or correct the code. A *test specification error* indicates that the test case was incorrectly specified, and the remedy is to revise the test case and update the TM. A *specification gap* indicates that the requirement or design element was underspecified, and the remedy is to update the relevant upstream documents and trigger the appropriate iteration cycle.

Correct categorization of failures is important because each category has different upstream implications. Treating a specification gap as a code generation error will result in code that passes its tests but still fails to satisfy the actual requirement — a condition that may not be discovered until system testing or user acceptance testing.

### 7.4 Integration Testing

After all individual components have been generated and their unit tests pass, integration testing verifies that components interact correctly across their specified interfaces. Integration test cases are derived from the integration architecture section of the SDD and should exercise both the expected (happy-path) and error-condition behaviors of each interface. The AI can generate integration test scaffolding from the SDD interface specifications using the same approach described in Section 6.4.

---

## 8. Phase 6 — Documentation and Delivery

### 8.1 Overview

A functioning application that passes its tests is a necessary but not sufficient deliverable. Phase 6 produces the documentation artifacts required to make the system deployable, operable, and maintainable by parties who were not involved in its construction.

### 8.2 Technical Documentation

**8.2.1 API Documentation.** If the system exposes interfaces — whether internal service APIs or external-facing endpoints — complete API documentation must be generated. This documentation should include endpoint descriptions, request and response schemas with type specifications, authentication and authorization requirements, error codes and their semantics, rate limiting behavior, and usage examples. The AI can generate a substantial portion of this documentation from the interface specifications in the SDD, which should be reviewed and supplemented by the engineering team.

**8.2.2 Deployment Guide.** The deployment guide documents the procedures for installing, configuring, and running the system in each supported environment. It should include infrastructure requirements, environment variable specifications with valid value ranges and default behaviors, database migration procedures, and post-deployment verification steps. The deployment guide must be treated as a tested artifact: deployment procedures should be executed against a clean environment and verified before the guide is accepted.

**8.2.3 Operations Runbook.** The operations runbook describes how to monitor, troubleshoot, and maintain the running system. It should cover alert definitions and response procedures, common failure modes and their diagnosis, backup and recovery procedures, and escalation paths. The runbook is a critical artifact for organizational knowledge retention: it encodes the operational knowledge that would otherwise exist only in the memories of the team members who built the system.

### 8.3 User Documentation

User-facing documentation should be generated from the functional requirements and user persona descriptions in the SRS and PSD. AI-generated draft documentation of this type typically requires more human editorial refinement than technical documentation because it must be calibrated to the vocabulary, context, and task model of the intended user population. Where budget allows, AI-generated user documentation drafts should be reviewed and refined by a technical writer with access to representative users.

### 8.4 Final Traceability Audit

The final deliverable of Phase 6 is a completed traceability audit report demonstrating that every requirement in the SRS is traceable to implemented and tested code and to documentation. This audit report serves as the definitive quality gate of the workflow. Requirements without corresponding verified implementation, test coverage, or documentation are treated as defects requiring resolution before delivery. The audit report should be archived with the project's other specification documents as a permanent record of the delivery state.

---

## 9. Change Management and Version Control

### 9.1 The Change Log

The Change Log is a chronological record of every significant decision and document change made throughout the project. Each entry should record the date, the document or artifact affected, a description of the change, the business or technical rationale for the change, and the name of the individual who authorized it. The Change Log serves as the institutional memory of the project, answering the question "why is the system designed this way?" for future maintainers who were not present when the decisions were made.

In AI-assisted development workflows, the Change Log has particular importance because the speed and volume of AI generation can create an illusion of completeness that obscures the history of decisions and revisions. A well-maintained Change Log counteracts this illusion by making the iterative nature of the process explicit and traceable.

### 9.2 Document Version Control

All specification documents should be stored in a version-controlled repository alongside the codebase. This practice enables three critical capabilities: the ability to determine which version of the SDD was current when a given component was generated; the ability to identify when a specification was changed and trace downstream impacts; and the ability to restore a previous specification state if a change is found to be incorrect. Specification documents in plain text or structured text formats (Markdown, YAML, JSON) are significantly more amenable to version control than binary document formats.

### 9.3 Specification Drift

Specification drift — the gradual divergence between the documented specification and the actual implemented system — is one of the most insidious long-term risks in software development. In AI-assisted development, this drift can occur with unusual speed because the ability to generate large amounts of code rapidly creates strong incentive pressure to skip documentation updates.

The recommended mitigation is a project policy that no implementation change is complete until the affected specification documents are updated and the TM is reconciled. The Traceability Matrix provides an effective operational mechanism for enforcing this policy: if a proposed code change cannot be mapped to an existing requirement, it must either be traced to a new requirement (which must be added to the SRS and reviewed), or its necessity must be questioned.

---

## 10. Best Practices and Common Pitfalls

### 10.1 Best Practices

**10.1.1 Invest Disproportionately in the PSD.** The quality of every downstream artifact is bounded by the quality of the PSD. Analysis of the iterative refinement phase consistently reveals that the majority of SRS and SDD deficiencies can be traced to gaps or ambiguities in the PSD rather than to AI generation errors. Time invested in PSD refinement before AI generation commences is the highest-leverage investment in the entire workflow.

**10.1.2 Use the AI as a Reviewer.** In addition to generating documents, the AI can be instructed to review its own output against the PSD, identifying gaps, contradictions, and ambiguities. This self-review step, performed after initial document generation, frequently surfaces issues that would otherwise require a full human review cycle to detect. The AI can also be instructed to critique specific requirements for testability, identify design elements with underspecified interfaces, and flag TM entries with missing test coverage.

**10.1.3 Maintain Strict Identifier Discipline.** Every requirement should have a unique, stable identifier (FR-001, NFR-007, etc.) that is never reused and never changed, even if the requirement is substantially revised. When a requirement is deprecated, it should be marked as deprecated in the SRS rather than deleted. This discipline preserves traceability integrity across the entire project lifecycle and is essential for audit and compliance purposes.

**10.1.4 Generate Code in Small, Testable Increments.** The temptation to generate large amounts of code in a single session should be resisted consistently. Smaller generation sessions, bounded by the component boundaries defined in the SDD, produce more coherent output and make it significantly easier to identify and isolate errors before they propagate through the codebase.

### 10.2 Common Pitfalls

**10.2.1 Generating Code Directly from Requirements.** Omitting the SDD and generating code directly from the SRS is the single most commonly observed and most damaging mistake in AI-assisted development practice. The architectural incoherence that results from this approach is typically not apparent until integration testing, at which point correcting it requires substantial rework.

**10.2.2 Accepting Generated Documents Without Critical Review.** AI-generated specification documents are not authoritative outputs — they are drafts that require expert human review. Common generation errors include requirements that are subtly inconsistent with stated constraints, design elements that technically satisfy requirements but employ inappropriate patterns for the domain, and test cases that cover happy-path scenarios but omit important error conditions.

**10.2.3 Neglecting Non-Functional Requirements.** LLMs trained primarily on source code and technical documentation tend to under-specify non-functional requirements — particularly security, performance, and scalability — unless explicitly prompted to address them. These requirements must be stated explicitly in the PSD and formally verified in the SRS or they will be systematically underrepresented in the design and implementation.

**10.2.4 Deferring Test Planning.** Teams that defer test planning to after code generation consistently find that their test cases validate what the code does rather than what it should do. The resulting false sense of test coverage is a significant risk, particularly in systems with security or compliance obligations.

---

## 11. Tools and Technology Considerations

### 11.1 AI Model Selection

Not all LLMs are equally suited to specification-driven development workflows. The most important evaluation criteria are instruction-following fidelity (how accurately does the model follow complex, multi-part, structured instructions?), effective context window size (can the model reliably attend to a full PSD and SRS simultaneously without losing information?), output format consistency (does the model produce reliably structured output suitable for machine parsing and review?), and domain knowledge depth (does the model have strong knowledge of the relevant technology stack, domain conventions, and applicable standards?).

### 11.2 Prompt Management

The prompts used to drive each generation step are themselves valuable intellectual property and engineering artifacts. As the workflow matures, these prompts will be refined through experience. They should be stored in version-controlled repositories, documented with the rationale for their structure, and treated as first-class project infrastructure rather than ephemeral inputs. Prompt templates for PSD-to-SRS generation, SRS-to-SDD generation, SDD-to-code generation, and other workflow transitions should be maintained, versioned, and shared across projects where the technology domain is similar.

### 11.3 Document Format Considerations

Specification documents stored in plain text formats (Markdown, reStructuredText) or structured formats (YAML, JSON for machine-readable sections) offer significant advantages over binary document formats for AI-assisted workflows. They can be directly submitted to AI systems as part of generation prompts without conversion or extraction. They support meaningful version control diffing. And they can be processed programmatically for traceability analysis, completeness checking, and report generation.

### 11.4 Continuous Integration

AI-generated code should be integrated into a continuous integration (CI) pipeline from the first day of code generation. Automated test execution, static analysis, security vulnerability scanning, and build verification provide objective quality signals that are essential for maintaining confidence in a rapidly growing AI-generated codebase. The CI pipeline should be configured and verified before code generation begins, so that generated components can be integrated and tested immediately upon completion.

---

## 12. Discussion

### 12.1 Implications for Software Engineering Practice

The workflow proposed in this paper is, at its foundation, an argument that the emergence of AI code generation does not reduce the importance of software engineering discipline — it amplifies it. The principal effect of AI generation tools is to shift the locus of intellectual work. In traditional development, substantial effort is expended translating specifications into code. AI tools automate much of this translation, which is a genuine and significant productivity benefit. However, this benefit is only realized when the specifications being translated are correct, complete, and internally consistent. The preparation of such specifications is the intellectual work that AI cannot automate, and it is precisely the work that the proposed workflow is designed to support.

This has an important implication for how organizations should configure their teams and their training investments when adopting AI-assisted development. The skills that become more valuable are requirements elicitation, specification writing, architectural design, and systematic testing — the disciplines that produce the inputs to AI generation. The skills that become less differentiating are the ability to write large amounts of correct boilerplate code and the ability to remember syntax and API details. Organizations that invest in the former while relying on AI for the latter are likely to realize the full productivity potential of AI-assisted development.

### 12.2 Limitations and Future Work

The workflow described in this paper has several limitations that suggest directions for future work. First, the workflow as described is primarily sequential, with iteration occurring within phases. In practice, teams operating under aggressive timelines may need to parallelize certain activities, and the interaction effects of such parallelism require further investigation.

Second, the quality criteria for specification documents described in this paper are primarily qualitative. Future work should develop quantitative metrics for specification quality in the context of AI-assisted development — metrics that can predict the expected number of iteration cycles required, the likely defect density of generated code, or the probability of successful single-pass code generation for a given specification.

Third, this paper does not address the specific challenges of AI-assisted development in regulated industries, where compliance documentation requirements may impose additional artifact obligations beyond those described here. The extension of this workflow to domains such as medical device software (IEC 62304), automotive software (ISO 26262), or aerospace software (DO-178C) represents an important area for future investigation.

---

## 13. Conclusion

This paper has presented a six-phase workflow for AI-integrated software development that systematizes the use of AI code generation within a structured, document-driven engineering process. The workflow addresses the fundamental specification-sensitivity of AI code generation tools by mandating a hierarchy of specification artifacts — the Project Scope Document, Software Requirements Specification, Software Design Description, and Traceability Matrix — that collectively provide the AI with the context, precision, and structural information required to generate correct and maintainable code.

The central finding is that the discipline of software specification is more important in AI-assisted development than in traditional development, not less. AI code generation tools amplify both the precision of well-formed specifications and the consequences of poorly formed ones. The teams that realize the greatest benefit from these tools are not those who treat them as shortcuts around the hard work of software engineering, but those who use them as force multipliers for that work — generating more comprehensive requirements, more thorough test coverage, more consistent designs, and more complete documentation than would be feasible without AI assistance.

The workflow described here is not a final or complete answer to the challenges of AI-assisted development. It is a practical starting point — grounded in established software engineering principles and adapted for the specific demands of AI-mediated development — that development teams can adopt, adapt, and improve as the tools and the practice continue to evolve.

---

## 14. References

Arora, C., Sabetzadeh, M., Briand, L., & Zimmer, F. (2019). Automated extraction and clustering of requirements glossary terms. *IEEE Transactions on Software Engineering, 43*(10), 918–945.

Balog, M., Gaunt, A. L., Brockschmidt, M., Nowozin, S., & Tarlow, D. (2017). DeepCoder: Learning to write programs. *Proceedings of the 5th International Conference on Learning Representations (ICLR 2017)*.

Boehm, B. W. (1981). *Software engineering economics*. Prentice-Hall.

Brown, T. B., Mann, B., Ryder, N., Subbiah, M., Kaplan, J., Dhariwal, P., … & Amodei, D. (2020). Language models are few-shot learners. *Advances in Neural Information Processing Systems, 33*, 1877–1901.

Chen, M., Tworek, J., Jun, H., Yuan, Q., Pinto, H. P. de O., Kaplan, J., … & Zaremba, W. (2021). *Evaluating large language models trained on code* (arXiv:2107.03374). arXiv.

Ferrari, A., Spoletini, P., & Gnesi, S. (2018). Ambiguity and tacit knowledge in requirements elicitation interviews. *Requirements Engineering, 21*(3), 333–355.

Hindle, A., Barr, E. T., Gabel, M., Su, Z., & Devanbu, P. (2012). On the naturalness of software. *Proceedings of the 34th International Conference on Software Engineering (ICSE 2012)*, 837–847.

IEEE Computer Society. (1998). *IEEE recommended practice for software requirements specifications* (IEEE Std 830-1998). IEEE.

IEEE Computer Society. (2009). *IEEE standard for information technology — Systems and software engineering — Software life cycle processes — Software design descriptions* (IEEE Std 1016-2009). IEEE.

ISO/IEC/IEEE. (2018). *Systems and software engineering — Life cycle processes — Requirements engineering* (ISO/IEC/IEEE 29148:2018). ISO.

Kleppe, A. G., Warmer, J., & Bast, W. (2003). *MDA explained: The model driven architecture — Practice and promise*. Addison-Wesley.

Peng, S., Kalliamvakou, E., Cihon, P., & Demirer, M. (2023). *The impact of AI on developer productivity: Evidence from GitHub Copilot* (arXiv:2302.06590). arXiv.

Project Management Institute. (2021). *A guide to the project management body of knowledge (PMBOK® Guide)* (7th ed.). PMI.

Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., … & Zhou, D. (2022). Chain-of-thought prompting elicits reasoning in large language models. *Advances in Neural Information Processing Systems, 35*, 24824–24837.

Ziegler, A., Kalliamvakou, E., Li, X. A., Rice, A., Rifkin, D., Simister, T., … & Aftandilian, E. (2022). Productivity assessment of neural code completion. *Proceedings of the 6th ACM SIGPLAN International Symposium on Machine Programming (MAPS 2022)*, 21–29.

---

## Appendix A — Document Templates and Prompt Structures

### A.1 Project Scope Document Template

```
# Project Scope Document
Version: [X.Y]  |  Date: [YYYY-MM-DD]  |  Author: [Name]

## AI Instruction Directives
[Explicit instructions to the AI about how to interpret this document
and what to generate from it.]

## 1. Project Overview
[2–3 paragraphs describing the system, domain, and problem being solved.]

## 2. Objectives and Success Criteria
1. [Objective]: [Success criterion]
2. [Objective]: [Success criterion]

## 3. Stakeholders and User Personas
### Primary Users
[Description, technical level, goals, pain points]

### Secondary Users / Administrators
[Description, technical level, goals]

## 4. In-Scope Features
1. [Feature name]: [Brief description]
2. [Feature name]: [Brief description]

## 5. Out-of-Scope Exclusions
- [Excluded feature or capability]
- [Excluded feature or capability]

## 6. Technical Constraints and Environment
- Programming Language(s): [Languages]
- Framework(s): [Frameworks]
- Database: [Database system]
- Deployment Target: [Infrastructure]
- Performance Constraints: [Specific targets]
- Security Standards: [Applicable standards]
- Accessibility Standards: [Applicable standards]

## 7. Assumptions and Dependencies
- [Assumption or dependency]
- [Assumption or dependency]

## 8. Glossary
| Term | Definition |
|------|------------|
| [Term] | [Definition] |
```

### A.2 Requirement Identifier Convention

| Prefix | Requirement Type |
|--------|-----------------|
| FR-XXX | Functional Requirement |
| NFR-XXX | Non-Functional Requirement |
| IR-XXX | Interface Requirement |
| DR-XXX | Data Requirement |
| CR-XXX | Constraint / Compliance Requirement |
| TC-XXX | Test Case |
| DE-XXX | Design Element (SDD) |
| CL-XXX | Change Log Entry |

### A.3 AI Generation Prompt Templates

**PSD → SRS Generation Prompt:**

```
You are a senior software requirements engineer with expertise in IEEE 830
requirements specification standards.

Using the attached Project Scope Document as your sole source of truth,
generate a complete Software Requirements Specification (SRS) conforming
to IEEE Std 830-1998 / ISO/IEC/IEEE 29148:2018.

Requirements:
- For each in-scope feature, generate numbered functional requirements
  (FR-XXX) with: unique identifier, description, priority (High/Medium/Low),
  preconditions, and measurable acceptance criteria.
- Generate non-functional requirements (NFR-XXX) for all performance,
  security, and scalability constraints stated in the PSD.
- Generate interface requirements (IR-XXX) for all stated user interface,
  API, and integration points.
- Generate data requirements (DR-XXX) for all data entities, retention
  policies, and integrity constraints implied or stated in the PSD.
- Assign each requirement a unique identifier and a verification method
  (Inspection / Analysis / Test / Demonstration).
- Include a glossary of all domain-specific and project-specific terms.
- Explicitly flag any ambiguities or gaps in the PSD that prevent you from
  writing a complete, testable requirement.

Do not generate requirements for any feature listed in the Out-of-Scope
section of the PSD.
```

**SRS → SDD Generation Prompt:**

```
You are a senior software architect.

Using the attached Software Requirements Specification as your primary input,
generate a complete Software Design Description (SDD) conforming to
IEEE Std 1016-2009.

Requirements:
- Define the top-level system architecture and provide explicit rationale
  for the architectural pattern chosen.
- For each component: specify its responsibilities, its complete public
  interface (with fully typed parameters and return values), its internal
  dependencies, and its error handling behavior.
- Design a complete data schema satisfying all data requirements in the SRS.
- Specify all inter-component communication patterns, internal API contracts,
  and event/message schemas.
- Define the security architecture including authentication, authorization,
  encryption, and audit logging.
- Define the deployment architecture consistent with the technical constraints
  in the originating PSD.
- Document all key technology decisions with explicit rationale.
- Flag any SRS requirements that are insufficiently specified to support
  unambiguous design.
```

**SRS + SDD → Traceability Matrix Generation Prompt:**

```
You are a software quality assurance engineer.

Using the attached SRS and SDD, generate a complete Traceability Matrix.

For every requirement in the SRS (FR-XXX, NFR-XXX, IR-XXX, DR-XXX, CR-XXX):
- Identify the SDD design element(s) that implement it (DE-XXX).
- Specify the test case identifier(s) that will verify it (TC-XXX);
  if test cases have not yet been written, mark as PENDING.
- Set the implementation status to NOT STARTED.
- Flag any requirements with no identifiable design element as UNTRACED
  (indicating a gap in the SDD).
- Flag any design elements with no corresponding requirement as ORPHAN
  (indicating potential scope creep).

Output the matrix as a structured table.
```

---

*© 2025 Gordon Tulloch — Sunrise School Division. This paper may be reproduced for educational and non-commercial purposes with attribution.*
