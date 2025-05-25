# AI Report Writing Agent

Generate a structured report for any topic.

This project uses **LangGraph** and **LLM** to create a simple multi-node agent that:
1. Generates sub-questions based on a topic
2. Answers each question in parallel
3. Compiles all responses into a concise final report

---

## How It Works

The agent follows a multi-step process:
1. **Generate Questions**: Based on the topic, it dynamically chooses 3 or 5 concise sub-questions.
2. **Answer Questions**: Each question is answered in parallel using the LLM.
3. **Compile Report**: All answers are summarized into a structured report (with length constraints to reduce token use).

---
## Technical Highlights: LangGraph & the `Send` Function

This project showcases how to use **LangGraph** to build a dynamic and parallelized multi-agent workflow, especially with the `Send` function.

### LangGraph Node Design

Each stage of the report generation is built as a LangGraph **node**:

- `generate_questions`: Classifies topic complexity and generates either 3 or 5 sub-questions
- `continue_to_answers`: Uses `Send` to dynamically dispatch each question to the `generate_answer` node in parallel
- `generate_answer`: Handles answering each sub-question
- `compile_report`: Consolidates all answers into a final report, with optional word limits


### Workflow Diagram

```mermaid
graph TD
    A[Start: Topic Input] --> B[Generate Sub-Questions]
    B --> C{Continue to Answers}
    C --> D1[Generate Answer 1]
    C --> D2[Generate Answer 2]
    C --> D3[Generate Answer 3]
    C --> D4[Generate Answer 4]
    C --> D5[Generate Answer 5]
    D1 --> E[Compile Report]
    D2 --> E
    D3 --> E
    D4 --> E
    D5 --> E
    E --> F[Final Report Output]
