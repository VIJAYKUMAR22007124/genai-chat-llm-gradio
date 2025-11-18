## Development and Deployment of a 'Chat with LLM' Application Using the Gradio Blocks Framework

### AIM:
To design and deploy a "Chat with LLM" application by leveraging the Gradio Blocks UI framework to create an interactive interface for seamless user interaction with a large language model.

### PROBLEM STATEMENT:
This program uses the FalconLM model through a HuggingFace text-generation API to produce text completions.Users provide a prompt and choose the maximum number of tokens to control the length of the response.A Gradio interface is used to generate and display the model’s output interactively.
### DESIGN STEPS:

#### STEP 1:
The program loads environment variables, initializes the FalconLM client using the HuggingFace API, and sets up the text-generation function.
#### STEP 2:
When the user enters a prompt and selects the maximum number of new tokens, the model generates text using the client.generate() method.
#### STEP 3:
The generated output is displayed in a Gradio interface as the completion result.

### PROGRAM:
```
import os
import io
import IPython.display
from PIL import Image
import base64 
import requests 
requests.adapters.DEFAULT_TIMEOUT = 60

from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv()) # read local .env file
hf_api_key = os.environ['HF_API_KEY']
# Helper function
import requests, json
from text_generation import Client

#FalcomLM-instruct endpoint on the text_generation library
client = Client(os.environ['HF_API_FALCOM_BASE'], headers={"Authorization": f"Basic {hf_api_key}"}, timeout=120)
#Back to Lesson 2, time flies!
import gradio as gr
def generate(input, slider):
    output = client.generate(input, max_new_tokens=slider).generated_text
    return output

demo = gr.Interface(fn=generate, 
                    inputs=[gr.Textbox(label="Prompt"), 
                            gr.Slider(label="Max new tokens", 
                                      value=20,  
                                      maximum=1024, 
                                      minimum=1)], 
                    outputs=[gr.Textbox(label="Completion")])

gr.close_all()
demo.launch(share=True, server_port=int(os.environ['PORT1']))
```

### OUTPUT:
<img width="688" height="430" alt="image" src="https://github.com/user-attachments/assets/dd37a3e9-55ca-4f75-85f9-3b0b8d2f2543" />


### RESULT:
The system successfully generates coherent and context-aware text based on the user’s prompt.It provides an easy and interactive way to control output length and view AI-generated responses in real time.
