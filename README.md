# LLM-Recommender-System

This project builds an LLM recommender system from scratch using Reddit data. The goal is to advise a user on the best LLM (like ChatGPT, Claude, or Gemini) for a specific task by analyzing real user sentiment for that exact use case.

The system ingests 2,440 raw Reddit posts and processes them through a multi-stage data pipeline to create a smart, semantic search application.

## Pipeline & Methodology

The project is broken down into five distinct stages, each represented by a Jupyter Notebook:

1.  **`Topic Modeling.ipynb`**:
    * Ingests all 2,440 Reddit posts.
    * Uses **BERTopic** to cluster the documents into 10 distinct topics, such as "Use Case: Coding & Development" and "Pain Point: Content Filters."

2.  **`Sentiment Analysis.ipynb`**:
    * Employs a **RoBERTa transformer model**, which is highly effective for social media text.
    * Assigns a `positive`, `negative`, or `neutral` sentiment score to each post.

3.  **`NER.ipynb` (Named Entity Recognition)**:
    * Identifies which LLM is being discussed in each post.
    * Cleverly uses regex patterns to find explicit mentions (e.g., "Grok", "GPT-4o").
    * For posts without explicit mentions, it falls back to the post's subreddit (e.g., a post in `r/ClaudeAI` is tagged as "Claude").

4.  **`Knowledge Base.ipynb`**:
    * This is the core of the project. It merges the data from the previous steps (topics, sentiment, and NER).
    * It aggregates sentiment by both topic and LLM to find the performance of each model for each specific task.
    * It calculates a "positive experience score" (`positive / (positive + negative)`) for every LLM-topic pair (e.g., "Claude" + "Coding").

5.  **`LLM Recommender.ipynb`**:
    * Provides the final, interactive application.
    * A user can type a natural language query (e.g., "I need help with debugging").
    * The query is **semantically matched** to the most relevant topic ("Use Case: Coding & Development").
    * The system then retrieves and ranks the best-performing LLMs for that specific task, based on the aggregated user sentiment from the knowledge base.
