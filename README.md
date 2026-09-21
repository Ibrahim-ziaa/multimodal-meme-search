# Meme search: finding images by describing them

Type a description ("person in a Spider Man outfit") and get back the matching memes. The search runs over the caption text attached to each image, and compares two classic ways of turning text into vectors.

```
query text --> clean and lemmatise --> vector --> cosine similarity against every caption vector --> top matches shown as images
```

## Methods compared

- **TF-IDF:** sparse word weighting with scikit-learn. No training, matches exact words well.
- **Word2Vec:** 512 dimensional word vectors trained on the captions with Gensim (window 4, 100 epochs). A caption or a query is the average of its word vectors, so related words can match even when the exact word differs.

Text is cleaned first: lower casing, punctuation and stop word removal, and lemmatisation with NLTK.

## What the notebook shows

`notebooks/processor.ipynb` runs the same query through each method and displays the retrieved images side by side. Observations recorded in the notebook, from that run on Kaggle:

| | TF-IDF | Word2Vec |
|---|---|---|
| Time per query | about 16 seconds | about 3 seconds |
| Training time | none | about 90 seconds |
| Behaviour | strongest on exact wording | better on related wording |

This is a qualitative comparison. The notebook does not contain a labelled evaluation set, so no accuracy figures are claimed.

## Known issue

The model labelled CBOW is currently trained with the same skip gram setting as the Skip-Gram model (`sg=1` in both calls), so the two Word2Vec result sets come from the same algorithm. The fix is a one character change (`sg=0`) followed by a rerun.

## Data

[MemeConvX](https://www.kaggle.com/datasets/harshittiwari007/meme-convx) on Kaggle. The images are not included in this repository.

## Why it is relevant

This is the same retrieval idea that sits under modern semantic search and retrieval augmented generation: put queries and documents in one vector space, then rank by similarity. Here it is built from first principles, without a vector database.

## Stack

Python, scikit-learn, Gensim, NLTK, pandas, matplotlib.

## License

GPL-3.0
