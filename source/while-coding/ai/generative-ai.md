# Generative AI for Everyone

Reference: https://www.coursera.org/learn/generative-ai-for-everyone/home/welcome

downloaded Cource slides at: /home/dhaval/docs/learning/tech/learning material/ai/Generative-ai-for-everyone


## important terms:

- Knowledge cutoff: Most recent Time/date when model's training data was updated.

## mental notes:

- Normal NLP vs LLM based gen ai project
  - In normal NLP project,
    1. you label the data
    2. and then train your neural network(model)
    3. and then you build your application that calls that model and passes a parameter
  - In LLM based project, there can be two types
    1. you directly build an application (step-3 above) to call a pretrained ai model (like chatgpt, perplexity etc). Because of this, building LLM based application is very fast and easy. And that is because lot of people are creating such applications that are just wrappers on top of an third-party LLM.
    2. You can take an LLM, and improve it for your usecase using RAG, model fine-tuning, pretrain models. This takes some efforts but has more value

- What is a token:
  Token doesn't always mean a single `word`. It is how LLM considers a word. For example, common words like `the example` may be considered to be a single token. While words like `programming` might be considered as two tokens (`program`+`ming`). So, on the average `1 token` = `3/4 of a word`. So for 300 words would roughly equal to 400 tokens.
- LLM charges: LLM models like chatGPT and others charge different rates for input tokens and output tokens. For example, price for input would be 0.0001$/1k tokens, while output is usually costlier like 0.002$/1k tokens. With this rate, it takes 0.08$ to create 40k tokens. 40k tokens is enough reading material for one adult for an hour. So, overall, using 3rd party LLMs is cheap.

- think of LLM as a reasoning engine in addition to knowing lot of things. This way of thinking will expand the usecases where LLMs can be used. Future uses of LLMs will be leveraging reasoning capabilities more than knowledge bank.
- My note: So LLM = Reasoning engine + data store(RAG etc)
