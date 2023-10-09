# Summarize Articles with OpenAI GPT-4

Sumz is a user-friendly tool powered by OpenAI's GPT-4, designed to simplify lengthy articles into concise, understandable summaries. It helps users quickly grasp the main points without losing critical information. Sumz leverages GPT-4's advanced language capabilities to make complex content more accessible.

## App UI 
<div style="clear: both;">
  <img src="/src/assets/deploy.png"/>
</div>

## Installation
Follow these steps to install and set up Sumz on your local machine:

Install Dependencies:  
`npm i` **or** `npm install`

Create dotenv file:

`VITE_RAPID_API_KEY=yourapikey`

Run on your local machine:
  
`npm run dev`
# Article Extractor and Summarizer API

This API is designed to extract the body of news articles from a URL and utilize GPT for summarizing the article content.

## Usage via RapidAPI

You can access the API on [RapidAPI](https://rapidapi.com/restyler/api/article-extractor-and-summarizer).

### Example Configuration

Here's an example of how to make a request to the API using Axios:
Replace 'yourapikey' with your actual RapidAPI key .

```js
const axios = require("axios");

const options = {
  method: 'POST',
  url: 'https://article-extractor-and-summarizer.p.rapidapi.com/summarize-text',
  headers: {
    'content-type': 'application/json',
    'X-RapidAPI-Key': 'yourapikey',
    'X-RapidAPI-Host': 'article-extractor-and-summarizer.p.rapidapi.com'
  },
  data: '{"text":"article of markdown text"}'
};

axios.request(options).then(function (response) {
  console.log(response.data);
}).catch(function (error) {
  console.error(error);
});
```
### Usage via RDTK (Rapid Development Toolkit)
Here's how you can configure the request using RDTK:
```js
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

const rapidApiKey = 'yourapikey';

export const articleApi = createApi({
    reducerPath: "articleApi",
    baseQuery: fetchBaseQuery({ 
        baseUrl: "https://article-extractor-and-summarizer.p.rapidapi.com/",
        prepareHeaders: (headers) => {
            headers.set("X-RapidAPI-Key", rapidApiKey);
            headers.set("X-RapidAPI-Host", 'article-extractor-and-summarizer.p.rapidapi.com');
            return headers;
        }
    }),
    endpoints: (builder) =>  ({
        getSummary: builder.query({
            query: (params) => `/summarize?url=${encodeURIComponent(params.articleUrl)}&length=3`
        })
    })
});
```
To adjust the length of the summary, modify the length parameter in the getSummary query:
```js
endpoints: (builder) =>  ({
    getSummary: builder.query({
        query: (params) => `/summarize?url=${encodeURIComponent(params.articleUrl)}&length=3` // Change the length here
    })
})
```