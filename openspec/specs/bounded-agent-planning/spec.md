# Bounded Agent Planning Specification

## Purpose

Define task intent routing, explicit tool allowlisting, step bounds, and the fail-explicit optional LLM boundary for `RuleBasedPlanner` and `OptionalLLMService`.

## Requirements

### Requirement: Intent Routing and Bounded Allowlisted Plan
`RuleBasedPlanner` SHALL map operator queries to `RECEIPT`, `ISSUE`, or `CHECK` intents and construct a plan whose length is at most 8 steps and whose tools belong strictly to the 7-tool allowlist.

#### Scenario: Chinese outbound query routed to ISSUE plan
- **GIVEN** an operator submits query `出庫檢查`
- **WHEN** `RuleBasedPlanner.build_plan()` resolves the intent
- **THEN** the intent is `ISSUE`
- **AND** the generated plan contains 7 `PlanStep` entries all within `allowed_tools` (`ocr`, `parse_document`, `query_history`, `analyze_duplicate`, `query_inventory`, `analyze_inventory`, `evaluate_rules`)

### Requirement: Fail-Explicit Optional LLM Boundary
`OptionalLLMService` MUST default to `disabled` and MUST raise `NotImplementedError` if an external LLM provider is configured without an implemented adapter.

#### Scenario: Unimplemented external LLM provider configured
- **GIVEN** `LLM_PROVIDER` is set to a non-disabled provider with an `LLM_API_KEY`
- **WHEN** `OptionalLLMService.plan()` is invoked
- **THEN** it raises `NotImplementedError` rather than silently falling back or fabricating a plan
