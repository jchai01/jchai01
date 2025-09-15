+++ 
date = 2025-09-13T18:58:49+01:00
title = "Using AG-UI with Google Gemini"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

Example from AG-UI only shows chatGPT as the base model, which isn't free.

```
./agent/.env:
GOOGLE_API_KEY=your_api_key
```

activate the .venv file inside `agent` folder then install:
`pip install -U langchain-google-genai`

Under agent.py. add the following:

```python
from langchain.chat_models import init_chat_model

# 1. Define the model
# model = ChatOpenAI(model="gpt-4o")
model = init_chat_model("google_genai:gemini-2.0-flash")

```
