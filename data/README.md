# Datasets

This project uses two datasets:

## 1. Text corpus (for text-to-text semantic search)

Place a `food_recipes.csv` file here with at least `title` and `directions` text columns.
Any recipe dataset from [Kaggle](https://www.kaggle.com/datasets) with those fields (or
similarly named ones you rename to match) will work — the notebook only needs a decent
amount of free-text documents to embed and search over.

Expected path: `data/food_recipes.csv`

## 2. Flickr8k (for text-to-image search)

The notebook downloads this automatically via the Kaggle API
([adityajn105/flickr8k](https://www.kaggle.com/datasets/adityajn105/flickr8k)). You need
a Kaggle API token, `kaggle.json`, generated from
<https://www.kaggle.com/settings> → API → Create New Token.

The notebook's setup cell copies `kaggle.json` from the `notebooks/` folder into
`~/.kaggle/`, so either:

- put `kaggle.json` in `notebooks/` before running (it is git-ignored), or
- put it at `~/.kaggle/kaggle.json` yourself and skip that cell.

The download cell then saves `flickr8k.zip` here and extracts it to `data/flickr8k/`.
The text-to-image section uses the first 200 images (sorted by filename) from
`data/flickr8k/Images/`.
