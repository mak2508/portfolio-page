---
layout: page
title: ilm-ai
description: Agentic Course Studying Platform
# img: assets/img/3.jpg
importance: 1
category: work
---

Created an app for personalized exam prep using an agentic framework that lets you:
1. practise on questions similar to past exam/tutorials
2. get detailed feedback for each question with references to the lecture materials and topics to revise
3. generate personalized notes based on your performance on the practice quizzes
4. chat with an LLM about the course material

All the agents are built using small, locally deployable models as this was the theme of the hackathon. We use the Qwen3 4B model.

This is enabled by the following set of agents:
- **Course Generation Agent** \\
Makes use of web-scraper and PDF parser tools to collect data on a course given the course page link. All pdfs on the page are identified and parsed to get natural language text. Further, the html pages are also loaded. We then chunk and embed these documents and insert into a Vector DB.

- **Question Generation Agent** \\
Makes use of content mastery state (that is internally maintained and updated as the user practices questions), along with the Vector DB containing course content to generate questions for practice. To ensure question quality, we implement a **Verifier-Reviewer** pattern where the Verifier generates initial questions and the **Reviewer** critically evaluates them, providing feedback on clarity, answerability, and alignment with course material to iteratively improve question quality.

- **Answer Evaluation Agent** \\
The answer evaluation system implements an iterative Verifier-Reviewer architecture. When a student asks "Is my answer correct?", the **Verifier** retrieves relevant lecture content from the Vector DB and makes an initial assessment. The **Reviewer** then critically evaluates this assessment, providing feedback on reasoning quality, identifying potential errors, and suggesting improvements. This iterative process simulates higher-level chain of thought reasoning, ensuring students receive accurate, well-reasoned feedback with proper references to course materials.

- **Personalized Note Generation Agent** \\
When a student requests "Make personalized notes for me for topic X", we make use of another dual-model approach. The first **Qwen3 4B model** acts as the content generator, accessing both the Course Content Vector DB and the User Mastery/Past Question Answer Pairs database to create notes tailored to the student's current understanding level. The second **Qwen3 4B model** serves as the quality reviewer, ensuring the generated notes are grammatically and syntactically correct while verifying they contain only lecture content and does not include random hallucinations.. This two-stage process ensures personalized, accurate study materials that match the student's knowledge gaps and learning needs.

- **Chat QA Agent** \\
When a student has a question like "I don't get the Bayes theorem", the Chat QA Agent uses a single model with self-reflection capabilities. The agent retrieves relevant lecture content from the Vector DB and engages in self-reflection to ensure comprehensive and accurate explanations. Unlike the other agents, this uses a simpler single-model approach since conversational QA benefits from direct, contextual responses rather than iterative review cycles.


The choice of a dual-model approach for many of the agents is empirically motivated, where we initially struggled with getting high quality outouts but found that using a second model to review the work improved preformance significantly.

All the agents are built using [Pydantic AI](https://ai.pydantic.dev/). For our Vector DB we use [Milvus](https://milvus.io/) and for the DB we use [Supabase](https://supabase.com/).

This was created for the [ETH Entrepreneurship Club](https://www.entrepreneur-club.org/) Hackathon, where we got the runner-up spot. You can see our final pitch deck [here](assets/pdf/ilm-ai.pdf)
