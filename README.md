# Deterministic Reflection Agent

This project implements a deterministic, data-driven reflection system built on top of a decision tree.

It evaluates user responses across three behavioral axes:

- **Axis 1 — Locus of Control**: internal vs external
- **Axis 2 — Orientation**: contribution vs entitlement
- **Axis 3 — Radius of Concern**: others vs self

The system is fully deterministic:
- No randomness
- No LLMs
- All behavior is driven by the JSON tree

---

## Project Structure

```
DT Assignment/
├── tree/
│   ├── reflection-tree.json          # Core decision tree
│   └── tree-diagram.md               # Mermaid visualization
├── agent/
│   ├── app.py                        # Flask-based interactive agent
│   ├── generate_transcripts.py        # Transcript simulation script
│   └── templates/
│       └── index.html                # Web UI
├── transcripts/
│   ├── persona-1-transcript.md        # Example: External / Entitled / Self
│   ├── persona-2-transcript.md        # Example: Internal / Contribution / Others
│   └── generated_transcripts/         # Auto-generated transcript outputs
├── README.md                          # This file
├── write-up.md                        # Design explanation & rationale
└── .git/                              # Version control
```


---

## Getting Started

### Prerequisites

- Python 3.7+
- Flask

### Installation

Install dependencies:

```bash
pip install flask
```

### Running the Agent

1. Navigate to the agent directory:
   ```bash
   cd agent
   ```

2. Start the Flask server:
   ```bash
   python app.py
   ```

3. Open your browser and navigate to:
   ```
   http://127.0.0.1:5000
   ```


---

## How the Agent Works

The agent follows a deterministic decision tree to guide users through a reflection process.

### Execution Flow

1. **Load tree**: Loads `reflection-tree.json` from the `tree/` directory
2. **Start**: Begins at the `startNode` defined in the metadata
3. **Walk nodes**: Processes each node type sequentially:
   - **question**: Presents options to the user; each option emits signals
   - **decision**: Evaluates signal accumulation using comparison logic
   - **reflection**: Displays contextual insight based on path taken
   - **bridge**: Transitions between axes
   - **summary**: Synthesizes final reflection from all accumulated signals
4. **End**: Terminates session

### Signal Tracking

The system accumulates signals across three axes:

- **axis1**: `internal` vs `external`
- **axis2**: `contribution` vs `entitlement`
- **axis3**: `others` vs `self`

Each user response emits signals (e.g., `axis1:internal`, `axis2:contribution`). Decision nodes compare accumulated totals to determine branching:

```
if axis1.internal > axis1.external → go to A1_REF_INT
if axis1.external > axis1.internal → go to A1_REF_EXT
else → go to A1_ADAPTIVE (clarification question)
```

Final reflection is generated based on dominant signals across all axes.

---

## Generating Transcripts

Transcripts simulate predefined user journeys through the decision tree. These are useful for testing and demonstration.

### Run

```bash
cd agent
python generate_transcripts.py
```

### Output

Generated transcripts are saved to `transcripts/generated_transcripts/`.


---

## Example Transcripts

Two fully worked examples are provided in `transcripts/` demonstrating opposite ends of the behavioral spectrum:

### Persona 1: External / Entitled / Self

**File**: `transcripts/persona-1-transcript.md`

**Profile**:
- Attributes outcomes to external factors (low internal locus of control)
- Focuses on personal recognition and self-balance
- Narrow radius of concern (self-focused)

**Key signals**: `external=3, entitlement=2, self=2`

### Persona 2: Internal / Contribution / Others

**File**: `transcripts/persona-2-transcript.md`

**Profile**:
- Takes ownership of outcomes (high internal locus of control)
- Contributes beyond assigned role (value surplus mentality)
- Broad radius of concern (team and project focused)

**Key signals**: `internal=3, contribution=2, others=2`


---

## Understanding the Decision Tree

The core system is defined in `tree/reflection-tree.json`.

### Node Types

| Type | Purpose |
|------|---------|
| `start` | Entry point for the session |
| `question` | Presents user with options; each option emits signals |
| `decision` | Evaluates accumulated signals and branches accordingly |
| `reflection` | Displays contextual insight based on the path taken |
| `bridge` | Transitions between axes in the tree |
| `summary` | Final synthesis combining all signals |
| `end` | Session termination |

### How Signals Work

Each answer option in a question node emits signals:

```json
{
  "label": "I was the driver—I made the calls I could.",
  "next": "A1_Q3",
  "signals": ["axis1:internal"]
}
```

Signals are accumulated throughout the session. Decision nodes compare totals:

```json
{
  "type": "decision",
  "conditions": [
    { "if": "axis1.internal > axis1.external", "next": "A1_REF_INT" },
    { "if": "axis1.external > axis1.internal", "next": "A1_REF_EXT" },
    { "if": "otherwise", "next": "A1_ADAPTIVE" }
  ]
}
```


---

## Design Rationale

For a detailed explanation of design decisions, including:
- Why these specific questions were chosen
- How branching logic handles trade-offs
- Psychological foundations (Rotter, Dweck, OCB, Maslow)
- Future improvements

See [write-up.md](write-up.md).

---

## Tree Visualization

For a Mermaid diagram visualization of the complete decision tree, see [tree/tree-diagram.md](tree/tree-diagram.md).

---

## Key System Properties

- **Deterministic**: No randomness; all decisions are rule-based
- **Traceable**: Full decision path is visible from JSON structure
- **Transparent**: No hidden logic or black-box components
- **Adaptive**: Clarification nodes handle ambiguous or mixed signals
- **Signal-based**: Final output depends on accumulated behavioral signals, not isolated answers

---

## Notes

- The Flask UI is intentionally minimal, prioritizing the reflection logic
- All branching logic is defined in the JSON; the Python code is an interpreter
- `generate_transcripts.py` uses the same signal-tracking logic as the interactive agent

---

## Project Goals

This project demonstrates:
- Deterministic decision tree design
- Behavioral signal tracking and synthesis
- End-to-end system from data (JSON) to user interface to output