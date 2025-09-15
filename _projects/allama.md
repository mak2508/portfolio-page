---
layout: page
title: Allama
description: RAG-based chatbot for Qatar Government
# img: assets/img/3.jpg
importance: 2
category: work
---

[Allama](https://allama.ai/) is a GPT-based chatbot where you can ask questions about Qatar government services. It was built using [LangChain](https://www.langchain.com/) on data pulled from [Hukoomi](https://hukoomi.gov.qa/en/) and other Qatar Ministry data.

However, the primary contribution of Allama is not just a chatbot, but rather an infrastructure for easily deploying GPT based chatbot using publicaly available datasets. Allama was designed in a modular fashion, with a pipleine to continuually collect updated data, connected through a backend server to a frontend chat interface.

We will first discuss the treatment of data by Allama. We make use of a cron job (periodic task) using [celery workers](https://docs.celeryq.dev/en/stable/getting-started/introduction.html) to crawl data from a website specified in the crawling worker. In the document crawler, the job is set up to download/scrape desired data from a certain domain. The worker will be invoked at a configured periodicity, where it will check for new data on the specified domain. In the case of [Hukoomi](https://hukoomi.gov.qa/en/), we check the date of the posts to see if there are any new posts, and keep downloading articles until we arrive at a post that has been already downloaded. In the case of a different webpage, a different check might be make more sense. The crawler then adds a parsing task for each newly downloaded document.

The parse tasks are picked up by the parsing worker, which filters out irrelevant parts of the downloaded document as setup by the user. The filtered document is sent to the chunker through redis once again.

This is in fact the only part of the entire codebase that needs to be adapted to set up a new chatbot for a new data source. You need to configure a crawler to download the latest data periodically and a parser to extract the useful sections of the downloaded data. The rest of the pipeline, namely chunking, embedding, and inserting into the vector db remains unchanged.

The rest of the architecture includes a frontend built using Angular to render the chatbot, a backend built using FastAPI to handle requests, and a PostgreSQL database that we use to cache some queries to conserve GPT api usage.
