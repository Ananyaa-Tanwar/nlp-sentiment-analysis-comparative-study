# Sentiment Analysis of IMDB Movie Reviews: A Comparison of TF-IDF and Word2Vec

This repository contains a comparative study evaluating two text representation approaches (TF-IDF and pretrained Word2Vec embeddings) for binary sentiment classification of movie reviews. The project was completed for IS 517: Methods of Data Science at the University of Illinois Urbana–Champaign.

---

## Project Overview

The goal of this project is to examine whether pretrained Word2Vec embeddings improve sentiment classification accuracy compared to TF-IDF features. Although distributed embeddings are widely used in modern NLP, classical feature engineering methods remain strong baselines. This project provides a controlled evaluation using identical classifiers across both representation methods.

**Research Question**

Do pretrained Word2Vec embeddings outperform TF-IDF features for sentiment classification on the IMDB movie reviews dataset?

---

## Dataset

- IMDB Movie Reviews dataset (TensorFlow Datasets)
- 50,000 reviews: 25,000 training and 25,000 testing
- Balanced classes: 12,500 positive and 12,500 negative in each split
- Raw text paired with binary sentiment labels:  
  - 0 = negative  
  - 1 = positive

---

## Methods

### Text Preprocessing
- Lowercasing, punctuation normalization, and tokenization
- Stopwords retained to preserve sentiment-bearing context

### Feature Representations

**TF-IDF**
- Sparse, high-dimensional vectors derived from the training corpus vocabulary (approximately 10,000 terms)

**Word2Vec**
- 300-dimensional pretrained embeddings (Google News)
- Review-level vectors created by averaging token embeddings

### Models
Both feature types were evaluated with:
- Logistic Regression
- Random Forest

All models were trained and tested on the same dataset to ensure a controlled comparison.

### Evaluation Metrics
- Accuracy, precision, recall, F1-score
- Confusion matrices
- Training time
- McNemar’s test to assess statistical significance between TF-IDF and Word2Vec prediction differences

---

## Results

### Performance Summary

**Best Model: TF-IDF + Logistic Regression**
- Accuracy: 89.70 percent
- F1-score: 0.8975
- Fastest training time among all models

Additional findings:
- Word2Vec models underperformed TF-IDF by approximately 4–9 percentage points
- Random Forest models performed worse than Logistic Regression for both representations and had significantly longer training times

### Statistical Significance (McNemar’s Test)
Comparing TF-IDF + Logistic Regression with Word2Vec + Logistic Regression:
- TF-IDF uniquely classified 2,128 reviews correctly
- Word2Vec uniquely classified 893 reviews correctly
- p-value < 0.0001

These results confirm that TF-IDF significantly outperformed Word2Vec.

### Error Analysis
- TF-IDF worked well when strong sentiment markers were present
- Word2Vec captured semantic similarity and paraphrased expressions
- Both struggled with sarcasm, mixed sentiment, and long narrative reviews lacking explicit sentiment cues

---

## Key Findings

- TF-IDF remains a strong and reliable baseline when domain-specific labeled data is available
- Pretrained Word2Vec embeddings did not improve performance for this task
- Averaging embeddings weakened the sentiment signal in Word2Vec representations
- Logistic Regression outperformed Random Forest on both feature types
- Random Forest models were slower and less accurate than Logistic Regression models

