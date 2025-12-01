# prompt_prompting
An adaptive multi-agent system that improves user prompt-writing skills through practice, evaluation, coaching, and personalized learning paths.
Problem Statement — the problem you're trying to solve, and why it matters

Large Language Models are now part of everyday workflows, but most people still struggle to get the output they want. The root cause is not the model — it’s the prompt. Many users give unclear, vague, or incomplete instructions, which leads to incorrect answers, hallucinations, or wasted time. Despite increasing reliance on AI systems, there is no structured and adaptive way for beginners to learn how to prompt effectively.

PromptCraft addresses this by providing a guided, measurable, and agent-powered workflow for users to practice prompt-writing, receive feedback, and improve rapidly. Instead of static tutorials or one-time examples, PromptCraft treats prompting as a skill that strengthens over repeated practice.

Why agents? — Why agents are the right solution for this problem

Prompt engineering is inherently iterative: users attempt a prompt, see the output, refine it, and try again. This cycle is perfectly suited for an agentic design.

PromptCraft uses multiple agents working together:

Executor Agent — sends the user’s prompt to the LLM and captures output

Evaluator Agent — scores the output using deterministic tests or similarity metrics

Coach Agent — rewrites and explains improved prompts using an LLM

Memory Agent — stores attempts, weaknesses, improvements, and progress

Planner Agent — selects the next lesson based on past performance

Agents make the system adaptive, interactive, and self-improving, allowing the user to have a learning experience tailored exactly to their weaknesses. This agent-driven workflow is something a static tutorial cannot provide.

What you created — overall system architecture

PromptCraft is a lightweight agentic tutor built around the Practice → Evaluate → Coach → Improve loop.

System Architecture

User Interface (Notebook or UI Layer)
The user selects a task and writes a prompt.

Executor Agent
Takes the prompt and sends it to an LLM (OpenAI or Gemini) via a wrapper.

Evaluator Agent
Evaluates output using:

Unit tests (for code tasks)

Embedding similarity (for text tasks)

Exact match scoring (for Q&A tasks)

Coach Agent
Produces:

A short diagnosis of what the user did incorrectly

Two improved prompts: Strong Version and Concise Version

A short list of changes in reasoning

Memory Agent (SQLite)
Stores:

Prompts

Scores

Errors

Coach suggestions

Timestamped progress

Planner Agent
Uses memory to decide:

Which task the user should attempt next

Whether to increase or decrease difficulty

When to revisit weak areas

This modular architecture allows the system to grow: more tasks, more evaluation styles, more UI components.Demo — Showing the solution in action

A typical user session works like this:

User writes a vague prompt like:
“Write is_prime quickly.”

Executor Agent sends it to the LLM.

Evaluator Agent tests the generated code.
For a weak prompt, the code may fail multiple unit tests.

Coach Agent generates feedback such as:
Diagnosis:
“Prompt is vague; does not specify edge cases or function format.”

Strict Prompt:
“Write a Python function is_prime(n) that returns True only if n is prime. Include edge cases (n<=1). Provide only code.”

User runs the strict prompt again.
This time output passes all unit tests.

Progress chart shows the improvement from 0% → 100%.

This demonstrates measurable learning rather than subjective feedback.

The Build — Tools and technologies used
Backend / Core Logic (Notebook & Python)

Python 3.10

SQLite for memory storage

Matplotlib for progress visualization

Regex and JSON parsing for extracting structured LLM outputs

Custom unit test runner for deterministic scoring

Cosine similarity for text tasks (optional extension)

LLM Providers

OpenAI GPT-4o / GPT-4o-mini (API)

Optional: Google Gemini models (via google-genai)

Agent Logic

Fully implemented inside the notebook with modular functions

Uses agent-like roles (Executor, Evaluator, Coach, Memory, Planner)

Deployment Plan (Optional)

Hugging Face Spaces (Gradio UI)

Allows judges to interactively try the system

Keeps notebook for reproducibility
