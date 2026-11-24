# Amazon review sentiment

I compare two sentiment models on the Amazon Fine Food Reviews dataset. VADER is rule based and comes with NLTK. RoBERTa is a transformer model from Hugging Face, `cardiffnlp/twitter-roberta-base-sentiment`.

The star rating is the answer key. One or two stars counts as negative, three counts as neutral, and four or five counts as positive. The test set has 100 reviews per label. For each model I check accuracy, macro F1, and the average time per review.

## How it works

```mermaid
flowchart LR
    A["Reviews.csv<br/>568,454 reviews"] --> B["Drop duplicates and HTML<br/>393,579 left"]
    B --> C["Stars to labels<br/>1-2 negative, 3 neutral, 4-5 positive"]
    C --> D["Balanced sample<br/>100 per label, seed 42"]
    D --> E["VADER"]
    D --> F["RoBERTa"]
    E --> G["Compare with star labels<br/>accuracy, macro F1, time"]
    F --> G
```

## How each model decides

```mermaid
flowchart TB
    subgraph V["VADER"]
        V1["Review text"] --> V2["Look up each word in a list of scored words"]
        V2 --> V3["Adjust for words like not and very, caps, and !!!"]
        V3 --> V4["Add it all up into one compound score from -1 to 1"]
        V4 --> V5{"Compound score"}
        V5 -->|"0.05 or more"| V6["positive"]
        V5 -->|"in between"| V7["neutral"]
        V5 -->|"-0.05 or less"| V8["negative"]
    end
    subgraph R["RoBERTa"]
        R1["Review text"] --> R2["Split into tokens, at most 512"]
        R2 --> R3["Transformer reads all the tokens together"]
        R3 --> R4["Three chances that add up to 1<br/>negative, neutral, positive"]
        R4 --> R5["Pick the highest"]
    end
```

## Results

I ran both models on a Kaggle CPU on the same 300 reviews. Random guessing would get about 33%.

| Model | Accuracy | Macro F1 | Seconds per review |
|---|---|---|---|
| VADER | 44.7% | 0.37 | 0.001 |
| RoBERTa | 61.3% | 0.57 | 0.21 |

RoBERTa is more accurate. VADER is about 200 times faster.

### Most reviews are 5 stars

After removing duplicates, 393,579 reviews are left and about 78% of them are positive. That is why the test set takes the same number of reviews from each label.

![Reviews by star rating](results/figures/stars_count.png)

### Where each model gets confused

Rows are the real label from the stars and columns are what the model guessed. VADER calls most reviews positive, including 53 of the 100 negative ones. RoBERTa gets 69 of the negative ones right. Both models get neutral wrong most of the time.

![Confusion matrices for VADER and RoBERTa](results/figures/confusion_matrices.png)

### Scores by star rating

RoBERTa's positive score goes up steadily from 1 star to 5 stars. VADER gives 3 star and 4 star reviews almost the same score, so it can't tell neutral apart from positive.

![Scores by star rating for VADER and RoBERTa](results/figures/scores_by_stars.png)

### Sarcasm

Both models called "Oh great, another bag of stale chips. Just what I wanted." positive.

## Running it

The notebook is `notebooks/vader_vs_roberta.ipynb` and it runs online.

On Kaggle import the notebook, add the Amazon Fine Food Reviews dataset with Add Input, turn on Internet in the settings, and run all cells.

On Colab open the notebook from GitHub and run all cells. It downloads the dataset into the Colab session by itself.

[Open in Colab](https://colab.research.google.com/github/danish-puri/amazon-review-sentiment/blob/main/notebooks/vader_vs_roberta.ipynb).

add Claude, GPT, and Gemini API and compare all five models on accuracy, cost, and speed.

## Sources
- [Amazon Fine Food Reviews dataset](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews)
