# LLM-Recommender-System
This project builds a smart LLM recommender from 2,440 Reddit posts. It uses BERTopic for topic modeling, RoBERTa for sentiment, and NER to find LLMs. A knowledge base aggregates sentiment by topic/LLM, so the final app can semantically match a user query and recommend the best LLM for that task.

This project builds an LLM recommender system from scratch using Reddit data. The goal is to advise a user on the best LLM (like ChatGPT, Claude, or Gemini) for a specific task by analyzing real user sentiment for that exact use case.

The pipeline begins with Topic Modeling.ipynb, which ingests 2,440 Reddit posts and uses BERTopic to cluster them into 10 distinct topics, such as "Use Case: Coding & Development" and "Pain Point: Content Filters."

Next, the Sentiment Analysis.ipynb notebook uses a RoBERTa transformer, a model well-suited for social media, to assign a positive, negative, or neutral sentiment score to each post. The NER.ipynb (Named Entity Recognition) notebook then identifies which LLM is being discussed, cleverly using regex for explicit mentions and falling back to the post's subreddit (e.g., a post in r/ClaudeAI) for implicit ones.

The Knowledge Base.ipynb notebook is the core of the project. It merges all this data, aggregating sentiment by both topic and LLM. It calculates a "positive experience score" (positive / (positive + negative)) for every LLM-topic pair (e.g., "Claude" + "Coding").

Finally, the LLM Recommender.ipynb notebook provides an interactive application. A user can type a query ("I need help with debugging"), which is semantically matched to the most relevant topic ("Use Case: Coding & Development"). The system then retrieves and ranks the best-performing LLMs for that specific task, all based on aggregated user sentiment.
