# Semantic Search Engine

Two complementary explorations of embedding-based search, as an alternative to keyword
matching:

1. **Text-to-text semantic search** — documents are embedded with a pre-trained
   sentence-transformer model and indexed with [Annoy](https://github.com/spotify/annoy)
   (Approximate Nearest Neighbors Oh Yeah) for fast similarity search.
2. **Text-to-image search** — a query like *"a dog running on the grass"* is used to
   search a database of photos directly, comparing [CLIP](https://openai.com/research/clip)
   and [BLIP](https://github.com/salesforce/BLIP) head-to-head on the same queries.

## Why this over keyword search?

Keyword search only matches exact terms. Embedding models map text (and, in CLIP/BLIP's
case, images) into a shared vector space where *meaning* determines closeness — so a
query for "car repair" can retrieve a document about "automobile mechanic" with zero word
overlap. The notebook walks through generating those embeddings, indexing them for fast
approximate search, and querying across both a single modality (text→text) and across
modalities (text→image).

## Results

Querying both models with `"a dog running on the grass"` over a Flickr8k subset:

| Model | Top score | Score spread |
|---|---|---|
| CLIP | ~0.30–0.32 | tightly clustered |
| BLIP | ~0.47–0.55 | well separated |

Both models surface relevant dog photos and their result sets overlap significantly, but
BLIP's scores are higher and more separated — it's more confident distinguishing its top
matches, at the cost of being heavier and slower than CLIP. See the notebook for the full
side-by-side comparison with rendered images.

## Getting started

```bash
pip install -r requirements.txt
```

See [`data/README.md`](data/README.md) for how to get the two datasets this project uses
(a text corpus for semantic search, Flickr8k for text-to-image search — the download
cells for both are already in the notebook).

Run `notebooks/semantic_search.ipynb` top to bottom.

## Project structure

```
semantic-search-engine/
├── notebooks/
│   └── semantic_search.ipynb   # all the code, results, and analysis
├── data/
│   └── README.md               # where to get the datasets
├── requirements.txt
└── README.md
```

## Tech stack

Python · Sentence-Transformers · Annoy · Hugging Face Transformers (CLIP, BLIP) · PyTorch
