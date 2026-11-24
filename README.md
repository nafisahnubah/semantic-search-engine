# Semantic Search Engine

Two complementary explorations of embedding-based search, as an alternative to keyword
matching:

1. **Text-to-text semantic search**: documents are embedded with a pre-trained
   sentence-transformer model (`all-MiniLM-L6-v2`) and indexed with
   [Annoy](https://github.com/spotify/annoy) (Approximate Nearest Neighbors Oh Yeah) for
   fast similarity search.
2. **Text-to-image search**: a query like *"a dog running on the grass"* is used to
   search a database of photos directly, comparing [CLIP](https://openai.com/research/clip)
   and [BLIP](https://github.com/salesforce/BLIP) head-to-head on the same query.

## Why this over keyword search?

Keyword search only matches exact terms. Embedding models map text (and, in CLIP/BLIP's
case, images) into a shared vector space where *meaning* determines closeness, so a
query for "car repair" can retrieve a document about "automobile mechanic" with zero word
overlap. The notebook walks through generating those embeddings, indexing them for fast
approximate search, and querying across both a single modality (text→text) and across
modalities (text→image).

## Results

Top-4 cosine similarity scores for `"a dog running on the grass"` over the first 200
Flickr8k images, from the notebook's saved run:

| Model | Top-4 scores | Spread |
|---|---|---|
| CLIP (`openai/clip-vit-base-patch32`) | 0.305–0.321 | tightly clustered |
| BLIP (`Salesforce/blip-itm-base-coco`) | 0.468–0.545 | more spread out |

Both models return dog photos, and 2 of the 4 top images are shared between them. BLIP's
scores are higher and further apart. See the notebook for the side-by-side comparison
with rendered images.

## Requirements

- Python 3 with Jupyter (JupyterLab, Jupyter Notebook, or VS Code)
- A Linux/macOS-style shell for the setup cells (`mkdir -p`, `cp`, `chmod`, `unzip`),
  e.g. Linux, macOS, WSL, or Google Colab
- A [Kaggle](https://www.kaggle.com/) account and API token, to download Flickr8k
- A recipe CSV for the text-search half (not included)

See [`data/README.md`](data/README.md) for how to get both datasets.

## Getting started

```bash
pip install -r requirements.txt
```

1. Put a recipe dataset at `data/food_recipes.csv` (see [`data/README.md`](data/README.md)).
2. Set up your Kaggle API token (see [`data/README.md`](data/README.md)).
3. Start Jupyter from the `notebooks/` folder and run `semantic_search.ipynb` top to
   bottom. The notebook downloads Flickr8k into `data/flickr8k/` and writes its Annoy
   index to `notebooks/text.ann` (both git-ignored). The first run also downloads the
   three pre-trained models from Hugging Face.

## Project structure

```
semantic-search-engine/
├── notebooks/
│   └── semantic_search.ipynb   # all the code, results, and analysis
├── data/
│   └── README.md               # where to get the datasets
├── requirements.txt
├── LICENSE
└── README.md
```

## Tech stack

Python · Sentence-Transformers · Annoy · Hugging Face Transformers (CLIP, BLIP) · PyTorch

## License

[MIT](LICENSE)
