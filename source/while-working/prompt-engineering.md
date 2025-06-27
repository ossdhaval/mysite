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
