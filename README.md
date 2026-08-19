# 🍽️ Restaurant Review Analysis using LLM & Prompt Engineering

An **LLM-based Restaurant Review Analysis system** that uses **Mistral-7B-Instruct** and carefully designed **prompt engineering** to analyze customer reviews and extract meaningful business insights.

The project focuses on understanding customer sentiment, analyzing different aspects of the dining experience, identifying liked/disliked features, and generating personalized responses.

> **Approach:** Prompt Engineering with an LLM
> **Model:** `mistralai/Mistral-7B-Instruct-v0.1`
> **RAG:** Not used

---

## 📌 Project Overview

Customer reviews contain valuable information about food quality, service, ambience, and overall customer satisfaction. Manually analyzing a large number of reviews can be time-consuming.

This project demonstrates how a Large Language Model can automatically analyze restaurant reviews and transform unstructured customer feedback into structured insights.

The system performs:

* Overall sentiment classification
* Aspect-level sentiment analysis
* Food quality analysis
* Service analysis
* Ambience analysis
* Liked/disliked feature extraction
* Review metadata extraction
* Personalized customer response generation
* Visualization of analysis results

The project is designed around **prompt engineering rather than Retrieval-Augmented Generation (RAG)**.

---

## 🎯 Objectives

The main objectives are:

1. Identify the overall sentiment of each restaurant review.
2. Classify reviews into:

   * Positive
   * Negative
   * Neutral
3. Analyze sentiment for important restaurant experience aspects:

   * Food Quality
   * Service
   * Ambience
4. Extract specific features customers liked or disliked.
5. Generate restaurant-specific insights.
6. Generate personalized responses based on customer feedback.
7. Visualize sentiment and aspect-level results.

---

## 🗂️ Dataset

The project uses `restaurant_reviews.csv`.

The dataset contains **20 restaurant reviews and 3 columns**.

### Dataset Columns

| Column          | Description                           |
| --------------- | ------------------------------------- |
| `restaurant_ID` | Unique identifier for each restaurant |
| `rating_review` | Customer rating                       |
| `review_full`   | Complete customer review              |

The ratings in the dataset range from **1 to 5**, with the provided dataset containing ratings of 1, 3, and 5.

### Dataset Quality

* Total records: **20**
* Total columns: **3**
* Missing values: **None**
* Unique restaurant IDs: **20**

## The notebook explicitly checks for missing values and reports zero missing values across all three columns.

## 🧠 Technology Stack

### Programming Language

* Python

### AI / Generative AI

* Large Language Models (LLM)
* Mistral-7B-Instruct
* Prompt Engineering
* Hugging Face Transformers

### Libraries

* Pandas
* JSON
* OS
* PyTorch
* Transformers
* Accelerate
* BitsAndBytes
* Matplotlib

The notebook installs specific versions of `transformers`, `accelerate`, and `bitsandbytes` for the model workflow.

---

## 🤖 LLM Model

The project uses:

```text
mistralai/Mistral-7B-Instruct-v0.1
```

The model is loaded using Hugging Face Transformers with **8-bit quantization** to reduce memory usage.

### Generation Parameters

The notebook uses parameters including:

```text
max_new_tokens = 300
temperature = 0.7
top_p = 0.9
do_sample = True
```

These parameters control the length and diversity of generated responses.

---

## 🔄 Project Workflow

```text
Restaurant Reviews CSV
        ↓
Load Dataset
        ↓
Data Inspection
        ↓
Missing Value Check
        ↓
Load Mistral LLM
        ↓
Prompt Engineering
        ↓
Overall Sentiment Analysis
        ↓
Aspect-Level Sentiment Analysis
        ↓
Liked / Disliked Feature Extraction
        ↓
Metadata Extraction
        ↓
Personalized Response Generation
        ↓
Visualization & Insights
```

---

# 1️⃣ Data Loading & Exploration

The CSV dataset is loaded using Pandas.

```python
data = pd.read_csv("restaurant_reviews.csv")
```

The notebook performs basic data exploration including:

* Viewing the first five records
* Checking dataset dimensions
* Checking missing values
* Creating a copy of the dataset for analysis

The dataset shape is:

```text
(20, 3)
```

## and no missing values were found.

# 2️⃣ Overall Sentiment Analysis

The first LLM task is to classify every review into one of three categories:

```text
Positive
Negative
Neutral
```

The model is instructed to return the result in JSON format.

Example expected format:

```json
{
  "Sentiment": "Positive"
}
```

The notebook then applies the classification function to every review and stores the result in a new `Sentiment` column.

### Sentiment Distribution

The analysis produced:

| Sentiment | Reviews |
| --------- | ------: |
| Positive  |       6 |
| Neutral   |       7 |
| Negative  |       7 |
| **Total** |  **20** |

---

# 3️⃣ Aspect-Level Sentiment Analysis

The project goes beyond overall sentiment by analyzing individual aspects of the restaurant experience.

The three major aspects are:

### 🍴 Food Quality

Analyzes opinions related to:

* Taste
* Food quality
* Presentation
* Temperature
* Preparation
* Overall food experience

### 👨‍🍳 Service

Analyzes:

* Staff behaviour
* Waiting time
* Responsiveness
* Customer service
* Ordering experience
* Service quality

### 🏠 Ambience

Analyzes:

* Interior
* Lighting
* Music
* Atmosphere
* Decor
* Overall environment

The resulting dataset contains separate sentiment fields for **Food Quality, Service, and Ambience**.

Possible aspect sentiment values include:

```text
Positive
Negative
Neutral
Not Applicable
```

---

# 4️⃣ Liked & Disliked Feature Extraction

The project also extracts **specific features** customers liked or disliked.

The model categorizes these features into:

```text
Food Quality Features
Service Features
Ambience Features
```

For example, features can include:

* Taste
* Temperature
* Presentation
* Waiting time
* Staff behaviour
* Lighting
* Music volume

The prompt specifically instructs the model to extract concrete features rather than generic phrases.

Example output structure:

```json
{
  "Food Quality Features": [],
  "Service Features": [],
  "Ambience Features": []
}
```

---

# 5️⃣ Restaurant Metadata & Insights

After sentiment and aspect analysis, the project extracts metadata associated with:

* Individual reviews
* Food quality features
* Service features
* Ambience features

This makes the results more useful for restaurant-specific analysis.

---

# 6️⃣ Personalized Customer Responses

The project also generates a personalized response for the customer based on:

* Review content
* Overall sentiment
* Aspect-level feedback
* Extracted customer experience

This allows the analysis system to move beyond classification and produce a more useful customer-facing response.

---

# 📊 Key Analysis Insights

The notebook reports the following aspect-level results:

| Aspect       | Positive | Negative | Neutral | Not Applicable |
| ------------ | -------: | -------: | ------: | -------------: |
| Food Quality |        6 |        8 |       5 |              1 |
| Service      |        8 |       10 |       2 |              0 |
| Ambience     |        8 |        1 |       6 |              5 |

### Key Findings

* **Service** is the most criticized aspect, with **10 negative reviews**.
* **Ambience** is the strongest positive driver, with **8 positive reviews**.
* **Food Quality** has a mixed distribution, with negative sentiment being the largest category.

---

# 📈 Visualization

The project creates visualizations to make the analysis easier to understand.

The notebook visualizes:

* Customer rating distribution
* Overall sentiment distribution
* Aspect-level sentiment
* Restaurant experience performance

## The aspect-level visualization compares Positive, Negative, and Neutral sentiment across Food Quality, Service, and Ambience.

# 🔐 Hugging Face Authentication

The notebook reads the Hugging Face token from a configuration file and stores it as an environment variable:

```python
os.environ["HF_TOKEN"] = HF_TOKEN
```

For your own implementation, **never commit your Hugging Face token or `config.json` containing secrets to GitHub**.

Recommended:

```text
config.json
.env
```

should be added to `.gitignore`.

Example:

```gitignore
config.json
.env
__pycache__/
*.pyc
```

---

# 🚀 Installation

Clone the repository:

```bash
git clone <your-repository-url>
cd restaurant-review-analysis
```

Install the required libraries:

```bash
pip install transformers==4.53.2
pip install accelerate==1.8.1
pip install bitsandbytes==0.46.1
pip install pandas
pip install torch
matplotlib
```

Or install everything using:

```bash
pip install -r requirements.txt
```

---

# ▶️ Running the Project

### Option 1 — Google Colab

1. Open the notebook in Google Colab.
2. Upload or connect the dataset.
3. Mount Google Drive if required.
4. Configure the Hugging Face token.
5. Run the cells sequentially.
6. Allow the Mistral model to download.
7. Execute the sentiment and aspect analysis sections.
8. Review the generated visualizations and insights.

The original notebook uses Google Drive to load `restaurant_reviews.csv`.

### Option 2 — Jupyter Notebook

Open:

```text
Restaurant_Review_Analysis_Notebook.ipynb
```

Then execute the cells sequentially.

---

# 📁 Project Structure

```text
restaurant-review-analysis/
│
├── Restaurant_Review_Analysis_Notebook.ipynb
├── restaurant_reviews.csv
├── README.md
├── requirements.txt
├── .gitignore
│
└── config.json              # Local only - DO NOT upload
```

---

# 🧩 Main Functions

### `query_mistral()`

Sends the prompt and review text to the Mistral model and returns the generated response.

### `classify_sentiment()`

Processes the model output and converts the JSON response into a sentiment classification.

```text
Positive
Negative
Neutral
```

### Aspect Classification

The project uses a separate prompt to classify sentiment for:

```text
Food Quality
Service
Ambience
```

### `classify_features()`

Extracts concrete liked/disliked features from the review and returns them as JSON.

---

# 🎯 Business Applications

This project can help restaurants and food platforms:

* Monitor customer satisfaction
* Identify service problems
* Understand food-related complaints
* Analyze ambience feedback
* Identify commonly liked features
* Identify recurring customer complaints
* Generate personalized responses
* Support restaurant improvement decisions

The overall goal is scalable automated review analysis for improving customer experience and service quality.

---

# ⚙️ Prompt Engineering Approach

The project relies heavily on structured prompts.

The prompts instruct the model to:

* Follow predefined sentiment categories
* Return structured JSON
* Analyze specific restaurant aspects
* Extract concrete features
* Avoid unnecessary explanations
* Produce machine-readable results

This makes the LLM output easier to process programmatically.

---

# 📏 Model Evaluation & Improvement

The notebook suggests manually labeling a subset of reviews and comparing those labels with the LLM's predictions to obtain a quantitative measure of accuracy and reliability.

Potential improvement strategies include:

* Refining prompts
* Adjusting `temperature`
* Adjusting `top_p`
* Improving output constraints
* Increasing the manually labeled evaluation set
* Testing different LLMs

---

# ⚠️ Limitations

The current project has a relatively small dataset of **20 reviews**, so the results should be treated as a demonstration rather than a production-level benchmark.

The notebook also proposes manual labeling of a subset of data for more quantitative evaluation; therefore, a formal accuracy score is not established in the current workflow.

Other practical considerations include:

* LLM inference requires significant computational resources.
* 8-bit quantization is used to reduce memory requirements.
* Prompt design can influence model output.
* JSON parsing can fail if the model produces invalid output.
* Larger and more diverse datasets would be needed for stronger evaluation.

---

# 🔮 Future Enhancements

Possible future improvements:

* Add a larger restaurant review dataset
* Build a Streamlit or Gradio interface
* Add restaurant-level dashboards
* Store analysis results in a database
* Add automated evaluation metrics
* Compare multiple LLMs
* Add multilingual review analysis
* Add trend analysis over time
* Add keyword and topic extraction
* Deploy the model as an API
* Add batch review processing

---

# 👨‍💻 Project Highlights

This project demonstrates practical experience with:

* Generative AI
* Large Language Models
* Prompt Engineering
* Hugging Face Transformers
* Mistral 7B
* LLM-based Sentiment Analysis
* Aspect-Based Sentiment Analysis
* Structured JSON Generation
* Natural Language Processing
* Python
* Pandas
* Data Visualization
* Business Intelligence

---

# 📜 Project Type

**Generative AI / NLP / LLM Project**

### Core Concept

```text
Customer Reviews
      ↓
Prompt Engineering
      ↓
Mistral 7B LLM
      ↓
Structured Analysis
      ↓
Sentiment + Aspects + Features
      ↓
Business Insights
```

---

## ⭐ Conclusion

The **Restaurant Review Analysis** project demonstrates how Generative AI can transform unstructured customer reviews into structured and actionable business insights.

By combining **Mistral-7B-Instruct**, **prompt engineering**, structured JSON outputs, aspect-level sentiment analysis, feature extraction, and visualization, the project provides a practical approach to understanding customer experiences across food quality, service, and ambience.

The project also demonstrates how LLMs can be used not only for classification, but also for extracting detailed customer feedback and generating personalized responses.
