# Datasets

This project uses two datasets:

## 1. Text corpus (for text-to-text semantic search)

Place a `food_recipes.csv` file here with at least `title` and `directions` text columns.
Any recipe dataset from [Kaggle](https://www.kaggle.com/datasets) with those fields (or
similarly named ones you rename to match) will work — the notebook only needs a decent
amount of free-text documents to embed and search over.

Expected path: `data/food_recipes.csv`

## 2. Flickr8k (for text-to-image search)

The notebook downloads this automatically via the Kaggle API:

```bash
pip install kaggle
# place your kaggle.json API token at ~/.kaggle/kaggle.json
# (generate one from https://www.kaggle.com/settings -> API -> Create New Token)
```

The relevant setup/download cells are already in `notebooks/semantic_search.ipynb` — just
make sure your Kaggle credentials are in place before running them. This will populate
`data/flickr8k/`.
