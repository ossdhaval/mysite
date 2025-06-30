Course: https://www.coursera.org/learn/essentials-of-prompt-engineering/


A prompt's form depends on the task that you are giving to a model. As you explore prompt engineering examples, you will review prompts containing some or all of the following elements:

• Instructions: This is a task for the large language model to do. It provides a task description or instruction for how the model should perform.

• Context: This is external information to guide the model.

• Input data: This is the input for which you want a response.

• Output indicator: This is the output type or format.

Sample prompt:

``` 

Given a list of customer orders and available inventory, determine which orders can be fulfilled and which items have to be restocked.

This task is essential for inventory management and order fulfillment processes in ecommerce or retail businesses.

Orders:
Order 1: Product A (5 units), Product B (3 units)
Order 2: Product C (2 units), Product B (2 units)

Inventory:
Product A: 8 units
Product B: 4 units
Product C: 1 unit

Fulfillment status:
```

The previous prompt includes all four elements of a prompt. You can break the prompt into the following elements:

• Instructions: Given a list of customer orders and available inventory, determine which orders can be fulfilled and which items have to be restocked.

• Context: This task is essential for inventory management and order fulfillment processes in ecommerce or retail businesses.

• Input data:

Orders:

Order 1: Product A (5 units), Product B (3 units)
Order 2: Product C (2 units), Product B (2 units)

Inventory:

Product A: 8 units
Product B: 4 units
Product C: 1 unit

• Output indicator: Fulfillment status: 


#### Negative prompting

Tell model what not to do. For instance, in a text generation model, negative prompts could be used to prevent the model from 
producing hate speech, explicit content, or biased language.

#### Model parameters

Temperature:

This parameter controls the randomness or creativity of the model's output. A higher temperature makes the output more diverse and unpredictable, and a lower temperature makes it more focused and predictable. Temperature is set between 0 and 1. The following are examples of different temperature settings.


-  Low temperature (for example, 0.2)	
    -  Outputs are more conservative, repetitive, and focused on the most likely responses.
-  High temperature (for example, 1.0)
    -  Outputs are more diverse, creative, and unpredictable, but might be less coherent or relevant.

TOP P:

Top p is a setting that controls the diversity of the text by limiting the number of words that the model can choose from based on their probabilities. Top p is also set on a scale from 0 to 1. The following are examples of different top p settings.

- Low top p (for example, 0.250)	
    - With a low top p setting, like 0.250, the model will only consider words that make up the top 25 percent of the total probability distribution. This can help the output be more focused and coherent, because the model is limited to choosing from the most probable words given the context.
- High top p (for example, 0.990)
    - With a high top p setting, like 0.990, the model will consider a broad range of possible words for the next word in the sequence, because it will include words that make up the top 99 percent of the total probability distribution. This can lead to more diverse and creative output, because the model has a wider pool of words to choose from.

Top K:

Top k limits the number of words to the top k most probable words, regardless of their percent probabilities. For instance, if top k is set to 50, the model will only consider the 50 most likely words for the next word in the sequence, even if those 50 words only make up a small portion of the total probability distribution.


- Low top k (for example, 10)	
    - With a low setting, like 10, the model will only consider the 10 most probable words for the next word in the sequence. This can help the output be more focused and coherent, because the model is limited to choosing from the most probable words given the context.
- High top k (for example, 500)
    - With a high top k setting, like 500, the model will consider the 500 most probable words for the next word in the sequence, regardless of their individual probabilities. This can lead to more diverse and creative output, because the model has a larger pool of potential words to choose from.

Length:

The length inference parameter category refers to the settings that control the maximum length of the generated output and specify the stop sequences that signal the end of the generation process. To learn more, choose each of the following parameters.

    - Maximum length
        The maximum length setting determines the maximum number of tokens that the model can generate during the inference process. This parameter helps to prevent the model from generating excessive or infinite output, which could lead to resource exhaustion or undesirable behavior. The appropriate value for this setting depends on the specific task and the desired output length. For instance, in natural language generation tasks like text summarization or translation, the maximum length can be set based on the typical length of the target text. In open-ended generation tasks, such as creative writing or dialogue systems, a higher maximum length might be desirable to allow for more extended outputs.

How to give these parameters to chatgpt:

![image](https://github.com/user-attachments/assets/2fe87700-0fec-4dec-b22c-d59ffdb51c75)


Adjusting these inference parameters can significantly impact the model's output, so you can fine-tune the level of creativity, diversity, and coherence to suit your specific needs.

#### Good bad prompt examples:

- Stay clear and consice:

Prompts should be straightforward and avoid ambiguity. Clear prompts lead to more coherent responses. 
Craft prompts with natural, flowing language and coherent sentence structure. Avoid isolated keywords and phrases.

  -  bad prompt

    - Compute the sum total of the subsequent sequence of numerals: 4, 8, 12, 16.

  - Good prompt:

    - What is the sum of these numbers: 4, 8, 12, 16?

- Include context if needed.

  Provide any additional context that would help the model respond accurately.
  For example, if you ask a model to analyze a business, include information about the type of business. What does the company do?
  This type of detail in the input provides more relevant output. The context that you provide can be common
  across multiple inputs or specific to each input.

  - Bad prompt

    -  Summarize this article: [insert article text]


  - Good prompt

    -  Provide a summary of this article to be used in a blog post: [insert article text]
   
-  Use directives for the appropriate response type.

   If you want a particular output form, such as a summary, question, or poem, specify the response type directly.
    You can also limit responses by length, format, included information, excluded information, and more.

  -  Bad prompt

      - What is the capital?

  -  Good prompt

      - What is the capital of New York? Provide the answer in a full sentence.

- Consider the output in the prompt.

  Mention the requested output at the end of the prompt to keep the model focused on appropriate content.

  -  Bad prompt

      - Calculate the area of a circle.

  -  Good prompt

      - Calculate the area of a circle with a radius of 3 inches (7.5 cm). Round your answer to the nearest integer.

 - Provide an example response.

    Use the expected output format as an example response in the prompt. Surround it in brackets to make it clear that it is an example.

   - Bad prompt

      Determine the sentiment of this social media post: [insert post]

   -  Good prompt

        Determine the sentiment of the following social media post using these examples:
      
        post: "great pen" => Positive
      
        post: "I hate when my phone battery dies" => Negative
      
        [insert social media post] =>

- Break up complex tasks.

  Foundation models can get confused when asked to perform complex tasks. Break up complex tasks by using the following techniques:

    - Divide the task into several subtasks. If you cannot get reliable results, try splitting the task into multiple prompts.
    - Ask the model if it understood your instruction. Provide clarification based on the model's response.
    - If you don’t know how to break the task into subtasks, ask the model to think step by step. You will learn more about this type of prompt technique later on in this course. This method might not work for all models, but you can try to rephrase the instructions in a way that makes sense for the task. For example, you might request that the model divides the task into subtasks, approaches the problem systematically, or reasons through the problem one step at a time.

- Experiment and be creative.

    Try different prompts to optimize the model's responses. Determine which prompts achieve effective results and which prompts achieve inaccurate results. Adjust your prompts accordingly. Novel and thought-provoking prompts can lead to innovative outcomes.

- Use prompt templates.

  Prompt templates are predefined structures or formats that can be used to provide consistent inputs to FMs. They help ensure that the prompts are phrased in a way that is easily understood by the model and can lead to more reliable and higher-quality outputs. Prompt templates often include instructions, context, examples, and placeholders for information relevant to the task at hand.

  Prompt templates can help streamline the process of interacting with models, making it easier to integrate them into various applications and workflows.


### Techniques

#### Zero-shot prompting

Zero-shot prompting is a technique where a user presents a task to a generative model without providing any examples or explicit training for that specific task. In this approach, the user relies on the model's general knowledge and capabilities to understand and carry out the task without any prior exposure, or shots, of similar tasks. Remarkably, modern FMs have demonstrated impressive zero-shot performance, effectively tackling tasks thatthey were not explicitly trained for.

Example:

Tell me the sentiment of the following social media post and categorize it as positive, negative, or neutral:

Huge shoutout to the amazing team at AnyCompany! Your top-notch customer service continues to blow me away. Proud to be a loyal customer!

Note that this prompt did not provide any examples to the model. However, the model was still effective in deciphering the task.

#### Few-shot prompting

Few-shot prompting is a technique that involves providing a language model with contextual examples to guide its understanding and expected output for a specific task. In this approach, you supplement the prompt with sample inputs and their corresponding desired outputs, effectively giving the model a few shots or demonstrations to condition it for the requested task. Although few-shot prompting provides a model with multiple examples, you can also use single-shot or one-shot prompting by providing just one example.

Example:

```
Tell me the sentiment of the following news headline and categorize it as positive, negative, or neutral. Here are some examples:

Investment firm fends off allegations of corruption
Answer: Negative

Local teacher awarded with national prize
Answer: Positive


Community organization exceeds fundraising goal, to provide meals for thousands in need

Answer:

```

#### Chain-of-thought (CoT) prompting 

is a technique that divides intricate reasoning tasks into smaller, intermediary steps. This approach can be employed using either zero-shot or few-shot prompting techniques.  CoT prompts are tailored to specific problem types. To initiate the chain-of-thought reasoning process in a machine learning model, you can use the phrase "Think step by step." It is recommended to use CoT prompting when the task requires multiple steps or a series of logical reasoning.

Example:

prompt:

```
Which service requires a larger deposit based on the following information?

The total cost of service A is $50,000, and it requires a 30 percent deposit.

The total cost of service B is $40,000, and it requires a 40 percent deposit.

Think step by step.

```

Response:

```
The deposit for service A is 30 percent of $50,000, which is
0.3 * 50,000 = $15,000



The deposit for service B is 40 percent of $40,000, which is
0.4 * 40,000 = $16,000



Therefore, based on the given information, service B requires a larger deposit.
```

==================== end of course ==================================================


#### helpful words to be used in a prompts

- actionable: “Give me an actionable summary of this article for someone who needs to make decisions.”
- concise: “Write a concise explanation of this product for a beginner.”
- insightful: “Give me an insightful review of this trend and what it means for consumers.”
- simplified: “Simplify this news article so a 12-year-old could understand it.”
- bullet-pointed: “Summarize this podcast episode in bullet points with timestamps.”
- prioritized: “List the top 3 takeaways from this report, prioritized by impact.”
- stategic: “Give me a strategic summary of this competitor’s product launch.”
- persuasive: “Write a persuasive pitch for this eco-friendly water bottle.”
- comparative: “Compare Claude and ChatGPT in a table showing strengths and weaknesses.”
- contextual: Give me a contextual overview of this legislation and who it affects.”
- visual: “Give me a visual summary of this market research in table form.”

#### 3 word rule

`Like a lawyer`
`Like a journalist`
`Like a 8 year old`

These three words can instantly shape the tone, voice and depth of the output.

Tell chatgpt how the response should be writen. This sets tone, structure and depth etc and responses will be better.

- “Summarize this article like a journalist”
- “Explain dark matter like a physics professor”
- “Give me career advice like a mentor”
- “Translate this email like a professional diplomat”
- “Write a poem like a Nashville songwriter”
- “Design a pitch deck like a Silicon Valley founder”
- “Review this document like a detail-oriented lawyer”
- “Brainstorm ideas like a Gen Z influencer”
- “Ask me questions like a therapist would”
- “Rewrite this paragraph like an editor at The Atlantic”
- “Give me feedback like a startup investor”
- “Summarize this book like a 10th grade English teacher”
- “Critique this image like an art historian”
- “Plan a vacation like a travel agent on a budget”
- “Explain this concept like I’m five”
- “Pitch this idea like a TED Talk speaker”

#### Prompt dusting

Use multiple chat bots (chatgpt, claude, perplexity etc) using the same prompt and combine the result 

https://www.tomsguide.com/ai/this-game-changing-ai-trick-is-the-secret-to-getting-the-best-chatbot-results

#### which bot is better at what

- ChatGPT (GPT-4o): Excellent for writing, summarizing, organizing thoughts and tone matching. Great at step-by-step logic and structure.
- Claude 3.7 Sonnet: Amazing at nuance, emotional intelligence and digesting long documents. Feels like a gentle co-thinker.
- Gemini 2.0: Strong at pulling in Google Search info, perfect for travel planning, event discovery and integrating with your calendar or Gmail.
- Perplexity AI: My go-to for source-backed research, current news and citations.
- Groq 3: Blazing fast. Ideal for logic puzzles, short answers or coding.
- DeepSeek: Surprisingly sharp at multimodal reasoning, good with charts, graphs and solving math problems step-by-step.
