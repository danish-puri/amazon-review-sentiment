# Amazon review sentiment

I compare two sentiment models on the Amazon Fine Food Reviews dataset. VADER is rule based and comes with NLTK. RoBERTa is a transformer model from Hugging Face, `cardiffnlp/twitter-roberta-base-sentiment`.

The star rating is the answer key. One or two stars counts as negative, three counts as neutral, and four or five counts as positive. The test set has 100 reviews per label. For each model I check accuracy, macro F1, and the average time per review.

## Running it

The notebook is `notebooks/vader_vs_roberta.ipynb` and it runs online, so nothing gets downloaded to my laptop.

On Kaggle I import the notebook, add the Amazon Fine Food Reviews dataset with Add Input, turn on Internet in the settings, and run all cells.

On Colab I open the notebook from GitHub and run all cells. It downloads the dataset into the Colab session by itself.

[Open in Colab](https://colab.research.google.com/github/danish-puri/amazon-review-sentiment/blob/main/notebooks/vader_vs_roberta.ipynb)

## Next

I plan to add Claude, GPT, and Gemini and compare all five models on accuracy, cost, and speed.

## Sources

- [Kaggle tutorial by Rob Mulla](https://www.kaggle.com/code/robikscube/sentiment-analysis-python-youtube-tutorial)
- [Amazon Fine Food Reviews dataset](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews)
