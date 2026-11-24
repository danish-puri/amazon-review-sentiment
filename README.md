# Amazon review sentiment

I compare two sentiment models on the Amazon Fine Food Reviews dataset. VADER is rule based and comes with NLTK. RoBERTa is a transformer model from Hugging Face, `cardiffnlp/twitter-roberta-base-sentiment`.

The star rating is the answer key. One or two stars counts as negative, three counts as neutral, and four or five counts as positive. The test set has 100 reviews per label. For each model I check accuracy, macro F1, and the average time per review.

## Running it

The notebook is `notebooks/vader_vs_roberta.ipynb` and it runs online.

On Kaggle import the notebook, add the Amazon Fine Food Reviews dataset with Add Input, turn on Internet in the settings, and run all cells.

On Colab open the notebook from GitHub and run all cells. It downloads the dataset into the Colab session by itself.

[Open in Colab](https://colab.research.google.com/github/danish-puri/amazon-review-sentiment/blob/main/notebooks/vader_vs_roberta.ipynb).

add Claude, GPT, and Gemini API and compare all five models on accuracy, cost, and speed.

## Sources
- [Amazon Fine Food Reviews dataset](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews)
