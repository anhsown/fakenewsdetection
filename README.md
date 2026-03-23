# fakenewsdetection

## A. Problem Statement
The widespread dissemination of fake news and propaganda presents serious societal
risks, including the erosion of public trust, political polarization, manipulation of
elections, and the spread of harmful misinformation during crises such as pandemics
or conflicts. From an NLP perspective, detecting fake news is challenging.
Linguistically, fake news often mimics the tone and structure of legitimate journalism,
making it difficult to distinguish using surface-level features. The absence of reliable
and up-to-date labeled datasets, especially across multiple languages and regions,
hampers the effectiveness of supervised learning models. Additionally, the dynamic
and adversarial nature of misinformation means that malicious actors constantly
evolve their language and strategies to bypass detection systems. This project
addresses these challenges using a transformer-based language model.
## B. Dataset Overview
- Source: Public dataset from Ahmed, H., Traore, I., & Saad, S. (2017)
- Files:
  - MisinfoSuperset_TRUE.csv (True articles from reputable sources such as Reuters, The New York Times)
  - MisinfoSuperset_FAKE.csv (Fake/misinformation articles from unreliable sources)
- Total Data: ~13,721 samples (after cleaning and deduplication)
## C. Data Preprocessing
- Steps performed:
  - 1. Load and merge datasets:
    - Assigned labels: 1 for TRUE, 0 for FAKE
  - 2. Drop null and duplicate entries:
    - Removed all rows with missing values and duplicate content
  - 3. Text cleaning:
    - Lowercased text, removed special characters and excessive whitespace
        (though BERT tokenizer handles most of it internally)
  - 4. Train-test split:
     Stratified 80/20 split
  - 5. Tokenization:
    - Used bert-base-uncased tokenizer
    - Padded/truncated to a max_length=256
## D. Exploratory Data Analysis (EDA)
- Label distribution: Balanced (approx. 50/50 FAKE vs. TRUE)
- Text length: Most articles < 300 tokens, justifying max_length=256
- Word cloud and N-gram analysis:
  - Fake news tends to use emotionally charged language
  - True news uses a more factual, neutral tone
- Visualization added:
  - WordCloud of fake and real articles
  - ROC Curve plotted for binary classification
## E. Model Building: BERT for Sequence Classification
- Model used: BertForSequenceClassification from HuggingFace Transformers
- Base model: bert-base-uncased• Classifier head: Linear layer with dropout
## F. Hyperparameter Tuning
- Batch size: 8 (to accommodate GPU memory)
- Learning rate: 2e-5 (AdamW optimizer)
- Epochs: 3
- Max sequence length: 256
## G. Model Training
- Trained on NVIDIA Tesla T4 (15GB VRAM, 16GB RAM)
- Training time per epoch: ~41 minutes
- Total training time: ~2.05 hours
- Training Loss per Epoch:
    - Epoch 1: 0.0665
    - Epoch 2: 0.0249
    - Epoch 3: 0.0148
## H. Performance Evaluation
- Test set performance (13,721 samples):
           precision recall f1-score support
Fake       1.00      0.98   0.99     6816
True       0.98      1.00   0.99     6905
accuracy                    0.99     13721
macro avg  0.99      0.99   0.99     13721
weighted avg 0.99    0.99   0.99     13721
- Confusion matrix: Near-perfect classification with minimal false
positives/negatives
- F1-score of 0.99 shows excellent balance between precision and recall
- ROC Curve: AUC near 1.0, confirming excellent discrimination capability
between classes
