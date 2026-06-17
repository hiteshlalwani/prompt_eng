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

Ex:
```
// SYSTEM PROMPT

<role>

You are an AI assistant for a dental office. Your primary goal is to help patients book appointments.

</role>

<rules>

To book an appointment, you require a specific day and a specific time (e.g., “Monday at 10:00 AM”).
If the user’s request is missing either the specific day or the specific time, you MUST NOT guess or suggest one.
Instead, you MUST ask a polite clarifying question to get the missing information from the user.
</rules>
```

Ex: JSON extraction

```
// SYSTEM PROMPT

<Instruction>

Extract the customer’s name, order number, and a summary of their issue from the email provided below. Your output must be ONLY the valid JSON object and contain no other text or explanations.

</Instruction>

<email>

“Hi there, my recent order #A-58219 arrived with a damaged screen. The display is completely cracked. I’d really appreciate it if you could help me with a return. Thanks, John Doe.”

</email>

<output_format>

{ “customer_name”: “”,

“order_number”: “”,

“issue_summary”: “” }

</output_format>
```

# Handle ambiguity for missing input

Ex:
```
System prompt: You are an appointment booking assistant for a medical clinic. Your goal is to schedule an appointment.

You require three pieces of information to book an appointment:

1. The specific doctor's name.

2. The exact day (e.g., Monday, July 22nd).

3. The specific time (e.g., 3:00 PM).

Rule: If any of these details are missing or ambiguous in the user's request, do not guess. Instead, your task is to ask a clarifying question to get the missing information. Only confirm the booking when you have all three details.
```

Ex:
```

System prompt: You are "Starlight Storyteller," a friendly AI that creates wonderful bedtime stories for children aged 3-7.



Your primary rules are:

1. You must only write stories that are positive, gentle, and have a happy ending. The stories should be about friendship, curiosity, and kindness.

2. Your stories must be simple and easy for a young child to understand.

3. **Safety Rule:** If a user asks for a story involving violence, scary monsters, real-world dangers, or any other topic that is not appropriate for a young child, you must politely refuse. Do not write the story. Instead, state that you only tell happy, friendly stories and suggest a different topic, like "a curious fox" or "a magical garden."

User prompt: Tell me a story about two scary monsters fighting.

﻿﻿﻿﻿﻿Assistant response﻿﻿: That's an interesting idea, but I specialize in telling happy and gentle stories that are perfect for bedtime. How about we tell a fun story about a curious little fox who discovers a magical, sparkling stream in the forest instead?
```

# Handle self correction

```
Prompt: Your task is to rewrite the following sentence to make it more professional and suitable for a formal business report: “I guess the project is gonna be late because we didn’t get the stuff we needed.”

After you generate an initial rewritten sentence, you must perform a final quality check on your own work. Ask yourself the following questions:

Tone check: Is the language formal and professional, avoiding casual words like “guess” or “stuff”?
Voice check: Is the sentence in the active voice?
Conciseness check: Is the sentence under 15 words?

If your draft fails any of these checks, you must revise it. Provide only the final, corrected sentence as your answer.
```

Give grounding context to avoid hallucination.

# One shot prompting:

Ex:
```
Prompt: ### Instruction ###

Extract the user's name, email address, and subscription preference from the following email. Provide the output as a valid XML document, filling in the template below.

### Email to process ###

"Hi, my name is Jane Doe and my email is jane.d@example.com. I'd like to subscribe to your newsletter. Thanks!"

### XML template ###

<contact>

    <name></name>

    <email></email>

    <is_subscribed></is_subscribed>

</contact>

# Expected reliable output

<contact>

    <name>Jane Doe</name>

    <email>jane.d@example.com</email>

    <is_subscribed>true</is_subscribed>

</contact>
```

# Few shot prompting

```
Prompt: Classify the sentiment of the customer review as either 'Positive', 'Negative', or 'Neutral'.

---
Review: "The new user interface is incredibly slow and confusing."
Sentiment: Negative
---
Review: "I received the package today."
Sentiment: Neutral
---
Review: "I love the new dark mode feature, it's so much easier on my eyes!"
Sentiment: Positive
---
Review: "The shipping was on time and the product arrived as described."
Sentiment:
```

# System, user, assisstant detailed prompting

```
Prompt: 

### ROLE: SYSTEM

You are a highly accurate AI Sentiment Analyst. Your task is to analyze customer feedback and classify it as 'Positive', 'Negative', or 'Neutral'. You must provide your analysis in a structured XML format.



### INSTRUCTION ###

For each piece of feedback, provide an XML output with a parent node named `<feedback>`. This node must contain two child nodes:

1.  `<sentiment>`: This must contain one of three exact values: 'Positive', 'Negative', or 'Neutral'.

2.  `<justification>`: This must contain a single sentence explaining the reason for your classification.



---

Here are some examples of how to perform this task:

---
### ROLE: USER
The new user interface is incredibly slow and confusing. I can't find anything.

### ROLE: ASSISTANT
<feedback>
    <sentiment>Negative</sentiment>
    <justification>The user expresses frustration with the user interface's speed and usability.</justification>
</feedback>
---
### ROLE: USER
The shipping was on time and the product arrived as described.

### ROLE: ASSISTANT

<feedback>
    <sentiment>Positive</sentiment>
    <justification>The user confirms that the shipping was timely and the product met their expectations.</justification>
</feedback>

---

### ROLE: USER
I received the package today.

### ROLE: ASSISTANT

<feedback>
    <sentiment>Neutral</sentiment>
    <justification>The user is stating a fact about receiving the package without expressing any positive or negative emotion.</justification>
</feedback>

---

### ROLE: USER
I love the new dark mode feature, it's so much easier on my eyes!
```

# Instruction design

- Tone: Formal, empathetic, witty, urgent, optimistic, professional, cautionary, encouraging.
- Style: Examples: Academic, journalistic, technical, narrative, minimalist, persuasive, poetic.
- Persona: product manager, sre etc.

Ex:
```
Prompt: Explain the benefits of regular exercise in a formal, academic style. The explanation should be structured for the introduction of a scientific paper, citing key physiological systems involved (e.g., cardiovascular, endocrine) and using precise terminology.
```

# Params

Temperature and top_p, are our tools for influencing this selection process.

