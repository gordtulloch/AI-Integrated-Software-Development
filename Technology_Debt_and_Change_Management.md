# Specification Drift and the Debt Spiral: How Ineffective Change Management Drives Technology Debt Accumulation in AI-Integrated Software Development

**Gordon Tulloch**
Director of Information & Communications Technologies
Sunrise School Division

---

*Abstract* — Technology debt — the accumulated cost of deferred quality obligations in software systems — is among the most significant and least visible drains on organisational technology budgets. Empirical research consistently finds that technology debt consumes 20 to 40 percent of the total value of enterprise technology estates and diverts 10 to 20 percent of new product budgets to remediation rather than innovation. This paper argues that ineffective change management is not merely a contributing factor to technology debt accumulation but is its primary structural driver in post-deployment systems. In AI-integrated development environments governed by formal specification hierarchies, ineffective change management operates through five compounding pathways — specification drift, orphaned implementations, regression gaps, lost rationale, and deferred preventive maintenance — each of which contributes a distinct debt type while simultaneously degrading the organisation's capacity to use AI-assisted development productively. The paper maps these pathways to the established taxonomy of debt types (Kruchten, Nord & Ozkaya, 2012) and to Fowler's (2009) debt quadrant, demonstrating that change-management failures are the primary mechanism by which deliberate, prudent debt is transformed into inadvertent, reckless debt. A debt accumulation model is presented that characterises the non-linear compounding relationship between specification drift and development velocity. The paper concludes with a framework for debt-aware change management that integrates debt visibility, triage, and remediation into the Requirements Change Management process defined in Tulloch (2025b), and identifies the specific process controls that interrupt the debt spiral at its earliest stage.

**Keywords:** technology debt, technical debt, change management, specification drift, AI-integrated development, requirements debt, design debt, debt accumulation, debt remediation, software maintenance

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Technology Debt: Concepts, Taxonomy, and Scale](#2-technology-debt-concepts-taxonomy-and-scale)
3. [The Structural Link Between Change Management and Debt](#3-the-structural-link-between-change-management-and-debt)
4. [The Five Accumulation Pathways](#4-the-five-accumulation-pathways)
5. [The Debt Spiral: Compounding and Non-Linearity](#5-the-debt-spiral-compounding-and-non-linearity)
6. [The AI-Specific Amplification Effect](#6-the-ai-specific-amplification-effect)
7. [Classifying Change-Induced Debt in the Fowler Quadrant](#7-classifying-change-induced-debt-in-the-fowler-quadrant)
8. [Debt-Aware Change Management](#8-debt-aware-change-management)
9. [Debt Remediation: Restoring Specification Integrity](#9-debt-remediation-restoring-specification-integrity)
10. [Discussion](#10-discussion)
11. [Conclusion](#11-conclusion)
12. [References](#12-references)

---

## 1. Introduction

Ward Cunningham introduced the technical debt metaphor in 1992 to explain to non-technical stakeholders why development teams needed to allocate time for refactoring. His original formulation was precise: shipping first-time code is like going into debt. A little debt speeds development so long as it is paid back promptly with a rewrite. The danger occurs when the debt is not repaid. In the three decades since, the metaphor has been refined, expanded, and subjected to increasing empirical scrutiny. The core insight — that deferred quality obligations compound into future costs — has been confirmed at scale. McKinsey's research across 220 organisations found that technology debt amounts to 20 to 40 percent of the total value of enterprise technology estates before depreciation, and that companies reporting the highest debt burdens consistently underperform their peers on revenue growth, innovation output, and the ability to complete modernisation initiatives (McKinsey, 2020; 2022).

What the literature has been slower to characterise with precision is the specific mechanism by which debt accumulates. The conventional account treats debt as the result of time-pressured development decisions: cutting corners to meet deadlines, skipping tests, deferring documentation. This account is accurate but incomplete. It describes the *origin* of individual debt items but not the *structural process* by which those items compound into a system-wide liability that eventually constrains every development activity.

This paper proposes that the structural driver of technology debt accumulation in post-deployment systems is not development-time shortcutting — which is bounded by the scope of each development cycle — but *ineffective change management*, which operates continuously throughout the system's operational lifetime and compounds without bound. Every change to a deployed system that is not managed through a disciplined process connecting the change to the specification hierarchy generates debt across multiple debt types simultaneously. The accumulation is not linear: as debt accumulates, it raises the cost of subsequent changes, which in turn increases the time pressure to bypass change management discipline, which generates more debt. This is the debt spiral.

In AI-integrated development environments — those governed by the specification-driven workflow described in Tulloch (2025a) — this dynamic has an additional amplifying dimension. The specification hierarchy that was the primary quality assurance mechanism during development becomes increasingly unreliable as a basis for AI-assisted change implementation as specification drift accumulates. The productivity gains from AI-assisted development are progressively eroded, not because the AI tools have become less capable, but because the specifications they operate against have become inaccurate representations of the real system.

This paper makes the following contributions:

1. A structural account of the relationship between change management process quality and technology debt accumulation, framed in terms of the established debt taxonomy.
2. A characterisation of five compounding accumulation pathways through which ineffective change management generates multi-type debt simultaneously.
3. An analysis of the non-linear debt spiral dynamic and the specific threshold at which debt transitions from manageable to constraining.
4. A description of the AI-specific amplification effect: the mechanism by which specification drift specifically degrades AI-assisted development capacity.
5. A framework for debt-aware change management that integrates debt visibility and triage into the Requirements Change Management process.

---

## 2. Technology Debt: Concepts, Taxonomy, and Scale

### 2.1 The Financial Metaphor and Its Limits

Cunningham's original metaphor describes debt as the trade-off between short-term delivery speed and long-term maintenance cost, with interest accruing as additional effort that could have been avoided if the initial shortcuts had not been taken. The metaphor is powerful for communicating the concept to business stakeholders precisely because it maps to familiar financial reasoning: principal (the deferred work), interest (the ongoing overhead), and the risk of bankruptcy (a system so degraded it cannot be economically maintained or extended).

The metaphor has, however, well-recognised limitations. Financial debt scales linearly: a business carrying 30 percent more debt than its peers faces a proportionally higher interest burden. Technology debt does not scale linearly. As Fowler (2009) and subsequent empirical researchers have noted, the drag imposed by accumulated debt grows faster than the debt itself once certain architectural thresholds are crossed. An engineering team whose core domain model has become entangled with infrastructure concerns through accumulated undocumented changes does not face a proportionally higher drag — it faces a qualitative change in the nature of development work, in which every change requires touching multiple interlocked systems and the cost per feature grows with something closer to superlinear complexity (Java Code Geeks, 2026). This non-linearity is the defining property of what this paper calls the *debt spiral*, described in Section 5.

### 2.2 The Debt Taxonomy

Kruchten, Nord, and Ozkaya (2012) provide the most widely adopted taxonomy of technology debt types, identifying distinct categories corresponding to different stages and artifacts of the software development lifecycle:

- **Code debt:** Suboptimal implementation — overly complex methods, poor naming, duplicated logic, insufficient comments. The most visible and most commonly discussed form.
- **Design debt:** Architectural and structural problems — inappropriate design patterns, tight coupling, violated separation of concerns, missing abstractions. Often invisible in individual files but apparent at system level.
- **Test debt:** Insufficient, incorrect, or incomplete test coverage — missing test cases, tests that test implementation rather than requirements, inadequate regression scope.
- **Documentation debt:** Missing, inaccurate, or outdated documentation — including specification documents, API documentation, deployment guides, and rationale records.
- **Requirements debt:** Incomplete, inconsistent, or unverifiable requirements — specifications that do not accurately describe the system's intended or actual behaviour.

The literature also recognises *architectural debt* (a severe form of design debt involving fundamental structural violations) and *process debt* (inadequate or absent development and maintenance processes). All of these types interact; debt in one category typically generates secondary debt in others, which is the mechanism underlying the compounding dynamics described in Section 5.

### 2.3 The Fowler Debt Quadrant

Fowler's (2009) debt quadrant classifies debt not by type but by *origin*: how it was incurred and whether it was incurred knowingly. The two axes are deliberate versus inadvertent (did the team know they were taking on debt?) and reckless versus prudent (was the decision made thoughtfully?). The resulting quadrant identifies four categories:

- **Deliberate and prudent:** "We know we are taking on debt and have a plan to repay it." The least harmful form; the debt is visible, bounded, and managed.
- **Deliberate and reckless:** "We know this will cause problems but we are shipping anyway." Harmful; generates known liabilities without a repayment plan.
- **Inadvertent and prudent:** "We now realise we should have done it differently." Discovered after the fact by a team that learns and corrects.
- **Inadvertent and reckless:** "We didn't know what we were doing." The most harmful form; the debt is invisible, unbounded, and generates further debt because the team cannot recognise when it is accumulating more.

The debt quadrant is important for this paper because one of the defining consequences of ineffective change management is the systematic transformation of deliberate debt into inadvertent debt. When changes are not documented, design decisions that were originally understood and intentional become opaque. What began as a deliberate, prudent shortcut with a documented rationale transforms, through the loss of that rationale, into an inadvertent, reckless constraint. This transformation is the mechanism by which manageable debt becomes debt that constrains the organisation's entire development capacity.

### 2.4 The Economic Scale

The economic scale of technology debt is substantial. McKinsey's survey research found that CIOs estimate technology debt amounts to 20 to 40 percent of the value of their entire technology estate before depreciation, and that 10 to 20 percent of the technology budget dedicated to new products is diverted to resolving issues related to technology debt (McKinsey, 2020). The same research found that companies with lower technology debt consistently outperform peers on revenue growth, that companies in the bottom 20th percentile for technology debt severity are 40 percent more likely to have incomplete or cancelled IT modernisations, and that actively managing technology debt can free engineers to spend up to 50 percent more of their time on value-generating work (McKinsey, 2022). These figures establish the economic significance of effective debt management beyond any reasonable doubt. What they do not establish is the mechanism of accumulation — the subject of this paper.

---

## 3. The Structural Link Between Change Management and Debt

### 3.1 Development-Time Debt versus Operational Debt

Conventional treatments of technology debt focus primarily on *development-time* debt: shortcuts taken during initial development under deadline pressure, inadequate testing due to resource constraints, architectural compromises made to meet delivery schedules. This is a real and important source of debt, but it is structurally bounded. Development-time debt is incurred within the scope of a development project that eventually completes. Its accumulation rate is limited by the pace of development; it cannot exceed the total development effort.

*Operational debt* — debt accumulated through post-deployment change management failures — is structurally unbounded. A deployed system that receives changes will accumulate operational debt for as long as it operates, at a rate determined by the quality of its change management processes. For systems with long operational lifetimes, operational debt typically dominates development-time debt within the first few years of deployment, regardless of how well the initial system was built. This is why the Lientz and Swanson (1980) finding — that over half of software maintenance effort is devoted to perfective maintenance (requirements evolution) rather than corrective work — has proven so durable across four decades of changing development practices. The driver of that maintenance burden is not the initial quality of the code; it is the quality of the process that manages requirements change over the system's operational lifetime.

### 3.2 The Specification Hierarchy as the Debt Containment Mechanism

The specification-driven AI development workflow described in Tulloch (2025a) establishes a specification hierarchy — PSD, SRS, SDD, TM, test suite, codebase — whose internal consistency is the primary quality assurance mechanism of the system. This hierarchy is not merely a documentation convenience; it is the structural mechanism that prevents operational debt from accumulating by providing a traceable, verifiable record of every design decision and its relationship to every requirement and every test.

When the specification hierarchy is maintained through effective change management, a change to any element of the system is immediately reflected in all related elements. The debt principal remains at zero because no obligations are deferred. When the specification hierarchy is not maintained — when changes are implemented in code without corresponding updates to specifications, tests, or documentation — each unmanaged change creates a small increment of debt across multiple debt types simultaneously. The specification hierarchy's value as a debt containment mechanism is precisely its completeness; a hierarchy with gaps provides dramatically weaker containment than a complete one.

### 3.3 The Asymmetry of Accumulation and Remediation

Technology debt accumulates incrementally and largely invisibly; its remediation is discontinuous and expensive. The asymmetry is fundamental to understanding why rational actors systematically under-invest in change management discipline: each individual undocumented change costs very little in the moment — a few minutes not spent updating a TM entry, a hotfix deployed without a specification update. The marginal cost of skipping the documentation step is negligible and immediate. The marginal cost of that decision is paid diffusely, in the future, across all subsequent development activities, in amounts that cannot be attributed to any specific prior decision.

There is a well-established analogue in the costs of software requirements defects: Boehm (1981) demonstrated that defects introduced during requirements specification are orders of magnitude more expensive to correct after deployment than during the specification phase. The same asymmetry applies to the requirements and specification documents themselves: failing to update a specification at the time of a change costs minutes; restoring the accuracy of a specification that has drifted through dozens of undocumented changes costs days or weeks of forensic analysis against the running system.

---

## 4. The Five Accumulation Pathways

Ineffective change management generates technology debt through five distinct but interacting pathways. Each pathway contributes a primary debt type while generating secondary effects in others. Together, they constitute the complete mechanism by which change management failures translate into the debt burden characterised in Section 2.4.

### 4.1 Pathway 1 — Specification Drift as Requirements Debt

**Mechanism:** When a change is implemented in code without corresponding updates to the PSD, SRS, or SDD, those documents progressively describe a system that no longer exists. The divergence between documented and actual system behaviour is *specification drift*. Each unmanaged change adds a small increment to the drift, and the increments compound.

**Debt type generated:** Requirements debt — the primary and most consequential type generated by this pathway. The SRS ceases to be an accurate specification of the system's actual requirements; it becomes a record of what the requirements *were* at some point in the past, progressively less useful as a planning or analysis instrument.

**Secondary debt:** Design debt (from undocumented design decisions), documentation debt (from inaccurate specifications), and process debt (from the erosion of the specification-as-single-source-of-truth principle).

**Change management failure that causes it:** Failing to update upstream specification documents as part of change implementation — the most common and most consequential change management shortcut.

**Specific cost:** Every subsequent change must be analysed against a misrepresentation of the current system. The impact analysis is unreliable because the TM traces to requirements that may no longer accurately describe the design elements and code. Design decisions must be reconstructed by reading the code rather than consulting the SDD. The cost of each subsequent change is elevated by the amount of pre-change forensic work required to establish the true current state.

### 4.2 Pathway 2 — Orphaned Implementations as Design Debt

**Mechanism:** Every change that modifies the codebase without a corresponding SDD update creates a design element with no documented rationale and no traceable requirement. Over time, these orphaned implementations accumulate into what practitioners recognise as *accidental architecture*: a system whose actual structure is substantially different from its documented structure, shaped by accumulated undocumented workarounds rather than intentional design.

**Debt type generated:** Design debt — the accumulated structural degradation of the system's architecture through undocumented changes. Architectural debt in its most severe form, when foundational structural assumptions have been violated by accumulated changes.

**Secondary debt:** Requirements debt (orphaned implementations often represent requirements that were never formally recorded), test debt (no test cases exist for undocumented behaviour).

**Change management failure that causes it:** Bypassing SDD updates during change implementation, particularly in corrective changes made under urgency pressure.

**Specific cost:** As Jayatilleke and Lai (2018) note in their systematic review of requirements change management, the consequences of a change ripple through the system in ways that cannot be determined without accurate design documentation. Orphaned implementations are the primary source of unexpected integration failures in post-deployment systems: components that have been changed without documented interface updates fail when other components are subsequently changed in ways that assume the original interface. The cost is paid as integration debugging effort that could have been avoided had the SDD been maintained.

### 4.3 Pathway 3 — Regression Gaps as Test Debt

**Mechanism:** When change impact analysis is incomplete or bypassed, the regression test scope for a given change is underspecified. Tests that should have been updated to reflect the changed behaviour are not updated; tests that should have been added to cover new behaviour are not added; tests that should have been re-executed to verify unchanged behaviour are not re-executed. The result is a test suite that appears to provide coverage but whose actual defect-detection capability has declined because its content no longer accurately represents the system's requirements.

**Debt type generated:** Test debt — the accumulated gap between the test suite's nominal coverage and its actual verification capability. This is the most dangerous form of debt from a reliability perspective because it is actively misleading: a test suite that passes does not mean the system is correct; it means the system is consistent with the subset of its historical behaviour that the test suite still accurately represents.

**Secondary debt:** Requirements debt (the unenforced requirements are functionally equivalent to unverified requirements), code debt (defects that should have been caught propagate into the codebase unchallenged).

**Change management failure that causes it:** Inadequate impact analysis that fails to identify the full regression scope, or time-pressured decisions to run a reduced regression test suite without documenting the reduction.

**Specific cost:** Defects that should have been caught during change verification reach production, where they generate corrective change requests. Those corrective changes, implemented under higher urgency pressure, are more likely to bypass the same change management disciplines, generating further test debt. The escalating frequency of production defects is a diagnostic indicator of accumulated test debt.

### 4.4 Pathway 4 — Lost Rationale as Documentation Debt

**Mechanism:** Every change implemented without a Change Log entry removes knowledge from the system. The rationale for design decisions — which constraints were regulatory, which were integration requirements, which were performance trade-offs — is available only in the memories of the individuals who made those decisions. As those individuals leave the project, the team loses the ability to distinguish intentional design from accidental constraint, load-bearing requirements from arbitrary choices.

**Debt type generated:** Documentation debt — specifically the loss of design rationale that is the most expensive form of documentation debt to remediate, because it cannot be recovered from the code itself; it must be reconstructed from memory, from stakeholder interviews, or from analysis of system behaviour against external requirements.

**Secondary debt:** Requirements debt (requirements that cannot be explained cannot be reliably revised), process debt (teams that cannot understand existing design make conservative changes that preserve unnecessary constraints, slowing development).

**Change management failure that causes it:** Treating the Change Log as optional overhead rather than as a mandatory process step, particularly for changes characterised as "small" or "obvious."

**Specific cost:** Future developers — and future AI generation sessions — cannot determine why the system is designed as it is. As McKinsey (2022) characterises it, technology debt is "like dark matter: you know it exists, you can infer its impact, but you can't see or measure it." Documentation debt is the mechanism by which system knowledge becomes dark matter: present in the system's behaviour, invisible to its maintainers, inferable only from its effects.

### 4.5 Pathway 5 — Deferred Preventive Maintenance as Code and Architectural Debt

**Mechanism:** When the change management process overhead is perceived as disproportionate to the effort of small structural improvements — refactoring, dependency updates, security hardening, complexity reduction — teams defer those improvements indefinitely. In AI-generated codebases, this is particularly consequential because the structural quality of AI-generated code already tends toward higher cyclomatic complexity and lower modularity than human-written equivalents (Sonar, 2025; ScienceDirect, 2026). Without a lightweight preventive change pathway, every corrective and adaptive change adds more complexity on top of a foundation that is already structurally weaker than a human-designed system would typically be.

**Debt type generated:** Code debt and architectural debt — the accumulated structural degradation of implementation quality through deferred refactoring and deferred security remediation.

**Secondary debt:** Test debt (complex code is harder to test), documentation debt (complex code is harder to document accurately).

**Change management failure that causes it:** Absence of a defined lightweight preventive change pathway; change management overhead that is disproportionate to the effort of preventive work.

**Specific cost:** Cyclomatic complexity above certain thresholds is empirically associated with higher defect rates (McCabe, 1976) and lower test coverage achievement. Deferred security remediation is associated with vulnerability accumulation that is discovered reactively under the highest possible urgency pressure, generating emergency corrective changes that are the most likely to bypass documentation requirements. The compound cost is a codebase that becomes progressively more expensive to change, test, and understand with each deployment cycle.

---

## 5. The Debt Spiral: Compounding and Non-Linearity

### 5.1 The Compounding Mechanism

The five accumulation pathways do not operate independently. Each pathway generates conditions that accelerate the others, creating a self-reinforcing feedback loop that is the defining dynamic of the debt spiral.

The sequence is characteristic. Specification drift (Pathway 1) makes impact analysis less reliable, because the TM traces to requirements that no longer accurately represent the design. Unreliable impact analysis leads to inadequate regression scope definition (Pathway 3), because the analyst cannot correctly determine which components are affected by a given change. Growing test debt means that defects pass through change verification and reach production, generating corrective change requests. Corrective changes, implemented under urgency pressure, are the changes most likely to bypass documentation requirements (Pathway 4) and SDD updates (Pathway 2). Emergency hotfixes in particular are the primary source of orphaned implementations in most production systems. As orphaned implementations accumulate, the structural quality of the codebase degrades (Pathway 5), making each subsequent change more complex and more error-prone. Greater change complexity increases the time pressure to skip documentation — which accelerates specification drift, closing the spiral.

Importantly, each iteration of this loop elevates the *baseline cost* of every future change. The spiral does not merely maintain the debt level; it grows it. And it does so not through exceptional events but through the accumulation of individually small process shortcuts that are each, individually, rational responses to time pressure.

### 5.2 The Non-Linear Transition

The most important property of the debt spiral is that its cost is not linear with debt magnitude. At low levels of accumulated debt, the impact on development velocity is approximately proportional — a small drag on each change, annoying but manageable. This is the regime that the financial metaphor describes well: a known interest payment on a manageable principal.

At higher levels of accumulated debt, the relationship becomes superlinear. Changes that should affect a single component begin to require modifications across multiple entangled components because architectural debt has eliminated the clean separation of concerns. Tests that should verify a specific requirement must be extensively updated because test debt has caused the test suite to conflate requirements in ways that make targeted testing impossible. Documentation that should clearly describe a component's interface must be reconstructed from the code because documentation debt has left it inaccurate.

The transition point — what Fowler (2009) calls the "design payoff line" — is the threshold beyond which every change, regardless of its intrinsic scope, requires addressing accumulated debt before it can be safely implemented. Teams that have crossed this threshold experience it as a qualitative change in the nature of their development work: changes that used to take hours take days; defects that used to be rare become routine; the effort required to understand the system before making any change becomes the dominant component of every development cycle. This is the point at which McKinsey's observation that teams may spend 75 percent of engineering time paying the "tech debt tax" rather than building new value becomes operationally real (McKinsey, 2022).

### 5.3 Debt Across the Maintenance Lifecycle

The debt spiral is not a sudden onset — it develops over time, with the rate of accumulation determined by the quality of change management processes. A useful characterisation of the lifecycle is in three phases:

**Manageable debt phase:** Individual debt items are visible, bounded, and documented. The specification hierarchy is substantially accurate. Impact analyses are reliable. Development velocity is approximately as designed. Remediation of individual debt items is feasible within normal development cycles.

**Degrading debt phase:** Specification drift has accumulated sufficiently to make impact analyses unreliable. Test debt has grown to the point where regression failures are discovered post-deployment rather than pre-deployment. Architectural drift has begun to make "clean" changes — those that affect only intended components — increasingly rare. Development velocity has declined measurably, but the cause is diffuse and hard to attribute.

**Critical debt phase:** The specification hierarchy is so far from the actual system state that it provides limited guidance for new development. The test suite provides false assurance rather than genuine verification. Every change requires extensive forensic analysis of the codebase before design decisions can be made. Development velocity has collapsed to a fraction of its original rate. New team members require months of orientation to become productive. The organisation considers replacing the system rather than continuing to maintain it — and often finds that debt has accumulated in the replacement project's requirements and design documents before code has been written.

---

## 6. The AI-Specific Amplification Effect

The debt spiral described in Section 5 operates in all software systems. In AI-integrated development environments, it has an additional amplifying dimension that is specific to the specification-driven workflow and that significantly raises the cost of specification drift.

### 6.1 Specification Quality as AI Capability

In the AI-integrated development workflow, the specification hierarchy is not merely documentation — it is the primary operational context for AI generation. The quality of every AI generation activity — requirements updates, design revisions, code generation, test generation, documentation updates — is bounded by the accuracy of the specification it operates against. This is the specification-sensitivity principle established in Tulloch (2025a): AI tools amplify both the precision of well-formed specifications and the imprecision of poorly formed ones.

When the specification hierarchy is maintained accurately through effective change management, the AI's effectiveness as a development tool compounds over the system's lifetime: each AI-assisted change builds on a richer, more accurate specification context, producing better-quality output with less iteration. When the specification hierarchy drifts from the actual system, the AI's effectiveness degrades: it generates code that is coherent with the documented system but inconsistent with the actual one, introducing new inconsistencies on top of existing debt.

### 6.2 The Dual Debt Mechanism

In AI-integrated development, specification drift generates debt through two mechanisms simultaneously. The standard mechanism — which affects all software systems — is that future developers must work around the inaccurate specification, doing additional forensic analysis to establish the true current state before implementing each change. The AI-specific mechanism is that AI-assisted changes generate *specification-consistent but system-inconsistent* output: code that is correct relative to the documented requirements but incorrect relative to the actual system behaviour.

This second mechanism is particularly insidious because the generated code will typically pass tests — the tests were also generated against the documented specification and share its inaccuracies. The debt is invisible until integration testing reveals that new components do not interact correctly with the actual system. At that point, the team faces a choice between a time-consuming specification reconciliation effort (addressing the debt principal) and a targeted code fix that treats the symptom without addressing the underlying specification inaccuracy (adding more debt). Under time pressure, the targeted fix is rational in the short term and systematically irrational at the lifecycle level — precisely the dynamic that Cunningham's original metaphor was designed to make visible.

### 6.3 The Productivity Loss Trajectory

The productivity trajectory of an AI-integrated development team is shaped by the compound interaction of AI capability and specification accuracy. In the early life of a system with well-maintained specifications, AI-assisted development productivity grows as the specification becomes richer with each documented change — more context, more examples, more established patterns. As specification drift accumulates, this trajectory reverses: the AI's output becomes less reliable, more iteration is required to correct generation errors, and the specification context must be supplemented with increasing amounts of inline explanation in prompts to compensate for its inaccuracies.

The practical consequence is that the productivity benefits of AI-assisted development are front-loaded in systems with ineffective change management: they are realised primarily during initial development and the early deployment period when the specification is still substantially accurate, and decline as specification drift accumulates. Teams that observe declining AI-assisted productivity and attribute it to the limitations of AI tools are often observing the consequences of their own change management discipline rather than a technology ceiling.

---

## 7. Classifying Change-Induced Debt in the Fowler Quadrant

A productive application of the Fowler debt quadrant to the change-management context reveals a pattern that is not immediately obvious from the quadrant's original formulation: ineffective change management does not merely generate debt in specific quadrants — it *migrates* debt from less harmful to more harmful quadrants over time.

### 7.1 The Migration Pattern

Consider a hotfix applied under urgency pressure, where the team is aware they are bypassing the specification update and consciously accepts that as a trade-off. At the moment of the hotfix, this is *deliberate, prudent* debt in Fowler's terminology: the team knows they are taking on debt and plans to address it in the next planned release cycle. This is the most manageable form of debt.

If the planned repayment — the specification update — is never made, what began as deliberate and prudent debt transitions to *deliberate and reckless* debt: the obligation was incurred knowingly and the repayment was deferred indefinitely. If subsequent team members are not aware the hotfix was undocumented, the debt transitions again to *inadvertent* debt: the next developer to work on the affected component is not aware of the constraint introduced by the hotfix, cannot understand why the code behaves as it does, and risks introducing a change that violates the constraint without knowing it exists.

The final state — *inadvertent and reckless* debt — is reached when the constraint introduced by the undocumented change is no longer discoverable from any written record and is too distant in time for any team member to recall. At this point the debt is maximum: invisible, unconstrained in its effects, generating further debt because the team cannot recognise when they are accumulating more.

### 7.2 The Change Log as the Debt Quadrant Anchor

The Change Log entry is the specific mechanism that anchors debt in the most manageable quadrant of the Fowler matrix. A documented change — even an undocumented-in-specification emergency fix — that is recorded in the Change Log with its rationale, its acknowledged technical debt implications, and the date it was incurred remains deliberate debt. It can be found, assessed, and repaid. An undocumented change is invisible debt from the moment it is made.

This reframing has an important implication for the design of change management processes: the Change Log entry is not the most important process step for managing well-executed changes — it is the most important process step for managing poorly-executed ones. For changes that update all required specification documents on the correct timeline, the Change Log is a useful record but not a critical intervention. For changes that cannot update all required specifications due to urgency, resource constraints, or complexity, the Change Log entry that records the shortcut, its rationale, and the repayment obligation is the mechanism that prevents the debt from becoming inadvertent.

---

## 8. Debt-Aware Change Management

### 8.1 Integrating Debt Visibility into the RCM Process

The Requirements Change Management process defined in Tulloch (2025b) provides the structural framework for managing changes in AI-integrated development environments. Rendering that process *debt-aware* requires the addition of three specific steps that make technology debt visible, assessed, and tracked at each stage of the change lifecycle.

**At Stage 1 (Change Documentation):** The Change Request Form should include a *Debt Implication* field that captures, for each change, whether its implementation will require any departure from the full specification hierarchy update process (due to urgency, resource constraints, or complexity). If it will, the specific debt being incurred, the planned repayment timeline, and the repayment obligation owner must be recorded at the time the CRF is submitted — not retrospectively. This is the mechanism that transforms deliberate debt into visible, managed debt rather than allowing it to become inadvertent debt through the passage of time.

**At Stage 2 (Impact Analysis):** The Impact Analysis Report should include a *Debt Surface* assessment: an identification of existing debt items in the areas affected by the proposed change that may complicate its implementation. Changes made to areas with high existing debt carry higher risk and typically require more extensive remediation work as part of their implementation. The Debt Surface assessment ensures this risk is quantified before the change is authorised, preventing the common pattern of scope expansion that occurs when teams discover mid-implementation that debt remediation is required but was not planned for.

**At Stage 4 (Verification and Deployment):** The post-deployment monitoring period described in Tulloch (2025b, §8.4) should include a scheduled debt reconciliation step: within a defined period after deployment (typically the next planned maintenance window), any specification documentation deferred due to urgency is completed, any debt incurred is recorded in the formal debt register, and the TM is updated to reflect the actual post-deployment state of all affected artifacts.

### 8.2 The Debt Register

The debt register is a structured record of all known, intentionally-incurred technology debt items. For each item, it records the debt type (from the Kruchten et al. taxonomy), the debt quadrant (from Fowler's framework), the date incurred, the CRF that generated it, the estimated remediation cost, the planned remediation date, and the current status. The debt register is a living document maintained alongside the specification hierarchy and reviewed at each CCB meeting.

The debt register serves a critical governance function: it makes the total accumulated debt visible to decision-makers who must prioritise between new development work and debt remediation. Without a debt register, the cost of accumulated debt is invisible in planning cycles, and the rational short-term decision (prioritise new features over debt remediation) consistently dominates, causing the debt spiral to continue unchecked until it reaches the critical phase described in Section 5.3.

### 8.3 The Debt Budget

Effective debt-aware change management requires an explicit debt budget: a defined, scheduled allocation of development capacity to debt remediation activities. The McKinsey evidence suggests that organisations that actively manage technology debt free engineers to spend up to 50 percent more time on value-generating work (McKinsey, 2022). This finding implies that the return on investment for debt remediation effort is substantially positive at most debt levels, and that the common practice of deferring all debt remediation until it becomes critical is economically irrational.

A practical debt budget allocates a defined percentage of each development cycle — typically 10 to 20 percent — to preventive maintenance and debt remediation activities. This allocation should be treated as a fixed overhead of sustainable development operations, not as discretionary investment that can be deferred under delivery pressure. The change management process should include a mechanism for selecting which debt items are addressed in each cycle, prioritising by the combination of remediation cost, risk reduction benefit, and debt quadrant severity.

---

## 9. Debt Remediation: Restoring Specification Integrity

### 9.1 The Forensic Specification Audit

When a system has accumulated significant specification drift through ineffective change management, the primary remediation activity is a forensic specification audit: a systematic comparison of the documented specification hierarchy against the actual deployed system to identify and document all discrepancies.

The forensic audit proceeds from the bottom of the specification hierarchy upward, using the running code as the ground truth:

1. **Code inventory:** Document all components, interfaces, data schemas, and behaviours present in the deployed system.
2. **TM reconciliation:** For each code component, identify the corresponding TM entry. Components without TM entries are orphaned implementations; document them as new requirement candidates.
3. **SDD reconciliation:** Compare the documented SDD design elements against the actual code structure. Document all discrepancies as design debt items.
4. **SRS reconciliation:** For each identified discrepancy between the SDD and the code, determine whether the discrepancy represents an undocumented requirement. If so, draft a new SRS requirement and submit it for formal review and acceptance.
5. **PSD consistency check:** Review all new or revised requirements against the PSD objectives. Requirements that cannot be derived from the PSD represent either scope creep that was absorbed without governance review, or PSD updates that were never made. Both require resolution.

The forensic specification audit is expensive — it is precisely the cost of not maintaining the specification hierarchy through effective change management. For systems with significant accumulated drift, the audit may represent weeks or months of effort. This cost is the concrete, quantifiable expression of the debt principal that ineffective change management has accumulated.

### 9.2 Incremental Remediation Strategy

For systems with large accumulated debt, a full forensic audit may not be feasible as a single project. An incremental remediation strategy addresses debt in bounded areas, prioritised by development activity:

- **Activity-triggered remediation:** Before implementing any new change in an area with known specification debt, require that the specification for that area be brought current as a prerequisite. This ensures that the areas with the highest change frequency — which are also typically the areas where specification accuracy matters most — are remediated first.
- **Risk-triggered remediation:** Prioritise reconciliation of areas where specification inaccuracy poses the greatest risk — security-related components, components with complex external interfaces, and components that form the architectural core of the system.
- **Capacity-triggered remediation:** Allocate the debt budget described in Section 8.3 to systematic remediation of the lowest-hanging debt items — those with the lowest remediation cost relative to their risk reduction benefit.

### 9.3 The Role of AI in Debt Remediation

AI-assisted development tools can contribute to debt remediation, but their application requires care. The AI can be instructed to compare a described specification against a provided codebase and identify discrepancies — a form of specification-code consistency checking that automates part of the forensic audit work. However, consistent with the verification limitations identified by Endres et al. (2025) and noted in Tulloch (2025a), AI-generated discrepancy reports are preliminary assessments requiring human expert review, not authoritative audit findings.

The more productive application of AI in debt remediation is *specification reconstruction*: once a discrepancy has been identified and understood by a human reviewer, the AI can generate the required specification update — new SRS requirement, revised SDD design element, updated TM entry — as a draft subject to human approval. This is the same generation-plus-review pattern that characterises the initial development workflow; it is equally applicable and equally reliant on human authority for final decisions.

---

## 10. Discussion

### 10.1 Implications for Technology Governance

The framework presented in this paper has significant implications for how technology governance should approach the change management function. Conventional technology governance frameworks treat change management primarily as a risk control — a process for preventing unauthorised changes and ensuring tested, approved changes reach production safely. This is necessary but insufficient. Change management is also the primary debt management mechanism in any post-deployment system, and governance frameworks that evaluate its effectiveness solely on change success rates and rollback frequency are missing its most important quality dimension.

A governance framework informed by this paper would include debt accumulation rate as a primary metric for evaluating change management process effectiveness. A change management process that delivers a high change success rate while allowing significant specification drift is not an effective change management process — it is a process that is trading future development capacity for current operational stability. The debt is being accumulated invisibly, outside the metrics that governance uses to evaluate system health.

### 10.2 Implications for Resource Planning

The debt budget concept introduced in Section 8.3 has direct implications for technology resource planning. If McKinsey's finding that CIOs estimate 10 to 20 percent of the budget dedicated to new products is diverted to resolving technology debt is accurate, then organisations that do not explicitly budget for debt remediation are not avoiding that cost — they are paying it reactively, at a higher effective rate, in the form of delayed new development, increased defect rates, and emergency remediation costs. The economically rational approach is to budget preventive debt management as an explicit operational overhead, analogous to the way facilities management budgets preventive maintenance rather than waiting for equipment failures.

### 10.3 Limitations

The accumulation model and pathways described in this paper are analytical frameworks derived from the literature and from the logical structure of the specification-driven workflow. They have not been empirically validated through controlled measurement of debt accumulation rates under different change management process quality levels. Empirical validation — measuring specification drift rates, debt type distributions, and development velocity trajectories across organisations with varying change management maturity — would significantly strengthen the causal claims made here and is an important direction for future research.

Additionally, the five accumulation pathways are characterised qualitatively. Future work should develop quantitative metrics for each pathway — specification drift rate, orphan implementation frequency, regression coverage decay rate, documentation completeness score — that would enable the debt accumulation model to be applied predictively rather than diagnostically.

---

## 11. Conclusion

Technology debt is not primarily caused by shortcuts taken during initial development. It is primarily caused by the failure to maintain specification integrity through the post-deployment change management process. In AI-integrated development environments, this failure is doubly consequential: it accumulates the same multi-type debt that afflicts all software systems, and it additionally degrades the accuracy of the specification context on which AI-assisted development depends, eroding the productivity benefits of the AI investment over time.

The debt spiral — the self-reinforcing feedback loop through which specification drift, orphaned implementations, regression gaps, lost rationale, and deferred preventive maintenance compound into progressively higher change costs — is not an inevitable property of deployed software systems. It is the predictable consequence of a specific set of change management failures that are identifiable, preventable, and, once accumulated, remediable through systematic forensic specification auditing.

The financial metaphor that Cunningham introduced in 1992 remains the clearest way to communicate this dynamic to non-technical stakeholders: debt incurred without a repayment plan accumulates interest that eventually consumes the organisation's entire development capacity. The repayment plan, in the context of AI-integrated development, is effective change management: the discipline of maintaining the specification hierarchy's accuracy through every post-deployment change, treating that maintenance not as optional overhead but as the mechanism by which the organisation preserves its ability to develop, extend, and improve its systems over their operational lifetime.

---

## 12. References

Avgeriou, P., Kruchten, P., Ozkaya, I., & Seaman, C. (2016). Managing technical debt in software engineering. *Dagstuhl Reports, 6*(4), 110–138.

Boehm, B. W. (1981). *Software engineering economics.* Prentice-Hall.

Cunningham, W. (1992). The WyCash portfolio management system. *Addendum to the Proceedings of OOPSLA 1992*, 29–30.

Endres, M., Chong, K., Bhatt, N., & Abdelfattah, A. S. (2025). Uncovering systematic failures of LLMs in verifying code against natural language specifications. *arXiv:2502.11513*.

Fowler, M. (2009). *Technical debt quadrant.* Martin Fowler's Bliki. https://martinfowler.com/bliki/TechnicalDebtQuadrant.html

GitClear. (2024). *Coding on Copilot: 2023 data suggests downward pressure on code quality.* GitClear Research.

Java Code Geeks. (2026). The economics of technical debt: Why teams rationally choose to accumulate it. https://www.javacodegeeks.com

Jayatilleke, S., & Lai, R. (2018). A systematic review of requirements change management. *Information and Software Technology, 93*, 163–185.

Jha, N., & Babajide Mustapha, B. (2025). LLM-driven cost-effective requirements change impact analysis. *arXiv:2511.00262*.

Kruchten, P., Nord, R. L., & Ozkaya, I. (2012). Technical debt: From metaphor to theory and practice. *IEEE Software, 29*(6), 18–21.

Lientz, B. P., & Swanson, E. B. (1980). *Software maintenance management: A study of the maintenance of computer application software in 487 data processing organizations.* Addison-Wesley.

McCabe, T. J. (1976). A complexity measure. *IEEE Transactions on Software Engineering, 2*(4), 308–320.

McKinsey Digital. (2020). Tech debt: Reclaiming tech equity. McKinsey & Company.

McKinsey Digital. (2022). Demystifying digital dark matter: A new standard to tame technical debt. McKinsey & Company.

McKinsey Digital. (2023). Breaking technical debt's vicious cycle to modernize your business. McKinsey & Company.

Nord, R., & Ozkaya, I. (2022). *10 years of research in technical debt and an agenda for the future.* Carnegie Mellon Software Engineering Institute.

ScienceDirect. (2026). Quality assurance of LLM-generated code: Addressing non-functional quality characteristics. *Journal of Systems and Software.*

Sonar. (2025). *The inevitable rise of poor code quality in AI-accelerated codebases.* SonarSource.

Tom, E., Aurum, A., & Vidgen, R. (2013). An exploration of technical debt. *Journal of Systems and Software, 86*(6), 1498–1516.

Tulloch, G. (2025a). AI-integrated software development: A specification-driven framework for AI-assisted code generation. Sunrise School Division.

Tulloch, G. (2025b). Managing requirements change in AI-integrated software development: A process framework for post-generation change documentation, integration, implementation, and deployment. Sunrise School Division.

---

*© 2025 Gordon Tulloch — Sunrise School Division. This paper may be reproduced for educational and non-commercial purposes with attribution.*
