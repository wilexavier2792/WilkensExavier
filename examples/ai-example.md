# Example: Working with AI

This file shows a simple, practical example of using an AI assistant (chat model) to help with development tasks. It's intended as a quick-start example you can adapt for your own workflows.

## Purpose
- Demonstrate a minimal example of calling an AI model from code.
- Show an example prompt and how to verify/validate outputs.
- Include safety and best-practice notes.

---

## Quick Python example (using OpenAI-style client)

Install the official client (example):

```bash
pip install openai
```

Simple script:

```python
import os
import openai

# Set your API key in the environment: export OPENAI_API_KEY="sk-..."
openai.api_key = os.environ.get("OPENAI_API_KEY")

prompt = '''You are an assistant that writes a short, well-documented Python function.
Task: Implement a function `is_prime(n)` that returns True if n is a prime number, False otherwise.
Constraints: Keep it simple and include a short docstring.''' 

resp = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[{"role": "user", "content": prompt}],
    max_tokens=300,
)

assistant_text = resp['choices'][0]['message']['content']
print("--- AI output ---")
print(assistant_text)
```

Note: API names and client libraries evolve. Replace the client call with the one matching your installed SDK and model access.

---

## Example prompt (what to ask)
- Be explicit about the task, constraints, and expected output format.
- Ask the model to provide tests or examples for verification.

Example:

"""
Write a function `is_prime(n)` in Python (include docstring). Also provide 5 unit tests using `assert` showing expected behavior.
"""

---

## Validation and safety
- Do not assume AI code is correct; always run and test generated code.
- Inspect generated code for security issues (injection, unsafe eval, network calls).
- Prefer small, testable outputs and request unit tests from the model.

---

## Tips
- Use temperature=0 (deterministic) for reproducible code snippets.
- Ask the model to explain its reasoning or to add comments for readability.
- Pin model and library versions in your project to avoid breaking changes.

---

If you'd like, I can:
- Add this example as a README section, or
- Add an executable example in `examples/` with tests and a CI job that runs the example.
