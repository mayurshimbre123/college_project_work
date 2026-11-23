# Tweet sentiment analysis — explainable logistic regression

## Motivation

I wanted to understand classification without calling a pre-built ML model. I used 5,000 positive and 5,000 negative examples from NLTK's `twitter_samples`, split to 8,000 training and 2,000 test tweets.

## What happens to each tweet?

`tweet → remove links / mentions / ticker patterns → tokenize → remove stopwords → stem words → count positive-word frequency and negative-word frequency → sigmoid → prediction`.

I built a frequency dictionary keyed by `(word, sentiment_label)` from **training tweets** and implemented logistic regression and gradient descent. This is a classic small transparent feature-engineering pipeline; the trained representation is much simpler than a modern transformer.

## Result in original notebook

The saved output prints `Logistic regression model's accuracy = 0.9950`, i.e. **99.5% on the 2,000-example held-out split**. This is historical notebook output, not a new rerun or a guarantee on social media today.

The source notebook **does not implement Naive Bayes**. A resume mentioning both algorithms needs a separate artifact for the Naive Bayes claim.

## Caveats / next validation

Accuracy alone can conceal domain shift. Next I'd measure confusion matrix, precision/recall/F1, and test new unlabeled or independently labeled tweets from a different time period, documenting the split and data source. Dataset availability: NLTK's optional `twitter_samples` and `stopwords` corpora are downloaded separately if they are not cached.

## Source

See `original/Sentiment_Analysis.ipynb`. It contains the original implementation, historical outputs, and the original Colab link.

The logistic model uses a sigmoid of a weighted sum of the two frequency features plus a bias, then applies a 0.5 cutoff. The training loop updates the weights using the gradient of binary cross-entropy; accuracy counts correct predictions divided by the test set size.
