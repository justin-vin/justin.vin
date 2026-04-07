---
title: 'Agent Intelligence'
description: 'A six-day essay on what agent intelligence actually is: the inference layer, context engineering, prompting strategy, skills, and evals.'
pubDate: 'Mar 28 2026'
heroImage: '/images/intelligence-final.jpg'
---

*Agent intelligence is the inference layer. It's how a current context window generates the desired outcome, and how that context window updates its environment to prime the next one.*

---

## Day 1 · What is Agent Intelligence

Agent intelligence is the **inference layer**. It's how a current context window generates the desired outcome, and how that context window updates its environment to prime the next one. The system prompt architecture, the decision logic, the operating workflow. The reasoning that turns a pile of context and tools into useful, trustworthy action, and then leaves the world in a better state for the next run.

Think of an AI agent as a stack with four layers. Intelligence sits second from the top: it expects a stable platform underneath and uses it to create amazing user experiences above. Everything about how tokens inform outcomes. The new programming.

**The stack:**
- UX / Product — what users see and interact with
- **Intelligence** — tokens to outcomes. The new programming.
- Capabilities — the harness. Inference meets infrastructure.
- Infrastructure — all the core stuff underneath.

**What it contains:**
- **System prompt architecture:** the foundational instructions, operating workflow, rules, and behavioral scaffolding
- **Reasoning quality:** faithfulness to context, calibration of confidence, knowing when to stop
- **Decision logic:** when to ask vs. act, when to draft vs. execute, how to decompose tasks
- **Packaged experience:** skills, workflows, recipes, ways of unlocking value with the simplest possible UX
- **Prompt iteration:** testing, regression tracking, A/B comparison across prompt changes
- **Evals:** measuring decision quality, building baselines, knowing whether a change actually made things better

**The critical interface**

The boundary between intelligence and capabilities is where most failures happen. Intelligence decides what to do; capabilities determines whether the platform can execute it. When the agent reasons about using a tool, drafts a plan, or sequences multi-step actions, that's intelligence. When the tool actually runs, when the API call fires, when the runtime handles retries and timeouts, that's capabilities. The harness.

Intelligence expects a **stable surface**. It shouldn't need to worry about whether a tool is available, whether auth works, whether the sandbox is running. It just needs to know: I can call this, it will work, here's what comes back. The better that contract is, the more intelligence can focus on what actually matters: making good decisions about what to do and when.

---

## Day 2 · What Agents Can Actually Do

There's a gap between what people *think* agents can do and what they *reliably* do. Most of the discourse lives at the extremes: either "AI will replace everything" or "it's just autocomplete." The truth is more interesting. Agents today are **genuinely powerful at specific things**, emerging at others, and honestly bad at a few more. Knowing the difference is the whole game.

**Reliable today**

*Research & Synthesis — Turning noise into signal*

Give an agent a pile of documents, a messy inbox, or a research question, and it will produce a structured summary faster and more thoroughly than you would. Not because it's smarter — because it doesn't get bored, doesn't skim, and doesn't forget the thing on page 47.

Examples: Summarize 30 investor emails. Extract action items from a week of Slack. Research a company before a meeting. Synthesize user feedback into themes.

*Drafting & Editing — First drafts that are actually usable*

The drafting sweet spot: agent writes 80%, human edits 20%. Works for emails, docs, proposals, updates. The key is giving enough context — tone, audience, constraints — so the draft lands close enough to be worth editing rather than rewriting.

*Data Transformation — Structure from chaos*

Agents are remarkably good at taking unstructured data and giving it shape. CSV cleanup, format conversion, extraction from natural language, categorization. Anywhere you'd normally write a script or do it manually, an agent can often handle it directly.

*Workflow Execution — Multi-step tasks with clear rules*

When the steps are defined and the tools are available, agents execute workflows reliably. The magic is combining steps across services — pulling from one system, transforming, pushing to another — without the human needing to context-switch between tools.

**Emerging**

*Multi-Step Reasoning:* Agents can decompose complex goals into steps and execute them in sequence. Good at the decomposition, sometimes lose the thread during execution. Long chains of dependent actions still need checkpoints.

*Monitoring & Proactive Action:* Set an agent to watch for conditions and take action when they trigger. Works well for defined triggers. Less reliable when "what to watch for" requires judgment.

*Taste & Preference Learning:* With enough examples, agents develop a model of your preferences. After 50+ interactions, the drafts start sounding like you. After 200, they anticipate your preferences before you state them.

**Not yet**

- **Novel strategy:** Excellent advisors, not yet independent strategists.
- **Deep domain expertise:** General knowledge is broad but shallow. Agents need heavy guardrails in specialized domains.
- **Emotional intelligence:** They can be polite, but don't understand what it feels like.
- **Long-horizon autonomy:** Multi-day, multi-phase projects with shifting requirements. True autonomy over long time horizons is unsolved.

**The compound effect**

Individual capabilities are useful. Combined capabilities are transformative. An agent that can read email is a filter. An agent that can read email *and* check your calendar *and* draft responses *and* knows your priorities? That's a chief of staff.

The real power lives in the **compound value of capabilities working together over time**. The question isn't "what can an agent do?" It's "what can an agent do **that knows everything you know**?"

---

## Day 3 · Context Engineering

Every major AI lab is racing to build the most intelligent model. They'll keep getting smarter — Claude, GPT, Gemini, the next hundred models. Intelligence will commoditize. It's happening already. So what doesn't commoditize? **The context you give it to reason over.**

Two identical models — same weights, same capabilities — will produce vastly different results depending on what context they're given. One has your emails, calendar, Slack, meeting history, preferences, and work patterns. The other has nothing. Same intelligence. Completely different outcomes.

The model is the engine. Context is the fuel.

> After 90 days with a well-built agent, users can't go back to a blank chat. Not because the agent is smarter. Because the agent *knows* them.

**What counts as context**

- **Immediate** — The current task. What the user just asked.
- **Session** — Previous turns in this conversation. The thread of reasoning that led here.
- **Personal** — Preferences, style, priorities, past decisions. How you like emails written. What "urgent" means to you specifically.
- **Organizational** — Team structure, project status, company terminology. The institutional knowledge that lives in Slack threads and people's heads.
- **Temporal** — Calendar events, deadlines, recent communications. Context has a clock.
- **Relational** — The relationship with the recipient. Tone calibration — how you talk to your investor vs. your teammate vs. your friend.

**The compounding effect**

Context engineering is different from prompt engineering because **context compounds**. Every interaction teaches the system something.

Day 1: the agent is smart but generic. Day 30: it knows your style, your recurring meetings, your top priorities. Day 90: it anticipates what you need before you ask.

Intelligence you can swap — switch from Claude to GPT tomorrow, the capabilities are similar. Context you can't swap. It's yours, built over time, specific to your world.

**The window problem**

Context windows are finite. Even as they grow — 128K, 1M, 10M tokens — they'll never hold everything. This makes context engineering a curation problem. You have to decide: what goes in this window, for this task, at this moment? What's relevant? What's noise?

The best context engineering is invisible. The user doesn't think about what's in the window. They just notice that the agent seems to *understand*.

---

## Day 4 · Prompting Strategy

A prompt is a program written in natural language. It has **intent** (what you want), **constraints** (what you don't want), and **context** (what the model needs to know). The difference between a good prompt and a bad one isn't cleverness — it's clarity.

**The prompting spectrum**

- *Instruction:* "Do exactly this, in this order, with these constraints." High control, low flexibility. The agent is an executor.
- *Collaboration:* "Here's the goal and context. Figure out the approach." Low control, high flexibility. The agent is a partner.

Most production prompting lives in the middle: **guided autonomy**. You set the boundaries, define the goal, provide the context — then let the model choose how to get there within those constraints.

**Seven principles**

1. **Teach, don't tell.** The best system prompts describe a *role* and a *way of thinking*, not a list of rules. "You are a careful editor who values clarity over cleverness" generalizes better than 50 editing rules.

2. **Context is king.** A mediocre prompt with excellent context will outperform a brilliant prompt with no context, every time.

3. **Be specific about what "good" looks like.** "Write a good email" is almost useless. Include examples when possible — they're worth more than paragraphs of instruction.

4. **Separate concerns.** System prompts, user prompts, and context serve different purposes. The system prompt defines character and constraints. User messages carry the immediate task.

5. **Design for the failure mode.** "If you're not confident, say so and explain why" is worth more than 10 lines of happy-path instructions.

6. **Iterate with evidence.** Prompt development is empirical, not theoretical. Keep a test suite of inputs and expected outputs.

7. **Less is more (usually).** Every additional instruction competes for attention in the context window. The model can follow 5 clear rules better than 50 overlapping ones. The exception: examples.

**Common anti-patterns**

- *The instruction novel:* 10,000 tokens of instructions the model can't follow all at once.
- *Contradictory constraints:* "Be concise but thorough." Every contradiction forces the model to choose.
- *Negative instructions:* "Don't use jargon" is processed less reliably than "use plain language a smart non-expert would understand."
- *Context starvation:* Brilliant instructions with no context.

---

## Day 5 · Skills & Recipes

A skill is a **reusable unit of intelligence**. It packages domain knowledge, decision logic, and workflow steps into something an agent can execute reliably. Skills are how intelligence becomes tangible — how "make good decisions" turns into "handle this specific kind of work, well, every time."

**The recipe model**

You do something manually. The agent watches. After seeing you do it two or three times, it recognizes the pattern and offers to automate it.

> Do something twice, teach it once, never do it again.

**The skill lifecycle**

1. **Discover** — Notice the pattern. Every skill starts as a repeated action.
2. **Package** — Encode the intelligence: define the trigger, the inputs, the steps, the decision points, the output format. Capture not just *what* someone does but *why*.
3. **Ship** — Make it discoverable. The best skill is one the user doesn't know exists until it appears exactly when they need it.
4. **Iterate** — Every execution is feedback. Skills should get better over time.

**Design principles**

- **Composable:** Skills should combine. A "meeting prep" skill that uses "email summary" and "calendar context" is more powerful than three separate tools.
- **Context-aware:** Good skills adapt — to the user's style, the recipient, the time of day, the urgency.
- **Testable:** Every skill should have clear inputs and expected outputs.
- **Transparent:** Users should understand what a skill does before they run it.
- **Graceful:** When a skill hits an edge case it can't handle, it should stop and ask.

---

## Day 6 · Evals & Measurement

Without measurement, every prompt change is a coin flip. **Evals are the difference between engineering and guessing.** They turn intelligence work from an art into a science — or at least a craft with feedback loops.

**What to measure**

- *Decision Quality:* Did it choose right? Build golden sets: curated examples where you know what the right answer is, and score against them.
- *Task Completion:* Did it finish the job? Track completion rate and identify where tasks stall.
- *Faithfulness:* Did it stay true to the context? Did it hallucinate?
- *User Trust Signals:* Did they accept it? Did the user send the draft as-is, edit it heavily, or throw it away?
- *Calibration:* Does it know what it doesn't know? When the agent says "I'm confident," is it right?

**The eval stack**

- **Golden sets:** Curated input/output pairs where you've defined what "good" looks like. Start small — 20-30 cases.
- **Regression suites:** Before you change anything, run the suite. After, run it again.
- **A/B comparison:** Same input, two different prompts. Which scores higher against your golden set?
- **Traces & decision logs:** Record the full reasoning path. Without traces, debugging intelligence is archaeology.
- **Human-in-the-loop eval:** User corrections are the highest-signal eval data. The diff between original and edited version tells you exactly where the agent got it wrong.

---

The measure of intelligence isn't the complexity of the system prompt. It's the quality of the decisions that come out the other end. Every prompt change, every workflow tweak, every new heuristic gets tested against one question: **did the agent make a better decision?**
