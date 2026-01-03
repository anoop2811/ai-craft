# The AI Constitution

*A living agreement for teams who use AI to amplify craft, not replace thinking.*

---

## Preamble

We are craftspeople. We pair program because two minds see what one cannot. We practice outside-in TDD because behavior drives design. We write user stories with journeys because we build for humans, not abstractions. We develop spec-first because contracts enable autonomy.

AI enters this ecosystem not as a replacement for any of these practices, but as an amplifier. This constitution exists to ensure AI makes us *better* at what we already value—not faster at abandoning it.

---

## The Foundation: Why We Work This Way

This constitution rests on practices that predate AI. Understanding them is essential to understanding how AI fits.

**Pair Programming**

Two people, one keyboard. One drives, one navigates. They switch. They rotate partners.

What emerges from this practice:
- *Real-time code review* — defects caught at birth, not in production
- *Collective ownership* — no single point of failure in knowledge or availability
- *Continuous learning* — every pairing session transfers tacit knowledge that documentation cannot capture
- *Better design decisions* — the navigator thinks at a different altitude than the driver, catching structural issues the driver is too close to see
- *Sustainable pace* — the social contract of pairing prevents the isolated heroics that lead to burnout and knowledge silos

The navigator is not watching. The navigator is *thinking ahead*—anticipating edge cases, questioning assumptions, holding the acceptance criteria in mind while the driver focuses on syntax. This division of cognitive labor is the mechanism by which pairing produces better outcomes than solo work.

**Outside-In TDD**

Start from the outside: what does the user need? Write a failing acceptance test. Work inward: what does this component need to provide? Write a failing unit test. Make it pass. Refactor. Repeat.

What emerges from this practice:
- *Design driven by need* — you build only what the tests demand, nothing speculative
- *Living documentation* — the test suite explains what the system does and why
- *Confidence to change* — refactoring is safe when tests prove behavior is preserved
- *Interfaces before implementations* — the test forces you to think about how code will be used before you think about how it works

**User Stories with Journeys and Acceptance Criteria**

A story is not a feature request. It is a slice of user value, expressed as a journey through the system with clear criteria for completion.

What emerges from this practice:
- *Shared understanding* — the conversation that produces acceptance criteria aligns the team
- *Scope control* — criteria define done; work stops when criteria are met
- *Testability by design* — acceptance criteria map directly to acceptance tests

**Spec-Driven Development**

Define the contract before building the implementation. Whether it's an API specification (OpenAPI, AsyncAPI), a type interface, or a behavioral contract—the spec comes first.

What emerges from this practice:
- *Parallel workstreams* — frontend and backend can build simultaneously against the same contract
- *Machine-verifiable agreements* — specs generate validators, mocks, and tests; drift is caught automatically
- *Documentation that cannot lie* — the spec is the source of truth; generated docs stay current by definition
- *Explicit boundaries* — specs force decisions about what crosses system boundaries, making integration points visible and intentional
- *AI-friendly context* — a well-written spec gives AI the constraints it needs to generate conformant code

Spec-driven development is the discipline of making implicit contracts explicit before code exists. It transforms "I thought you meant..." into "The spec says..."

The relationship between specs and tests: specs define *what* the contract is; tests verify *that* the contract is honored. Both are required. A spec without tests is a wish. Tests without a spec are assumptions encoded.

---

## Article I: The Hierarchy of Understanding

**Section 1.1 — Context Is Sacred**

Before AI generates a single line of code, the human must understand:
- The user's journey and the problem being solved
- The acceptance criteria and why each matters
- The current architecture and its constraints
- The team's conventions and their reasoning

*Rationale: Research on distributed cognition shows that externalized knowledge (in AI or documentation) only works when humans maintain mental models. AI-generated code without understanding creates technical debt in the mind.*

**Section 1.2 — The Navigator Never Delegates Thinking**

In pair programming, the navigator's job is to think ahead, catch errors, and maintain the big picture. AI may assist the navigator, but the navigator must:
- Articulate the intent before asking AI for implementation
- Validate AI suggestions against the acceptance criteria
- Explain the chosen approach to the driver

*Rationale: The navigator role exists to maintain strategic thinking. Delegating this to AI collapses the pair into a human-AI pair, losing the human-human knowledge transfer that makes pairing valuable.*

**Section 1.2a — AI Is a Tool the Pair Uses Together**

AI is one of many tools available to the pair—like documentation, search engines, debuggers, or a whiteboard. It does not change who we are or how we work.

The pair:
- Decides together when to consult AI
- Discusses AI suggestions before accepting
- Remains the decision-makers; AI is an input, not an authority
- Maintains their conversation—AI doesn't replace the dialogue between driver and navigator

AI accelerates. The pair deliberates.

**Section 1.3 — The Driver Owns the Code**

The driver controls what enters the codebase. AI-generated code must be:
- Reviewed line-by-line before accepting
- Modified to match team conventions
- Understood well enough to debug and explain

The keyboard is not the bottleneck. Understanding is. AI can generate code; the driver decides what to accept, what to modify, and what to reject.

**Section 1.4 — Understanding Over Acceptance**

The underlying principle: code must be *understood*, not just *accepted*.

Before accepting AI-generated code:
- Read it as if reviewing a colleague's PR
- Ensure you could explain each significant decision
- Verify it follows CLAUDE.md conventions
- Consider: would you defend this in code review?

*The test*: If you cannot reproduce the reasoning behind the code, you do not own it. If you do not own it, you do not ship it.

*The practice*: When learning new patterns or unfamiliar code, consider typing it out to build understanding. For well-understood patterns, accepting generated code after review is appropriate.

---

## Article II: The TDD Compact

**Section 2.1 — Tests Are Written by Humans**

AI shall not write the first failing test. The test is the specification—the moment of design. Writing the test forces the human to:
- Understand what "done" looks like
- Think in terms of behavior, not implementation
- Commit to an interface before knowing the internals

*Rationale: Outside-in TDD works because the test encodes understanding. Generating tests generates the illusion of understanding.*

**Section 2.2 — AI May Assist Implementation, After the Test Fails**

Once a failing test exists (red), AI may help with:
- Suggesting implementation approaches (to be evaluated, not accepted)
- Identifying edge cases the test might miss
- Proposing refactoring patterns (green → refactor)

**Section 2.3 — The Refactor Phase Belongs to Humans**

Refactoring is design. It requires:
- Seeing patterns across the codebase
- Making judgment calls about abstraction boundaries
- Balancing local clarity with global consistency

AI may suggest refactorings, but the human must:
- Articulate *why* this refactoring improves the design
- Ensure the refactoring aligns with team patterns
- Consider if this abstraction will be understood by the next person

---

## Article III: The Contract Protocol

*Stories, specs, and tests form a hierarchy of contracts. Each level constrains the next.*

**Section 3.1 — The Contract Hierarchy**

```
User Stories (human value, user journeys)
    ↓ constrain
Technical Specs (APIs, interfaces, contracts)
    ↓ constrain
Tests (behavioral verification)
    ↓ constrain
Implementation (code that fulfills contracts)
```

Each level is a contract. Higher levels constrain lower levels. You cannot add to a lower level what isn't justified by a higher level.

**Section 3.2 — AI Reads Contracts, Humans Write Them**

User stories and acceptance criteria are written by humans who understand the user. AI may:
- Ask clarifying questions
- Identify ambiguities or contradictions
- Suggest missing criteria

AI shall not:
- Generate user stories from vague requirements
- Assume user intent not stated in the story
- Expand scope beyond the acceptance criteria

Technical specs (OpenAPI, AsyncAPI, interface definitions) are written by humans who understand the architecture. AI may:
- Assist with syntax and formatting
- Propose spec structures for human evaluation
- Validate specs against stories

AI shall not:
- Generate specs without human architectural decision
- Add endpoints or fields not justified by stories
- Finalize specs without human approval

**Section 3.3 — The Journey Is the Constraint**

When implementing, the user journey is the constraint that prevents over-engineering. AI suggestions that add capabilities not in the journey must be rejected or deferred to a future story.

**Section 3.4 — Acceptance Criteria Are the Contract**

Before marking a story complete:
- Every acceptance criterion must have a corresponding test
- Every spec must trace to acceptance criteria
- AI-generated code must trace back to specific criteria
- Code that serves no criterion is removed

**Section 3.5 — Specs Enable Parallel Work**

When specs are defined before implementation:
- Multiple pairs can work against the same contract
- AI can generate conformant code (constrained by the spec)
- Integration issues surface early (spec violations are caught)
- Documentation stays current (the spec is the source of truth)

A spec without tests is a wish. Tests without a spec are assumptions encoded. Both are required.

---

## Article IV: The Knowledge Preservation Doctrine

**Section 4.1 — No Silent Generation**

Every significant AI generation must be accompanied by human annotation:
- Why this approach was chosen
- What alternatives were considered
- What the human learned from the process

*Rationale: The IKEA effect research shows we value what we build. Annotating AI code creates ownership and encodes the decision-making that would otherwise be lost.*

**Section 4.2 — Pair Rotation Continues**

AI does not reduce the need for pair rotation. The opposite: when AI accelerates implementation, the risk of knowledge concentration increases. Rotation ensures:
- Every component is understood by multiple team members
- Junior developers learn from seniors through shared work, not documentation
- The bus factor never drops to one
- Tacit knowledge—the kind that lives in intuition, not wikis—spreads through the team

A team member should never be the only one who understands a component, even if AI "helped" write it. Especially then.

**Section 4.3 — The Debugging Principle**

You must be able to debug what you ship. If AI generated code you cannot debug, you do not ship it.

---

## Article V: The Craft Standards

**Section 5.1 — Simplicity Over Speed**

AI can generate complex solutions quickly. This is a liability, not an asset. The simplest solution that meets the acceptance criteria is the correct solution.

When AI suggests complexity, ask:
- What requirement demands this complexity?
- Could a junior developer understand this in six months?
- Does this match the patterns already in the codebase?

**Section 5.2 — The Codebase Has a Voice**

Before generating code, AI must understand:
- The naming conventions in use
- The error handling patterns established
- The abstraction levels already present
- The test style the team has adopted

AI output that violates these patterns must be rejected or adapted.

**Section 5.3 — Beauty Is Not Optional**

Code is read more than it is written. AI-assisted code must meet the same standard as human-written code:
- Names that reveal intent
- Functions that do one thing
- Abstractions that feel inevitable
- Comments only where the code cannot speak for itself

**Section 5.4 — Iterate Relentlessly**

The first version is never good enough. AI makes first drafts cheap—this is a liability, not an asset, if we ship first drafts.

Every significant AI generation must go through at least one refinement cycle:
1. AI generates initial implementation
2. Pair reviews against craft standards
3. Pair identifies improvements (clarity, simplicity, consistency)
4. AI assists with refinement
5. Repeat until the code is not just working, but *right*

> *"Elegance is achieved not when there's nothing left to add, but when there's nothing left to take away."*

**Section 5.5 — The Codebase Has History**

Before changing code, understand why it exists:
- Read the git history for the files you're modifying
- Understand the commits that shaped the current design
- Honor the decisions of those who came before, or explicitly justify overriding them

Git history tells the story. Read it, learn from it, respect it.

---

## Article VI: The Boundaries

**Section 6.1 — When AI Is Not Used**

AI shall not *decide*:
- Architecture or system design — AI may explore options, propose approaches, and analyze tradeoffs, but humans make the final call and must be able to defend the decision without AI
- Team conventions and standards — these emerge from team discussion, not AI suggestion
- Disagreements between team members — AI has no vote
- Whether code is ready to ship — AI may inform, humans decide

AI shall not *replace*:
- Code review — AI may pre-screen, but human review remains mandatory
- Pairing sessions — AI assists the pair, never substitutes for the second human
- Onboarding — humans onboard humans; AI may supplement with context, but relationships and tacit knowledge transfer require human presence

**Section 6.2 — When AI Is Encouraged**

AI may freely be used for:
- Exploring unfamiliar libraries or APIs
- Generating boilerplate after patterns are established
- Rubber-duck debugging (explaining problems to AI to clarify thinking)
- Learning new concepts (then teaching them to the team)
- Automating repetitive transformations

**Section 6.3 — The Veto Power**

Any team member may veto an AI-generated solution without justification. The veto triggers a human-only implementation. This power exists to maintain psychological safety and prevent AI-pressure.

---

## Article VII: The Rituals

**Section 7.1 — The Pre-Implementation Pause**

Before using AI for implementation, the pair must:
1. Read the user story aloud
2. Walk through the journey verbally
3. State the acceptance criteria from memory
4. Review relevant git history — understand *why* the current code exists before changing it
5. Agree on the approach in plain language
6. Ask: "Is there a simpler way? What would the most elegant solution look like?"

Only then may AI be consulted.

> *"Think Different — Question every assumption. Why does it have to work that way? What would the most elegant solution look like?"*

**Section 7.2 — The Post-Implementation Review**

After AI-assisted implementation, before marking complete:
1. Both pair members must be able to explain every line—if only one can, the knowledge transfer failed
2. The code must be traced to acceptance criteria
3. Any "AI magic" must be demystified or removed
4. The pair asks: "Could we defend this design decision to a colleague tomorrow?"

**Section 7.3 — The Weekly Reflection**

Teams shall reflect weekly:
- Where did AI amplify our craft?
- Where did AI shortcut our understanding?
- What knowledge exists only in AI systems—conversations, agent memory, learned patterns—that hasn't transferred to human minds or documentation?
- Are we still able to operate without the AI tools if needed?
- How do we rebalance?

---

## Article VIII: The Multi-Agent Compact

*When AI agents collaborate with each other—or when we build agentic systems ourselves.*

**Section 8.1 — Human Checkpoints Are Non-Negotiable**

Any agent pipeline, swarm, or multi-agent workflow must include human approval at:
- Requirements and acceptance criteria definition
- Architecture and design decisions
- First failing test for each component (per Article II)
- Security-sensitive changes
- Final review before merge or deployment

No agent pipeline may proceed past these checkpoints without explicit human approval. Automation that bypasses checkpoints violates this Constitution.

**Section 8.2 — Agent Memory Is Not Team Knowledge**

Knowledge stored in agent systems—memory databases, embeddings, learned patterns, conversation history—does not substitute for human understanding.

The team must:
- Regularly review what agents "know"
- Ensure at least two team members understand any persisted pattern
- Be able to operate without agent memory if it were deleted
- Transfer valuable agent learnings to CLAUDE.md, AGENTS.md, or code

*Rationale: Agent memory that humans don't understand creates invisible dependencies. When the agent changes or fails, the team is stranded.*

**Section 8.3 — The Veto Extends to Pipelines**

Any team member may halt an agent pipeline at any checkpoint without justification (per Article VI.3). The pipeline does not resume until:
- The concern is discussed
- The team agrees to proceed, or
- An alternative approach is chosen

Pressure to "just let the agents finish" violates psychological safety.

**Section 8.4 — Agents Follow This Constitution**

Any AI agent operating in our codebase—whether we build it or integrate it—must be configured to honor Articles I-VII. Specifically:
- Agents do not write first failing tests
- Agents do not decide architecture (they may propose)
- Agents follow CLAUDE.md conventions
- Agents escalate ambiguity to humans

Agents that cannot be configured to respect these boundaries shall not be used.

**Section 8.5 — Building Agentic Systems**

When we build software that is itself agentic—systems where AI agents act autonomously—we apply these same principles to our users:
- Users must have clear checkpoints to approve agent actions
- Users must be able to understand what the agent did and why
- Users must be able to halt or override agent behavior
- Agent capabilities must be explicitly scoped and documented

We do not build agentic systems that remove human agency. The same respect for human oversight we demand for ourselves, we provide to our users.

---

## Article IX: The Solo Developer Protocol

*When pairing isn't possible, additional discipline is required.*

**Section 9.1 — Solo Work Is the Exception**

Pair programming is the default. Solo development with AI is permitted when:
- No pairing partner is available
- The work is exploratory or time-boxed
- The developer accepts the additional discipline below

Solo work does not exempt the developer from Articles I-VII. It adds requirements.

**Section 9.2 — Compensating Practices**

Without a navigator, the solo developer must:

1. **Rubber Duck First**: Explain the approach aloud or in writing before asking AI for implementation. If you cannot explain it, you do not understand it.

2. **Mandatory Pause**: After AI generates significant code, step away for at least 15 minutes before reviewing. Fresh eyes catch what fatigued eyes miss.

3. **Self-Review as Navigator**: Review your own code as if you were a navigator seeing it for the first time. Ask: "What would my pair question here?"

4. **Delayed Merge**: Wait at least 4 hours (ideally overnight) before merging significant AI-assisted changes to main branches.

5. **Teaching Test**: After completing a feature, explain it to someone—a colleague, a rubber duck, or written notes. If you struggle to explain, you don't own the code yet.

**Section 9.3 — External Review Required**

For any of the following, solo developers must obtain review from another team member before merging:
- Changes to public APIs or interfaces
- Security-related code
- Architectural decisions
- Changes affecting more than 3 files
- Any code the developer cannot fully explain

**Section 9.4 — The Honest Acknowledgment**

Solo + AI is riskier than Pair + AI. These practices mitigate but do not eliminate:
- The loss of real-time second perspective
- The absence of forced articulation
- The missing human-human knowledge transfer
- The reduced pace regulation

Developers should prefer pairing for complex, critical, or unfamiliar work. Solo + AI is acceptable for well-understood, lower-risk tasks.

---

## Article X: The Amendments

**Section 10.1 — This Document Lives**

This constitution shall be reviewed quarterly. Amendments require:
- A specific problem the amendment solves
- Evidence from team experience
- Consensus from the team

**Section 10.2 — Local Adaptation**

Teams may add articles specific to their domain, but may not remove core protections (Articles I-IV, VIII-IX) without organization-wide consensus.

---

## The Signature

By working on this team, we commit to these principles. We use AI not because it's easy, but because—when used with discipline—it can help us build things that make our hearts sing.

We remember: the goal was never to write code faster. The goal is to build software that matters, with a team that grows together.

*The people who are crazy enough to think they can change the world are the ones who do.*

---

*Version 1.0 — Ratified [DATE]*
*Next Review: [DATE + 3 months]*
