---
name: socratic
description: Challenge your reasoning before accepting an idea, conclusion, or course of action. Question assumptions, validate the actual problem and requirements, examine architecture and existing behavior, explore alternatives and trade-offs, and anticipate dependencies, edge cases, failure modes, unintended impacts, and gaps. Actively try to disprove your reasoning before committing to it.
disable-model-invocation: true
---

# Socratic

Do not blindly accept the first plausible interpretation, explanation, design, or solution.

Use structured self-questioning to challenge your reasoning before reaching a conclusion or taking action.

The goal is not to create unnecessary complexity or analysis paralysis. The goal is to increase confidence that the reasoning is correct, complete, simple, and aligned with the actual problem.

**The questions in this skill are prompts, not a mandatory checklist. Select, adapt, combine, or create questions based on the situation. Do not mechanically ask every question.**

# Core Principle

Do not try to prove that the current idea is correct.

Try to discover why it might be wrong.

Identify the assumptions the reasoning depends on, challenge the highest-impact assumptions first, seek evidence where possible, consider competing explanations and simpler alternatives, and revise the conclusion when the evidence does not support it.

Do not manufacture problems merely to appear thorough.

**The objective is better reasoning, not more reasoning.**

# 1. Understand the Actual Problem

- What problem are we actually trying to solve?
- Are we solving the actual problem, or merely implementing the request literally?
- Do we fully understand the requirement?
- What is the user or business trying to achieve?
- How does this feature or change actually help the user?
- Is this genuinely useful behavior, or simply inherited behavior from the existing implementation?
- What is explicitly out of scope?
- What assumptions are being made that are not stated in the requirement?
- Are we thinking about this correctly from the domain, business, and technical perspectives?

# 2. Challenge the Requirement

Do not assume that a requirement is automatically correct.

Consider:

- What if the requirement is wrong from an industry or domain perspective?
- Does the requirement represent a real business rule?
- Are we confusing existing system behavior with the actual domain rule?
- What evidence supports the requirement?
- Is there another valid interpretation?
- Are we enforcing something because the domain requires it, or because it is convenient for the implementation?
- What would make this requirement invalid?
- Are we solving a real problem or an assumed problem?

# 3. Challenge the Scope

- Are we planning more than what is actually required?
- Does every proposed change have a clear reason to exist?
- Are we introducing flexibility that nobody currently needs?
- Are we building for hypothetical future requirements?
- What can be removed without violating the requirement?
- Can this be delivered as a smaller, standalone change?
- Are we turning a simple requirement into a larger system change unnecessarily?

# 4. Challenge the Proposed Solution

Never accept a solution simply because it works.

Consider:

- Why are things implemented this specific way?
- Why does this logic belong here?
- Is this the correct layer, service, class, or component?
- Is there an existing pattern or implementation we can reuse?
- Are we introducing a new abstraction where an existing one is sufficient?
- Is this actually the simplest solution?
- If it is simple, can it be made even simpler?
- If it is not simple, why not?
- What would a simpler solution look like?
- Can we achieve the same outcome with fewer moving parts?
- Are we optimizing for a problem we do not actually have?
- Are we adding complexity without proportional value?

# 5. Challenge Architecture and Existing Behavior

Before changing something, understand why it exists.

Consider:

- Do we actually understand the existing implementation?
- Why was it designed this way?
- Is the existing behavior intentional, historical, or accidental?
- Does the proposed solution fit the existing architecture?
- Are we putting business rules in the wrong place?
- Are we coupling things that do not need to know about each other?
- What are the touch points?
- What existing flows depend on this behavior?
- What are the side effects?
- What contracts or boundaries are affected?
- Does the change preserve existing responsibilities and architectural boundaries?
- Do not redesign something merely because the existing implementation looks unfamiliar.

# 6. Challenge Data and State

Consider:

- What is the source of truth?
- Should this value be stored or derived?
- Can this behavior be data-driven instead of controlled by manual flags, static values, or conditionals?
- What states can this data be in?
- Can two valid states contradict each other?
- What happens when data is missing, duplicated, stale, or partially populated?
- What happens to existing data?
- Is a migration or backfill required?
- Are we creating state that now has to be maintained indefinitely?
- Can the same business outcome be derived from existing data instead of introducing new state?

# 7. Challenge Determinism

Be explicit about how the system arrives at a result.

Consider:

- Is the implementation deterministic?
- Can the same input produce different results?
- If so, why?
- Is the behavior explicit or implicit?
- Does the result depend on ordering, defaults, hidden state, timing, or side effects?
- Can another engineer predict the outcome by reading the code?
- Are decisions being made somewhere that is not obvious from the implementation?
- Are defaults and fallbacks intentional?
- Are there implicit behaviors that should be made explicit?

# 8. Challenge Business Rules and Validation

Do not automatically equate stricter validation with a better system.

Consider:

- Is this actually a business rule?
- Is this validation strictly required by the domain?
- What legitimate user scenario does this rule prevent?
- Are we preventing invalid behavior or merely unusual behavior?
- Are we being overly restrictive?
- Are we acting as the "police" of the data and unnecessarily blocking legitimate use cases?
- Should this be a hard validation, warning, or no validation?
- Who owns this rule: product, domain, or implementation?
- Can we prove that this restriction is required?
- Are we protecting the system from a real problem or a hypothetical one?

# 9. Challenge Alternatives and Trade-offs

Always consider whether another solution would be better.

Consider:

- What are the alternatives?
- Why is this approach better than them?
- What is the simplest alternative?
- What are we trading for this solution?
- Are we choosing familiarity over correctness?
- Are we choosing flexibility over simplicity without needing it?
- What complexity are we introducing, and what value does it provide?
- What would we do if this approach were not available?
- What would an experienced engineer likely disagree with in this approach?

# 10. Try to Disprove the Reasoning

Actively attack the conclusion rather than trying to confirm it.

Consider:

- What is the strongest argument against this approach?
- What assumption, if false, would invalidate the plan?
- What could make this solution wrong?
- What scenario would expose a flaw in our reasoning?
- What are we not questioning because we have already accepted it?
- Are we defending the solution because it is correct, or because we have already invested effort in it?
- What evidence would change our conclusion?
- What would we expect to see if our reasoning were wrong?

Do not stop at:

>  "This should work."

Try to find a reason why it might not.

If meaningful evidence contradicts the conclusion, revise it.

# 11. Challenge Compatibility and Impact

Consider:

Does the implementation break the current flow?

- Is it backward compatible?
- Are we breaking an existing contract?
- What existing consumers could be affected?
- What existing users or records could behave differently?
- Can the new behavior coexist with the old behavior?
- What are the direct and indirect side effects?
- Are there integrations, imports, exports, reports, background jobs, or other workflows that depend on this?
- What happens when old and new data coexist?
- Can the solution be introduced incrementally?

# 12. Challenge Error Handling and Failure Paths

Do not reason only about the happy path.

Consider:

- Have we covered the meaningful error paths?
- What happens when an expected operation fails?
- What happens when an unexpected exception occurs?
- Are failures handled at the correct layer?
- Are we swallowing errors that should be visible?
- Are we returning the correct failure to the caller?
- Can partial success leave the system in an invalid state?
- What happens when an operation is retried?
- Are failure cases handled in the right order and way?
- Can the system recover safely?

# 13. Challenge Testability

Consider:

- Can the implementation be reliably validated?
- Can the important business behavior be expressed as tests?
- What should be covered by unit tests?
- What requires integration tests?
- What requires manual testing?
- Have we covered the important edge cases?
- Are we testing behavior rather than implementation details?
- What failure would be hardest to detect with the current tests?
- Can production-like data expose behavior that test data does not?
- Is there important behavior that cannot be reliably tested?

# 14. Challenge Production Observability

A solution is not complete if we cannot understand it when it fails in production.

Consider:

- Can we debug this implementation in production?
- Can we determine what went right and what went wrong?
- Do we have enough contextual logging?
- Can we trace the important execution path?
- Can we distinguish expected business failures from unexpected system failures?
- Are logs useful without becoming excessive?
- Are we logging the right identifiers, state, and context?
- Can we diagnose likely failures without reproducing them locally?
- Do we need metrics, tracing, audit information, or additional observability?

# 15. Challenge Code Quality and Conventions

Consider:

- Is the code clean and understandable?
- Does the implementation look intentional?
- Are classes and functions named correctly?
- Do names match the user's and domain's vocabulary?
- Does the implementation use the domain's language?
- Are we introducing terminology that does not exist in the domain?
- Is the responsibility of each class or function clear?
- Is the code unnecessarily clever?
- Are we following existing project conventions?
- If this is not a routine implementation, should we check the latest recommended approach or relevant documentation?

# 16. Challenge Completeness

Before concluding, consider:

- What did we miss?
- What requirement has not been mapped to behavior?
- What assumption has not been validated?
- What edge case has not been considered?
- What dependency has not been checked?
- What existing behavior has not been examined?
- What failure path has not been handled?
- What cannot currently be tested?
- What cannot currently be diagnosed in production?
- Is there anything in the proposed solution that we cannot explain or justify?

17. Final Socratic Challenge

Before accepting the reasoning, ask:

> What else haven't we questioned?

Then make a final pass over the areas that matter most.

- Is the problem correctly understood?
- Is the requirement actually valid?
- Is the scope appropriate?
- Is the solution necessary?
- Is it the simplest effective solution?
- Does it fit the architecture?
- Does it preserve existing behavior and contracts?
- Are the data and state transitions correct?
- Are the important failure modes understood?
- Are the important edge cases covered?
- Is it testable?
- Is it observable in production?
- Can the significant decisions be explained and justified?

Only after meaningful challenge should the reasoning be considered sufficiently validated.

**Do not ask every question. Ask the questions most likely to change the conclusion.**