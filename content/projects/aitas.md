---
title: "Artificial Intelligence - Teaching Assistant System (AI-TAS)"
date: 2024-08-08T20:53:21+01:00
---

An chatbot with an interactive 3D avatar, build for a research project in NUS with the goal to increase engagement. Used for the module "Leadership & Management".

# Frontend

- HTML, CSS & JS.

# Backend

- NodeJS Express server.
- MongoDB.
- WebSocketIO, enable real-time interaction.
- RASA, open source conversational AI framework.
- FastAPI, serves response from RASA.
- AWS Sumerian Host: 3D model and animation.
- AWS Polly, text-to-Speech (TTS) feature.

# Notes

AWS Polly isn't free and could potentially charge my credit card if the API usage exceeds free tier. Need to find a way to decouple AWS Sumerian and AWS Polly, ideally an open source TTS system that works with AWS Sumerian, seems quite [tightly integrated](https://stackoverflow.com/questions/73649019/how-do-i-integrate-aws-sumerian-host-without-the-use-of-aws-polly/76657529#76657529) for now.
