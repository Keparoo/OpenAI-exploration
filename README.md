# OpenAI Exploration

Several mini-projects exploring the OpenAI API exploring ideas from the OpenAI bootcamp
ChatGPT, GPT4, DALLE, etc.

## Testing results using the Moderation API

```python
response = openai.Moderation.create(input=”Sample text goes here”)
output = response[“results][0]
```

Endpoint to test whether a prompt violates moderation policies

[OpenAI Moderation](https://platform.openai.com/docs/guides/moderation/)

[OpenAI Usage Policies](https://platform.openai.com/docs/usage-policies)

## Pricing

[OpenAI Pricing](https://openai.com/api/pricing)

GPT-3 (Davinci)

- $0.02 / 1k tokens (approx 750 words)
- [Introduction of ChatGPT 3.5 and Whisper API](https://openai.com/blog/introducing-chatgpt-and-whisper-apis)

GPT-3.5 (gpt-3.5-turbo)

- $0.002 / 1K tokens
- As of 3/1/2023 fine-tuning is not available for the gpt-3.5-turbo models

Whisper (transcription of audio) is now available as an API

- $.006 / minute (rounded to the nearest second)

DALLE-2 (1024x1024 resolution)

- $0.02 / image

Training

- $0.03 / 1k tokens

Usage (Inference)

- $0.12 / 1k tokens

## Text Completion Models as of Feb 2023

[Model Index for Researchers](https://platform.openai.com/docs/model-index-for-researchers)

- Ada (Fastest) $0.0004/1K tokens
- Babbage $0.0005/1K tokens
- Curie $0.002/1K tokens
- Davinci (Most Powerful) $0.02/1K tokens
  - Davinci has code variants: code-davinci-002

## OpenAI Completion Call Parameters

- Model (davinci)
- Prompt
- Temperature
  - Higher values mean the model will take more risks
  - Try 0.9 for more creative application,
  - Try 0 (argmax sampling) for ones with a well-defined answer
  - In the case of simpler tasks with a clear correct answer, lean more toward 0
- Max Tokens
  - The max number of tokens to generate in the completion
  - The token count of your prompt plus max_tokens cannot exceed the model’s context length
  - Most models have a context length of 2048, the newest support 4096
- Top P
  - An alternative to sampling with temperature called nucleus sampling
  - The model considers the results of the tokens with top_p probability mass:
  - 0.1 means only consider the tokens comprising the top 10% probability mass.
  - Use Top P or Temperature but not both
- N
  - How many completions to generate for each prompt
  - This is the same as running the same prompt multiple times, so it is more expensive
  - We will pretty much always set this to 1 indicating we want 1 completion
  - This should only be used if the temp is set above zero
  - Multiple completions with a 0 Temp should generate the same result
- Frequency Penalty
  - Number between -2.0 and 2.0
  - Positive values penalize new tokens based on their existing frequency in the text
  - Positive values reduce the likelihood of the completion repeating itself
- Presence Penalty
  - Number between -2.0 and 2.0
  - Positive values penalize new tokens based on whether they appear in the text so far
  - This will increase the mode’s likelihood to talk about new topics
  - High numbers of Freq/Pres can lead the completion to go off track

Presence and Frequency Penalties: The presence penalty is a one-off additive contribution that applies to all tokens that have been sampled at least once and the Frequency penalty is a contribution that is proportional to how often a particular token has already been sampled. Reasonable values of either are between 0.1 and 1 if the aim is to just reduce repetitive samples somewhat. Negative values will increase the likelihood of repetition.

## Engines have been deprecated and replaced with models (Retrieve, Completion, Chat, etc.)

[Models List](https://platform.openai.com/docs/api-reference/models/list)

## Testing in the playground

[Playground](https://platform.openai.com/playground)

## Beware of prompt leakage or prompt reverse engineering

[Prompt reverse engineering](https://lspace.swyx.io/p/reverse-prompt-eng)

## Prompt Design

- **Model**:  
  the latest will give the best results

- **Instructions**:  
  Put instructions at the beginning of a prompt and use ### or “”” to separate out instructions from the desired output

```bash
Summarize the text below into bullet points.

Text: “””
{some text}
“””
```

- **Detail**:  
  instead of write a poen about OpenAI, “Write a poem about OpenAI in the style of a Haiku, make sure to only write 3 lines and focus on GPT.

- **Examples**:

```bash
Extract the first and last names from the text below:

Desired format:
Last Name, First Name
{some text}
```

- **Be Direct**:  
  Create a 3 to 5-sentence description about the product in the text below: {some text}

- **Initiate the Response**:

```bash
Instead of: Write a python function to scrape the wikipedia page on the world’s tallest buildings.
Try: The python function below scrapes Wikipedia to return a CSV of the world’s tallest buildings and their stats.

def scrape_wiki(
or start with import
```

[OpenAI Prompt Design Guide](https://platform.openai.com/docs/guides/completion/prompt-design)
