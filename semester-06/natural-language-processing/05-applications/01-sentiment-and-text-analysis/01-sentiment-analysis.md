# 5.1.1 Sentiment Analysis

## 1. Definition

**Sentiment Analysis** (also called **Opinion Mining**) is the computational study of people's opinions, sentiments, evaluations, attitudes, and emotions expressed in text, toward entities such as products, services, organizations, individuals, issues, events, or topics.

Formally, given a piece of text, the goal is to classify the **polarity** of the expressed opinion — typically as:
- **Positive**
- **Negative**
- **Neutral**

Some systems also detect finer-grained emotions (joy, anger, sadness, fear) or assign an **intensity/strength score** (e.g., a rating from −1 to +1, or 1 to 5 stars).

## 2. Why Sentiment Analysis Matters

- Enables businesses to automatically process large volumes of unstructured text (reviews, tweets, feedback) that would be impossible to read manually.
- Helps track public opinion in real time.
- Supports data-driven decision making in marketing, product design, and policy.

## 3. Levels of Sentiment Analysis

| Level | Description |
| --- | --- |
| **Document-level** | Classifies the sentiment of an entire document/review as a single polarity (assumes the document discusses one entity/opinion). |
| **Sentence-level** | Classifies sentiment for each individual sentence; first determines if a sentence is subjective (opinionated) or objective (factual), then classifies polarity. |
| **Aspect-based (ABSA)** | Identifies specific aspects/features of an entity (e.g., "battery," "camera" of a phone) and determines sentiment toward each aspect separately. Most fine-grained and informative level. |

*Example (Aspect-based):* "The camera is excellent, but the battery life is disappointing."
→ Aspect: *camera* → Positive; Aspect: *battery life* → Negative

## 4. Approaches to Sentiment Analysis

### A. Lexicon-Based Approach

- Relies on a predefined dictionary (lexicon) of words tagged with their sentiment orientation and strength.
- **Dictionary-based:** Uses existing sentiment lexicons such as **SentiWordNet**, **VADER**, or the **Bing Liu Opinion Lexicon**.
- **Corpus-based:** Builds a domain-specific lexicon by analyzing co-occurrence patterns of words in a large corpus, starting from a small seed list of sentiment words.
- *Advantage:* No labeled training data required.
- *Limitation:* Struggles with context-dependent, sarcastic, or domain-specific expressions.

### B. Machine Learning-Based Approach

- Treats sentiment analysis as a text classification problem.
- **Supervised learning:** Requires a labeled dataset. Common algorithms:
  - Naïve Bayes
  - Support Vector Machines (SVM)
  - Logistic Regression
  - Decision Trees / Random Forest
- **Unsupervised learning:** Used when labeled data is unavailable; relies on clustering or lexicon-assisted bootstrapping.
- *Advantage:* Can learn domain- and context-specific patterns.
- *Limitation:* Requires large amounts of labeled training data.

### C. Deep Learning-Based Approach

- Uses neural network architectures to automatically learn feature representations from text.
- Common models:
  - Recurrent Neural Networks (RNN), LSTM, GRU: capture sequential/contextual dependencies.
  - Convolutional Neural Networks (CNN): capture local n-gram-like features.
  - Transformer-based models (e.g., BERT): capture deep contextual meaning and currently achieve state-of-the-art results.
- *Advantage:* High accuracy, better handling of context and word order.
- *Limitation:* Computationally expensive; needs large datasets.

### D. Hybrid Approach

- Combines lexicon-based and machine learning methods to leverage the strengths of both (e.g., using lexicon scores as additional features for a classifier).

## 5. General Pipeline of Sentiment Analysis

1. **Data Collection:** gather text data (reviews, tweets, comments, survey responses).
2. **Text Preprocessing:** tokenization, stop-word removal, stemming/lemmatization, spelling correction, handling emojis/slang.
3. **Feature Extraction:** Bag-of-Words, TF-IDF, N-grams, POS tags, word embeddings (Word2Vec, GloVe, BERT embeddings).
4. **Sentiment Classification:** apply lexicon-based scoring or a trained ML/DL classifier.
5. **Evaluation:** assess performance using Accuracy, Precision, Recall, and F1-score against a labeled test set.

## 6. Key Challenges

- **Negation handling:** "not good" reverses polarity of "good."
- **Sarcasm and irony:** literal words may contradict the intended sentiment.
- **Context and domain dependence:** the same word can carry different sentiment in different domains (e.g., "unpredictable" is positive for a movie plot but negative for a car's steering).
- **Ambiguity of language:** comparative sentences, mixed opinions within one sentence.
- **Multilingual and code-mixed text:** informal, mixed-language social media text is hard to process.
- **Implicit sentiment:** opinions expressed without explicit sentiment words (e.g., "The phone died after two days").

## 7. Applications

- Product and service review analysis (e-commerce platforms)
- Social media monitoring and brand reputation management
- Customer feedback and support ticket prioritization
- Market research and competitor analysis
- Political opinion and election sentiment tracking
- Stock market prediction based on public sentiment
