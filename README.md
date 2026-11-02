### AIM:
To design and implement a Python function for calculating the volume of a cylinder, integrate it with a chat completion system utilizing the function-calling feature of a large language model (LLM).

### PROBLEM STATEMENT:

### DESIGN STEPS:

#### STEP 1:nstall and import the required Python libraries.

#### STEP 2:Define the pentagon area calculation function and tool.

#### STEP 3:Execute the function using OpenAI API and display the calculated area.

### PROGRAM:
## Name: Priyadharshini S
### Reg no: 212225230218
```
import os
import json
import math
from dotenv import load_dotenv, find_dotenv
from openai import OpenAI

# Load API key
load_dotenv(find_dotenv())
client = OpenAI(api_key=os.environ["OPENAI_API_KEY"])

# Define the mathematical function
def calculate_pentagon_area(side):
    """Calculate the area of a regular pentagon."""

    area = (1 / 4) * math.sqrt(
        5 * (5 + 2 * math.sqrt(5))
    ) * side**2

    return json.dumps({
        "side": side,
        "area": round(area, 2)
    })

# Define the tool
tools = [
    {
        "type": "function",
        "name": "calculate_pentagon_area",
        "description": "Calculate the area of a regular pentagon",
        "parameters": {
            "type": "object",
            "properties": {
                "side": {"type": "number"}
            },
            "required": ["side"],
            "additionalProperties": False
        },
        "strict": True
    }
]

# Ask the question
response = client.responses.create(
    model="gpt-5.5",
    input="Calculate the area of a regular pentagon with side length 5.",
    tools=tools,
    tool_choice="required"
)

# Process the tool call
for item in response.output:
    if item.type == "function_call":
        args = json.loads(item.arguments)

        result = calculate_pentagon_area(**args)

        print("Function arguments:", args)
        print("Calculated area:", result)
```

### OUTPUT:
<img width="1063" height="726" alt="Screenshot 2026-11-02 133059" src="https://github.com/user-attachments/assets/788edb14-227c-4b0f-ab96-21aca71a8abf" />


### RESULT:
The Python program successfully calculates the area of a regular pentagon using OpenAI function calling.
