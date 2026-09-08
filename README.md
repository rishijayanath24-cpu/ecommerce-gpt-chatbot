# AI-Powered E-Commerce Chatbot (RAG + Ollama)

**24CS2506 – Building Applications using GPT-4 · Experiment 1**

A modular Retrieval-Augmented Generation (RAG) e-commerce chatbot built with [Ollama](https://ollama.com) (local LLM), Sentence-Transformer embeddings, TF-IDF retrieval, and a HuggingFace sentiment-analysis pipeline. It answers FAQs, recommends products, answers product-specific questions, summarizes customer reviews, and routes each query to the right module using an LLM-based intent detector.

```
User Query
   -> Intent Detection (Ollama)
   -> FAQ | Recommendation | Product QA | Review
   -> Retrieval (Sentence-Transformer embeddings / TF-IDF / Reviews)
   -> Ollama
   -> Natural Language Response
```

## Project Structure

```
ECommerceGPT/
├── gpt4_1.ipynb        # Full implementation (all modules, run end-to-end with saved outputs)
├── requirements.txt     # Python dependencies
├── data/
│   ├── products.csv     # 100 products: ProductID, ProductName, Category, Brand, Price, Description, Rating
│   ├── faqs.csv          # 20 FAQ question/answer pairs
│   └── reviews.csv       # 1000 customer reviews across products
├── screenshots/          # Notebook run screenshots (see below)
└── README.md
```

## Modules Implemented

| Module | Technique |
|---|---|
| FAQ Semantic Search | `sentence-transformers/all-MiniLM-L6-v2` embeddings + cosine similarity, with a similarity threshold gate |
| Product Recommendation | TF-IDF over product descriptions, top-3 retrieval, Ollama picks the best match with justification |
| Product Q&A (RAG) | TF-IDF single best-match retrieval, Ollama answers constrained to the retrieved product context only |
| Review Intelligence | `distilbert-base-uncased-finetuned-sst-2-english` sentiment pipeline + Ollama-generated summary and buying suggestion |
| Intent Routing | Ollama zero-shot classifies each query into `FAQ` / `RECOMMENDATION` / `PRODUCT` / `REVIEW` |
| Integrated Chatbot | Continuous `input()` loop that routes every query through the module above, until `exit` |

All Ollama calls use the local model **`qwen2.5:0.5b`**.

## Setup

**1. Install Ollama and pull the model**

```bash
# https://ollama.com/download
ollama pull qwen2.5:0.5b
```

**2. Create a virtual environment and install dependencies**

```bash
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # macOS/Linux

pip install -r requirements.txt
```

**3. Run the notebook**

```bash
jupyter notebook gpt4_1.ipynb
```

Run all cells top to bottom. The last cell launches `ecommerce_chatbot()`, an interactive loop — type your question at the `You:` prompt, or `exit` to stop.

## Sample Interaction

```
You: Where is my parcel?
Detected Intent: FAQ
Assistant: Click on the 'Track Order' section on our platform...

You: Recommend a gaming laptop
Detected Intent: PRODUCT
Assistant: ...Price: ₹30,316 | Category: Laptop | Rating: 5/5

You: exit
Chatbot: Goodbye!
```

## Known Limitations

- TF-IDF is fit only on the `Description` column, and product descriptions are templated per brand — so retrieval can't always distinguish e.g. "Lenovo Laptop 1" from "Lenovo Laptop 3" by text alone.
- `qwen2.5:0.5b` is a very small (0.5B parameter) model; intent classification and product Q&A occasionally misroute or generalize rather than staying strictly grounded in the retrieved row. A larger Ollama model (`qwen2.5:7b`, `llama3.1:8b`, etc.) improves accuracy.
- The product Q&A loop has no conversational memory — each question re-runs retrieval independently.

## Screenshots

See [`screenshots/`](screenshots/) for notebook run captures of each module (dataset preview, FAQ search, recommendation, product Q&A, sentiment analysis, intent detection, and the full chatbot session).
