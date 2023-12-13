pnpm install ai
llllll

# Recaptcha
RECAPTCHA_SITE_KEY=<recaptcha site key>
RECAPTCHA_SECRET_KEY=<recaptcha secret key>

# Microsoft
MS_AZURE_COGNITIVE_SERVICES_API_KEY=<MS Azure Cognitive Services API Key>
MS_AZURE_COG_SERVICES_ENTITY_LINKING_API_KEY=<MS Azure Entity Linking API Key>
MS_AZURE_COMPUTER_VISION_KEY=<key>

# IBM Watson/Alchemy/etc (note that different IBM services have different auth requirements)
IBM_WATSON_TONE_USERNAME=<IBM Tone API Username>
IBM_WATSON_TONE_PASSWORD=<IBM Tone API Password>
IBM_ALCHEMY_API_KEY=<IBM Alchemy API Key>

# Google NLP
GCLOUD_PROJECT=<Google Cloud Platform Project ID>
GOOGLE_NLP_API_KEY=<API KEY>
GOOGLE_CLOUD_PRIVATE_KEY="<key>"
GOOGLE_CLOUD_EMAIL="888888888-something@developer.gserviceaccount.com"

# Clarifai
CLARIFAI_CLIENT_ID=<token>
CLARIFAI_CLIENT_SECRET=<secret>

# Recast.ai
RECAST_AI_TOKEN=<token>

# API.ai
API_AI_TOKEN=<token>

# Baidu
BAIDU_TRANSLATION_APP_ID=<token>
BAIDU_TRANSLATION_KEY=<token>

# this is enabled for rate limiting on our production environment
REDIS_URL=redis://<Redis location>
RATE_LIMITING_ENABLED=true
RATE_LIMITING_INTERVAL=<interval>
RATE_LIMITING_REQUESTS=<limit>


// ./app/api/chat/route.js
import OpenAI from 'openai';
import { OpenAIStream, StreamingTextResponse } from 'ai';

const openai = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY,
});

export const runtime = 'edge';

export async function POST(req) {
  const { messages } = await req.json();
  const response = await openai.chat.completions.create({
    model: 'gpt-4',
    stream: true,
    messages,
  });
  const stream = OpenAIStream(response);
  return new StreamingTextResponse(stream);
}
lllllll
// ./app/page.js
'use client';

import { useChat } from 'ai/react';

export default function Chat() {
  const { messages, input, handleInputChange, handleSubmit } = useChat();

  return (
    <div>
      {messages.map(m => (
        <div key={m.id}>
          {m.role}: {m.content}
        </div>
      ))}

      <form onSubmit={handleSubmit}>
        <input
          value={input}
          placeholder="Say something..."
          onChange={handleInputChange}
        />
      </form>
    </div>
  );
}

<p align="center">
  <img src="https://susi.ai/static/images/susi-logo.svg" alt="logo" width="35%" />
</p>
<h1 align="center">SUSI.AI Web Application</h1>
<p align="center">
  <a href="https://hosted.weblate.org/engage/susi-ai/?utm_source=widget">
    <img src="https://hosted.weblate.org/widgets/susi-ai/-/chat/svg-badge.svg" alt="Weblate" />
  </a>
  <a href="https://www.codacy.com/app/rishiraj824/susi.ai?utm_source=github.com&utm_medium=referral&utm_content=fossasia/susi.ai&utm_campaign=badger">
    <img src="https://api.codacy.com/project/badge/Grade/db948e1eb4b2457386ba80388e8390cf" alt="Codacy Badge" />
  </a>
  <a href="https://travis-ci.org/fossasia/susi.ai">
    <img src="https://travis-ci.org/fossasia/susi.ai.svg?branch=master" alt="Build Status" />
  </a>
  <a href="https://gitter.im/fossasia/susi_webclient?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge">
    <img src="https://badges.gitter.im/Join%20Chat.svg" alt="Gitter" />
  </a>
  <a href="https://twitter.com/susiai_">
    <img src="https://img.shields.io/twitter/follow/susiai_.svg?style=social&label=Follow&maxAge=2592000?style=flat-square" alt="Twitter Follow" />
  </a>
</p>

-------------

SUSI.AI is an artificial intelligence system, combining pattern matching, internet data, data flow, and inference engine principles. Through some abilities to reflect, it can remember the user input to produce deductions and personalized feedback. Its purpose is to explore the abilities of an artificial companion and to answer the remaining unanswered questions. The SUSI.AI web is a front-end developed for web access of SUSI.


## Communication

Please join our mailing list to discuss questions regarding the project: https://groups.google.com/group/susiai/

Our chat channel is to be found on Gitter: https://gitter.im/fossasia/susi_webchat

## Technology Stack

### Components
* CSS: Styling web pages, html files
* Javascript: Primary programing language
* ReactJS: Javascript library for building User Interfaces
* Redux: Managing global state
* Material-UI: UI library for design system
* styled-components: CSS-in-JS library

## Development
SUSI.AI is written in JavaScript with React. To get started with the code, follow this doc:

- [Project Information](https://github.com/fossasia/susi.ai/blob/master/docs/PROJECT_INFORMATION.md)
- [Architecture](https://github.com/fossasia/susi.ai/blob/master/docs/ARCHITECTURE.md)
- [Recommended Reading](https://github.com/fossasia/susi.ai/blob/master/docs/RECOMMENDED_READING.md)
- [API Keys](https://github.com/fossasia/susi.ai/blob/master/docs/API_KEYS.md)
- [Design](https://github.com/fossasia/susi.ai/blob/master/docs/DESIGN.md)

## Requirements
* node --version >= 6
* yarn --version >= 3

## Local Installation
### Steps
* `git clone <repository-url>` , where `<repository-url>` is the link to the forked repository
* `cd susi.ai`

**Note :** If you want to contribute, first fork the original repository and clone the forked repository into your local machine followed by ```cd``` into the directory
```sh
git clone https://github.com/USERNAME/susi.ai.git
cd susi.ai
```
* Install all the dependencies with `yarn install`
* Start the server with `yarn start`
* Visit your app at [http://localhost:3000](http://localhost:3000).

## Installation with docker
### Steps
* `git clone <repository-url>`, where `<respository-url>` is link to the forked repository
* `cd susi.ai`
```sh
git clone https://github.com/USERNAME/susi.ai.git
cd susi.ai
docker build --tag susi.ai:1.0 .
docker run -p 3000:3000 -d susi.ai:1.0
```
* Visit your app at [http://localhost:3000](http://localhost:3000).

## How to deploy?
[Click Here to read how to deploy](https://github.com/fossasia/susi.ai/blob/master/docs/DEPLOY.md)

## Translations
[Add translations in new language for SUSI.AI Web](https://github.com/fossasia/susi.ai/blob/master/docs/TRANSLATION.md)

## License

This repository is under a GNU LESSER GENERAL PUBLIC LICENSE 2.1.

