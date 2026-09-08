# Screenshots checklist

Add PNG/JPG screenshots of the notebook run here. Suggested filenames:

| # | Filename | Capture |
|---|---|---|
| 1 | `01_dataset_preview.png` | Dataset shapes + `products.head()` / `faqs.head()` / `reviews.head()` |
| 2 | `02_faq_embeddings.png` | FAQ embeddings shape (20 x 384) |
| 3 | `03_faq_search.png` | `search_faq_with_threshold(...)` + Ollama FAQ response |
| 4 | `04_tfidf_recommendation.png` | TF-IDF shape + top-3 retrieved products table |
| 5 | `05_ollama_recommendation.png` | Ollama recommendation + justification output |
| 6 | `06_product_qa.png` | `product_question_answer(...)` for the product + a follow-up question |
| 7 | `07_sentiment_analysis.png` | Sentiment pipeline load + per-review sentiment table |
| 8 | `08_review_summary.png` | Ollama-generated review summary output |
| 9 | `09_intent_detection.png` | Intent-detection test loop output |
| 10 | `10_chatbot_session.png` | Full interactive `ecommerce_chatbot()` session |

These correspond 1:1 to the cells in `gpt4_1.ipynb` — every cell already has saved output, so a screenshot of each cell (input + output) is all that's needed.
