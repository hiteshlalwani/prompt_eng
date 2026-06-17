# Notes
Prompt Engineering [Notes](https://docs.google.com/document/d/1b7tVvgZukmT3pW0bj-gN2ROyu5OT3HSo9SEfSgJ40RI/edit?tab=t.qu6uanpkkfqo)

# Prompt components

## Role
Ex:
Act as a science communicator writing for a homeowner's blog

Ex:
Prompt: You are 'SupportBot,' a friendly and helpful AI assistant for the e-commerce brand 'Innovate Forward.' Your primary goal is to resolve customer issues by providing accurate information from the company's official knowledge base. You must maintain a polite and professional tone at all times.

## Instruction

Your task is to write a short, engaging paragraph explaining the main benefits of installing solar panels for a homeowner

## Context
--- Key Points to Include ---

- Reduces monthly electricity bills.
- Can increase the home's market value.
- Positive environmental impact by reducing the family's carbon footprint.

--- End Key Points ---

##Output format

Write in an optimistic and accessible tone. Avoid technical jargon. The paragraph should be no more than 100 words.

## Example
```
Prompt: Act as a science communicator writing for a homeowner's blog. Your task is to write a short, engaging paragraph explaining the main benefits of installing solar panels.

Use the following key points in your response:

Reduces monthly electricity bills.
Can increase the home's market value.
Positive environmental impact by reducing the family's carbon footprint.

Write in an optimistic and accessible tone. Avoid technical jargon. The paragraph should be no more than 100 words.
```

## Give clear instruction

- Be specific and add context
- Assign an audience
- Use roles to imply a format
- Specifiy output format clearly to avoid unwanted conversational filler

Here we specified measurable success criteria for prompt:
```
Write a marketing email with a confident and professional tone. The email must highlight three specific benefits of our new software: increased productivity, improved team collaboration, and enhanced data security.
```

Here we specified unambiguous success criteria and audience:
```
Rewrite this paragraph to be approximately 50 words long. The tone should be formal and suitable for a corporate audience.
```

Here we avoided conversation filler:
```
Prompt: Act as a helpful customer service agent. Please read the following email and extract the product SKU. Return only the SKU.
```

Ex: Define task and success criteria:
```
Task: Write a single prompt that instructs an AI to perform the following two tasks based on a customer review:

Classify the sentiment of the review as a single, machine-readable word: Positive, Negative, or Neutral.

Draft a short, empathetic response to the customer, acknowledging their feedback.

Success criteria:

The prompt must successfully instruct the AI to perform both tasks.

The sentiment classification must be a single, clean word with no conversational filler.

The draft response to the customer must have an empathetic and helpful tone.
```

## Give step by step instructions

Ex: Multi step prompt:
```
Perform the following steps:

1. Summarize the provided text in a single paragraph.

2. Translate only the summary into Spanish.

3. Create a bulleted list of all the proper names mentioned in the original text.
```

# Prompt Engineering Template

A standard prompt template combines conversational roles and delimiters for clarity and reliability.
Use delimiters like triple backticks (```), markdown headers (###), or XML tags () within the user prompt to organize content clearly. This structure ensures the AI understands instructions, input data, and output format distinctly.
```
| ### ROLE: SYSTEM \

You are an expert AI assistant specialized in [domain]. Your goal is to [objective]. Follow these rules: [rules].
### ROLE: USER \
[User’s specific input or question]
```
Add "ASSISSTANT" message as well in end so we can demonstrate the exact format and style of the desired output.

Ex:
```
Role: System 

You are 'SupportBot,' a friendly and helpful AI assistant for the e-commerce brand 'Innovate Forward.' Your primary goal is to resolve customer issues by providing accurate information from the company's official knowledge base. You must maintain a polite and professional tone at all times.

﻿﻿﻿﻿﻿﻿﻿﻿﻿Role: User

My order #12345 arrived damaged. What is your return policy?

Role: Assistant (Model's Generated Response)

I'm so sorry to hear that your order arrived damaged. According to our policy, you can get a full refund or a free replacement for any damaged items within 30 days of delivery. I can help you start that process right now.
```

Ex: Here we specify exact output requirement making it more reliable because the model can identify each part of the task
```

Prompt: ### INSTRUCTION ###

Extract the renewal date and the notice period from the legal clause provided below. Provide the output in JSON format.

### LEGAL CLAUSE ###

<clause>

The agreement shall automatically renew on December 31st, 2025, unless either party provides a written notice of non-renewal at least 30 days prior.

</clause>



Response: {

  "renewal_date": "2025-12-31",

  "notice_period_days": 30

}
```

Ex: More detailed instructions:
```
### ROLE: SYSTEM

You are an expert AI code reviewer specializing in Python. Your purpose is to help developers improve their code quality.



### YOUR TASK ###

Review the Python code provided by the user and identify areas for improvement.



### REVIEW CRITERIA ###

You must evaluate the code based on the following three criteria:

1.  **Bugs or Logical Errors:** Identify any code that will not work as intended.

2.  **Style Guide Adherence:** Check if the code follows the official PEP 8 Python style guide.

3.  **Performance:** Suggest any opportunities for performance optimization.



### OUTPUT FORMAT ###

Provide your feedback as a bulleted list, with a separate bullet for each issue you find.



### ROLE: USER

Please review the following Python function:

'''python

def get_names( user_list):

  names=[]

  for user in user_list:

    names.append(user['name'])

  return names
'''
```


