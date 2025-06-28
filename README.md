"""#  LangGraph Multi-Agent Debate DAG

This project simulates a structured debate between two AI agents using OpenAI's GPT-3.5 and the LangGraph library. Each agent takes turns presenting arguments on a user-specified topic, and a judge (also an LLM) evaluates the debate and announces a winner. This project showcases DAG-based coordination using LangGraph and memory-passing logic across multiple rounds.

---

##  Features

-  Fully interactive CLI: Users provide the debate topic and roles for both agents.
-  LangGraph DAG structure with memory-passing and conditional judgment.
-  Supports 8 alternating rounds of debate using GPT-3.5-Turbo.
-  Judge node summarizes arguments and declares a winner.
-  Outputs:
  - `.txt` transcript + verdict
  - `.png` DAG visualization using Graphviz

---

##  Tech Stack

- **LangGraph** for DAG node coordination and memory handling.
- **OpenAI API (`openai==1.3.8`)** for LLM-based reasoning.
- **Google Colab** as runtime platform.
- **Graphviz** for visualizing the DAG.

---

##  How It Works

### 1. User Input (CLI)
Users provide:
- A debate topic
- Profession of Agent 1 (e.g., Scientist)
- Profession of Agent 2 (e.g., Philosopher)

This dynamic flow ensures agent roles are not hardcoded.

### 2. LangGraph DAG Setup
A custom `DebateState` is defined to carry:
- The current round
- Memory per agent
- Debate history
- Next speaker
- Final verdict

LangGraph nodes are configured:
- `agent_turn`: Generate LLM response
- `update_memory`: Store full transcript
- `judge`: Summarize and declare a winner

Control is routed using a `route()` function that sends flow to the judge after round 8.

### 3. Execution
The DAG is invoked using `.invoke(initial_state)`:
- 8 rounds are executed (turn-by-turn)
- The judge node is triggered on the 9th transition
- All outputs are printed and saved

### 4. Output Files
- `debate_log_<timestamp>.txt`: Full transcript + final verdict
- `debate_dag_<timestamp>.png`: A visual DAG flow

Files can be downloaded in Colab using:
```python
from google.colab import files
files.download(...)
Sample Flow
User Input:


Topic: Should AI be regulated as medicine?
Agent 1: Scientist
Agent 2: Philosopher
Round 1: Scientist argues

Round 2: Philosopher responds

...

Verdict: Judge declares the winner with reasoning

 DAG Architecture
The DAG diagram (auto-generated) contains:


User Input → Agent 1 Turn → Memory Update → Agent 2 Turn → ...
→ After 8 rounds → Judge → Verdict
Graphviz renders this into a .png file to satisfy the deliverable.

 Demo Video
https://www.loom.com/share/8cca0174bfdc4c7ab0dd839a210871ea?sid=3975f92d-8105-4a8d-89c1-3f5c057ad98f""""""
