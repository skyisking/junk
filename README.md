gemmyny 

```python
import os
import openai  # Or another LLM library

# Set your API key (environment variable is recommended)
openai.api_key = os.getenv("OPENAI_API_KEY")

def generate_code(prompt, language="python"):
    """Generates code using an LLM."""
    try:
        response = openai.Completion.create(
            engine="text-davinci-003",  # Or a suitable model
            prompt=f"``` {language}\n{prompt}\n```", # Format for code
            max_tokens=500,  # Adjust as needed
            temperature=0.7, # Adjust for creativity vs. accuracy
            n=1,            # Number of code generations
            stop=None,        # Optional stop sequences
        )
        code = response.choices[0].text.strip()
        return code
    except Exception as e:
        return f"Error: {e}"


def save_code(code, filename="generated_code.py"):
    """Saves generated code to a file."""
    try:
        with open(filename, "w") as f:
            f.write(code)
        return f"Code saved to {filename}"
    except Exception as e:
        return f"Error saving code: {e}"


if __name__ == "__main__":
    user_prompt = input("Enter your code description/request: ")
    generated_code = generate_code(user_prompt)

    if generated_code.startswith("Error"):
        print(generated_code)  # Print the error message
    else:
        print("Generated Code:\n", generated_code)
        save_result = save_code(generated_code)
        print(save_result)

```