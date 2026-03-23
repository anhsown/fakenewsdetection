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
