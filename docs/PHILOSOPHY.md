# Design Philosophy

This framework is built around three principles: scope discipline, expectations-first QA, and reusable process knowledge.

## 1) Expectations-First QA

AI agents are biased by implementation. If they see the code first, they often rationalize it as correct.
Expectations-first QA forces a pre-commitment to success criteria before inspection, which makes QA objective and repeatable.

Benefits:
- Clear DONE criteria that do not drift
- Less rubber-stamping of flawed work
- Faster reviews because expectations are already explicit

## 2) Small Diffs, Fast Feedback

Large diffs hide mistakes and increase risk. This framework defaults to minimal, reviewable change sets:
- Each task should be one cycle in size.
- Each change set should be easy to validate and roll back.

Small diffs keep QA honest and reduce the cost of mistakes.

## 3) Roles as Lenses

Different types of work require different mental models. Roles provide a consistent lens:
- Builder focuses on safe implementation.
- QA focuses on verification and evidence.
- Advisor focuses on scope and clarity.

This separation reduces cognitive overload and keeps output consistent across cycles.

## 4) Prompt Artifacts as Executable Contracts

Prompts are treated as executable task contracts. They encode:
- objective
- constraints
- plan
- commands
- verification criteria

This makes work repeatable and allows later auditing.

## 5) Skills as Knowledge Accumulators

Skills capture “how we do this safely” for recurring tasks. They prevent relearning the same lessons and reduce risk in complex operations.

## 6) Auditability Over Convenience

The workflow favors explicit logs and artifacts over convenience. Every cycle leaves a trail:
- expectations
- history log
- archived prompt

This is essential for reliability in production systems.
