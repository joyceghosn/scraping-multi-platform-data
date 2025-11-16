# Scraping Social Media for Mental Health Discourse  
**Multi-Platform Scraping • NLP Corpus Building • Sentiment & Context Analysis**

## Project Overview

This project builds a **multi-platform text dataset** about mental health by scraping posts from several social media platforms **without using official APIs**.  

The focus is not just to collect data, but to answer a central question:

> **How do different platforms talk about the *same* mental health keywords (e.g. “mental health”, “depression”, “burnout”, “therapy”)?**  
> Do they use them in the same way, or in completely different contexts?

To explore this, I:
- Scraped posts from multiple platforms (e.g. LinkedIn, Reddit, Nitter/Twitter, Threads)  
- Unified them into a single dataset  
- Performed **sentiment analysis** and basic **text analysis**  
- Compared **tone, context, and “style” of discourse** between platforms

The result is a **reusable NLP corpus** and an analysis showing that even when people use the same words, each platform has its own “personality”:
- **LinkedIn** → more professional, career-oriented framing  
- **Reddit** → more natural, long, raw, and vulnerable  
- **Twitter/Nitter** → short, familiar, reactive, and conversational  

---

## Goals & Research Questions

### Main Goal  
Build a **scraped, multi-platform dataset** about mental health topics and analyze how **the same keywords** are used in different contexts across social media.

### Key Questions
1. **Collection / Technical**
   - Can we collect a meaningful amount of data on mental health topics **without using official APIs**, despite rate limits and blocking?
   - What are the practical challenges of scraping modern, dynamic platforms?

2. **Content / NLP**
   - When users mention “mental health”, “depression”, “burnout”, “therapy”, etc.,  
     do they express **similar themes** across platforms?
   - How do **tone, sentiment, and context** differ between LinkedIn, Reddit, Twitter/Nitter, and others?

3. **Platform Differences**
   - Is LinkedIn really more **professional** and career-framed?
   - Is Reddit more **personal and deep**?
   - Is Twitter/Nitter more **familiar, reactive, and casual**?
   - Do platforms reuse the *same keywords* but give them **different meanings** through context?

---

## Repository Structure

*(Adjust file names if yours differ slightly.)*

- `01-All platforms combined.csv`  
  Unified dataset of all scraped posts with columns like:
  - `platform`
  - `username`
  - `post_text`
  - `date`
  - `likes`, `comments`, etc. (when available)
  - `keyword` (e.g. "mental health", "burnout", "depression")

- `02-Sentiment_analysis project.ipynb`  
  Notebook performing:
  - Basic preprocessing
  - Lexicon-based or model-based **sentiment analysis**
  - Sentiment distribution by platform and keyword
  - Comparative visualizations

- `03-data analysis scraping project.ipynb`  
  Notebook focusing on:
  - Exploratory data analysis (EDA)
  - Keyword usage by platform
  - Length, style, and context differences
  - Example posts per platform
  - Interpretation of results

- `scraping_*.py` or `scraping_*.ipynb` (optional, if added)  
  Platform-specific scraping scripts using **Selenium / requests** and HTML parsing.

- `README.md`  
  This documentation file.

---

## Data Collection & Scraping Approach

Because access to official APIs (especially Twitter/X) has become **restricted, paid, or unstable**, the project uses **HTML scraping** strategies instead of APIs.

### Platforms & Tools
- **Tools**: Python, Selenium (for dynamic content), requests, BeautifulSoup or similar HTML parsers.
- **Targets** (examples):
  - **Nitter/Twitter:** public instances as a “mirror” of Twitter timelines or search results
  - **Reddit:** public threads and comments pages
  - **LinkedIn:** public posts (limited, due to stricter protection)
  - **Threads (Instagram):** post feeds filtered by keywords (where structurally possible)

### Scraping Strategy
- Keyword-based search (e.g. `"mental health"`, `"depression"`, `"burnout"`, `"therapy"`, `"anxiety"`)
- Extract:
  - Username or handle (when visible)
  - Post text
  - Engagement metrics (likes, comments, reposts, etc., when possible)
  - Date and possibly language or location (if available)
- Save results in platform-specific dataframes, then **combine** into `01-All platforms combined.csv`.

### Challenges (Real-World)
- **API Restrictions & Costs**
  - Twitter/X API is now limited or paid, so a standard academic/API approach was not feasible.
- **Rate Limiting & Blocking**
  - Too many requests in a short period can:
    - Trigger CAPTCHA pages
    - Get the IP temporarily blocked
    - Break the HTML structure mid-scrape
- **Dynamic HTML & CSS**
  - Class names and DOM structure (e.g. `div` with weird dynamic classes) change over time.
  - Requires **manual inspection of HTML** and frequent updates to selectors.
- **Ethical & Legal Considerations**
  - Only scraping **public** content.
  - Avoiding authentication where possible.
  - No attempt to deanonymize users.
  - Data used only for **research/educational purposes** with caution about privacy and platform TOS.

---

## Text & Sentiment Analysis

Once the combined dataset is built, the analysis focuses on **how keywords are used** across platforms.

### Preprocessing
- Lowercasing text
- Removing URLs, usernames, emojis, punctuation
- Optional:
  - Stopword removal
  - Lemmatization / stemming
  - Tokenization for later NLP tasks

### Sentiment Analysis
Implemented in `02-Sentiment_analysis project.ipynb`:
- Lexicon-based tools (e.g. VADER/TextBlob) *or* model-based sentiment
- Sentiment categories:
  - **Positive**
  - **Negative**
  - **Neutral**
- Aggregated by:
  - Platform
  - Keyword
  - Possibly time (if enough data)

### Context / Style Analysis
In `03-data analysis scraping project.ipynb`:
- Average length of posts by platform
- Most frequent **co-occurring words** for each keyword, per platform
- Example posts illustrating typical tone/context on each site
- Basic comparisons like:
  - Use of hashtags vs long paragraphs  
  - Presence of personal pronouns (“I”, “me”) vs generic statements  
  - Frequency of terms like “job”, “manager”, “burnout”, “therapy”, etc.

---

## Key Observations & Insights

> These are high-level conclusions based on comparing posts about the **same mental health keywords** across different platforms.

### 1-Same words, different worlds

Even when people use identical keywords (e.g. *“burnout”*, *“mental health”*, *“depression”*), the **platform changes the meaning and context**:

- On **LinkedIn**, “burnout” often appears in:
  - Posts about **workload**, productivity, HR policies
  - Discussions on professional development, leadership, and corporate culture  
  ⇒ The tone is more **professional, advice-driven, and polished**.

- On **Reddit**, the same words appear in:
  - Long, detailed personal stories
  - Anonymous confessions
  - Deep emotional reflections  
  ⇒ The tone is more **raw, vulnerable, and natural**, often longer and more detailed.

- On **Twitter/Nitter**, mentions of mental health are:
  - Short, reactive, conversational
  - Mixed with humor, memes, political reaction, or quick personal updates  
  ⇒ The tone is more **familiar, real, and immediate**, but sometimes less detailed.

### 2️-Sentiment Differences

- **Reddit** posts:
  - Contain many **negative and deeply emotional** narratives, but also supportive comments.
- **LinkedIn** posts:
  - Tend to be slightly more **neutral or positive**, focused on solutions, awareness, and “lessons learned”.
- **Twitter/Nitter**:
  - Shows a **mixed sentiment** — frustration, humor, and activism can appear side by side within the same keyword.

### 3️-Platform “Personality”

The project confirms that:
- **LinkedIn** talks about mental health with a **professional filter**:
  - “Mental health at work”
  - “Preventing burnout in teams”
  - “HR initiatives”  

- **Reddit** treats mental health as a **safe space for sharing**:
  - “I’m struggling with…”
  - “How do I cope with…?”
  - “Has anyone else experienced…?”  

- **Twitter/Nitter** makes mental health:
  - Part of everyday public conversation
  - Often blended with jokes, sarcasm, or short bursts of honesty.

Even with the **same keywords**, each platform tells a **different story**.

---

## Limitations

- **Sampling Bias**
  - Data is restricted by what can be scraped without APIs and without getting blocked.
  - Some platforms (especially LinkedIn) are under-represented compared to Reddit/Twitter.

- **Rate Limits & Blocks**
  - Scraping had to be throttled and sometimes interrupted to avoid IP bans.
  - This means the dataset is *illustrative*, not “complete”.

- **No Official API**
  - Lack of API means:
    - Less control over search precision
    - More noise in results
    - Limited metadata compared to what APIs could offer

- **Language & Region**
  - Analysis mainly focuses on posts in a primary language (e.g. English); other languages may appear but are not separately analyzed.

Despite these limitations, the dataset is **rich enough** to clearly show **qualitative differences** between platforms.

---

## Skills Demonstrated

This project showcases skills highly relevant for **Data Science / NLP / Analytics internships**:

- **Web Scraping (without API)**
  - Selenium / dynamic content handling
  - Working around CSS classes, infinite scroll, and rate limits

- **Data Engineering**
  - Combining multiple raw sources into a unified dataset
  - Designing a schema suitable for NLP and sentiment analysis

- **NLP & Text Analysis**
  - Text preprocessing
  - Sentiment analysis
  - Comparative analysis of language use across platforms

- **Exploratory Data Analysis**
  - Visualizing distributions and patterns
  - Comparing behavior across groups (platforms, keywords)

- **Critical Thinking & Interpretation**
  - Turning raw metrics into **meaningful insights**
  - Understanding **how platform design shapes discourse**

- **Ethics & Practical Constraints**
  - Handling scraping responsibly
  - Recognizing limitations imposed by platform policies and infrastructure

---

## About the Author

I’m a Master’s student in Data Science, interested in **NLP, social media analysis, and mental health discourse online**.  

This project is part of a broader exploration of how **the same words** can mean very different things depending on **who says them, where, and how** — and what this implies for researchers and practitioners working with social media data.

