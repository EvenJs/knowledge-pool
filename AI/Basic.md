## Prompt

**A prompt has three levers:**

> **System prompt** — who the model is and how it behaves
> **User message** — the actual request
> **Context** — examples, data, conversation history

### Few-shot examples

Show the model what good looks like before asking it to do it:

```python
user = """
Extract name and price from these product descriptions.
Example 1:
Input: "The Nike Air Max retails for $180"
Output: {"name": "Nike Air Max", "price": 180}

Example 2:
Input: "Adidas Ultraboost costs $220"
Output: {"name": "Adidas Ultraboost", "price": 220}

Now extract from this:
Input: "New Balance 990 is priced at $175"
Output:
"""
```

### Chain-of-thought

For reasoning tasks, ask the model to think before answering

```python
# Without CoT — often wrong on complex problems
"Is 1,234,567 divisible by 9?"

# With CoT — forces reasoning steps
"Is 1,234,567 divisible by 9? Think step by step before giving your answer."
```

### Role prompting

```python
system = "You are a senior .NET engineer doing a code review. Be direct and specific. Flag any security issues first."
```

### Negative examples

Tell the model what NOT to do — often more effective than just saying what to do:

```python
system = """
Answer the user's question concisely.
Do NOT start your response with "Certainly!" or "Great question!".
Do NOT repeat the question back before answering.
"""
```

### Output format control

Always specify the exact format you want when you need to parse the output:

```python
system = """
Respond only with a JSON object in this exact structure:
{
  "sentiment": "positive" | "negative" | "neutral",
  "confidence": 0.0 to 1.0,
  "reason": "one sentence"
}
"""
```

prompt caching

## Context

## Agent

## Skills

## Transformer

![Transformer Architecture](/assets/transformer.png)

An attention mechanism identifies relevant token across a text.
embedding -> embedding with positional information
encoder - input -> generate vector
decoder - vector -> string

#### Tokens

chunks of words

### Tokenization

### Embedding

> Embedding is a mapping function that transforms raw data into a continuous, comparable vector space.

guardview

### vector

## Finetuning

## Benchmarks

## LangChain
