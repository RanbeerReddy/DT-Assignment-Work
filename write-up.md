## 1. Why These Specific Questions?

The main idea was to move from just recalling what happened to understanding where I was mentally in those situations.

Instead of asking abstract questions, I focused on real, everyday work situations — things like missed tasks, feedback, or helping someone. These are moments where people naturally reveal how they think.

### Question Design by Axis

**Axis 1 (Locus of Control):**
I used storytelling-type questions to understand whether the person felt like they were driving their day or just reacting to it. The goal wasn’t to judge, just to see how they interpret control.

**Axis 2 (Orientation):**
This is based on situations outside the “official job.” I wanted to capture whether someone naturally contributes beyond what’s required, or mainly sticks to defined responsibilities.

**Axis 3 (Radius of Concern):**
This looks at perspective. When someone is stressed, it’s often because their focus is very narrow. Expanding that to include others (team, users, impact) can change how the same situation feels.

### Question Design Principles

For all questions, I made sure:

- No option feels obviously right or wrong
- All options feel realistic
- Each option maps clearly to a behavioral signal

## 2. Branching Design & Trade-offs

The system works by collecting signals from answers and then branching based on those signals.

Each response adds to one side of an axis:

- Internal vs external
- Contribution vs entitlement
- Others vs self

### How Branching Works

Each axis follows a simple pattern:

**2–3 questions → decision → (if unclear) one extra question → final decision → reflection**

- If answers clearly lean one way → go directly to reflection
- If they're mixed → ask one clarifying question

I added this because I didn’t want the system to end with “neutral” outputs. Those don’t really tell you anything useful.

### Trade-offs I Made

**1. More depth vs fewer questions**
- I could have made a shorter tree, but it would've been less reliable
- I chose to include a few more nodes to get better signal clarity

**2. Simple logic vs complex scoring**
- Instead of using complicated thresholds, I kept it simple:
  ```
  if A > B → choose A
  if B > A → choose B
  else → ask one more question
  ```
- This makes the system easier to:
  - Understand
  - Debug
  - Trace directly from the JSON

**3. Adaptivity without randomness**
- The system feels adaptive because of the extra questions, but everything is still:
  - Predefined
  - Deterministic
- There's no randomness or AI decision-making at runtime

## 3. Psychological Foundations

The design is based on a few core ideas:

**Julian Rotter — Locus of Control Theory**
- Used for Axis 1 — understanding whether people attribute outcomes to themselves or external factors

**Carol Dweck — Growth Mindset**
- Influenced how reflections are written — focusing on patterns and responses rather than labeling outcomes

**Organizational Citizenship Behavior (OCB)**
- Used in Axis 2 to capture contribution beyond formal job requirements

**Abraham Maslow — Self-Actualization & Transcendence**
- Used in Axis 3 — expanding perspective beyond self

## 4. What I'd Improve with More Time

**1. Tracking Across Days**
- Right now, each session is independent
- It would be much more useful to compare patterns over time

**2. Weighted Signals**
- Currently, all questions contribute equally
- Some situations (like high-pressure decisions) should probably carry more weight

**3. Better Reflection Personalization**
- Right now reflections depend on dominant signals
- They could be improved by referencing specific answers more directly