# Finance News AI Analyzer

A finance-focused AI prototype developed in **Google Colab** with Python and **Gradio**. It combines traditional rule-based sentiment analysis (**VADER**), a pretrained financial sentiment model (**FinBERT**), and a small generative language model (**Qwen2.5-1.5B-Instruct**) for financial news summaries, risk and opportunity analysis, and question answering.

This project is for **educational purposes only**. It does not provide investment advice or predict stock prices.

## Features

- Select one of **six fictional example articles**, choose from **12 Kaggle financial statements**, or paste your own financial text.
- Analyze sentiment with **FinBERT**, including positive, negative, and neutral scores and a predicted label.
- Compare **VADER** (traditional rule-based NLP) with **FinBERT** using labeled financial data.
- Generate short article summaries and potential risks/opportunities with **Qwen**.
- Ask questions about an article and receive AI-generated answers grounded in its text.
- Evaluate sentiment predictions against reference labels using **accuracy, precision, recall, and F1-score**.

The project does **not** contain manually written keyword rules for sentiment or predefined financial answers. VADER uses its existing sentiment lexicon and rules; FinBERT and Qwen use pretrained models. Python handles basic input validation and preprocessing.

## Models and tools

| Component | Tool | Purpose |
| --- | --- | --- |
| Traditional sentiment analysis | `vaderSentiment` | Rule-based positive, negative, neutral, and compound sentiment scores |
| Financial sentiment model | `ProsusAI/finbert` | Predicts positive, negative, or neutral sentiment with confidence scores |
| Generative language model | `Qwen/Qwen2.5-1.5B-Instruct` | Generates summaries, financial insights, and answers |
| Interface | Gradio | Interactive article selection, text input, and output panels |
| Data handling and preprocessing | Pandas, regular expressions | Organizes text, removes unnecessary characters, tokenizes, and checks data quality |
| Evaluation | scikit-learn | Accuracy, precision, recall, F1-score, and classification reports |
| Visualization | Matplotlib | Sentiment charts and model comparison |
| Environment | Google Colab, PyTorch, Hugging Face Transformers | Runs pretrained models and the notebook |

No paid model API or API key is required. Internet access is needed for initial package installation and pretrained model downloads.

## Data

This project uses two sets of text:

1. **Six fictional finance examples**, created for testing longer summaries and natural-language Q&A. These are demonstrations, not genuine market news.
2. **FinancialPhraseBank**, distributed on Kaggle as `all-data.csv` in the *Sentiment Analysis for Financial News* dataset. The uploaded file contains **4,846 labeled financial statements**. After removing empty rows and exact duplicate texts, the notebook reports **4,838 usable statements**: **2,872 neutral**, **1,362 positive**, and **604 negative**.

The notebook selects a **stratified, reproducible sample of 300 statements** (`random_state=42`) to compare VADER and FinBERT against the reference labels. It also includes the first 12 Kaggle statements in the Gradio sample dropdown. The dropdown's `Positive`, `Negative`, or `Neutral` suffix is the **dataset reference label**, not FinBERT's prediction.

## Project structure

```text
Module_04_ITAI-2372/
├── Finance_News_AI_Analyzer_Viktoriya_Kurmisheva.ipynb
├── all-data.csv
├── README.md
├── requirements.txt
├── .gitignore
└── screenshots/
    ├── tech_stocks_sentiment.png
    ├── tech_stocks_ai_insights.png
    ├── kaggle_sentiment.png
    ├── kaggle_ai_insights.png
    ├── kaggle_dataset.png
    ├── vader_finbert_comparison.png
    └── model_evaluation.png
```

The example Flask project layout in the assignment is a suggested structure, not a requirement. Here, preprocessing, sentiment analysis, evaluation, generative AI, and the Gradio interface are organized into commented code and Markdown cells in one Colab notebook; separate `app.py`, HTML, and CSS files are unnecessary.

## How to run in Google Colab

1. Open [Google Colab](https://colab.research.google.com/) and upload `Finance_News_AI_Analyzer_Viktoriya_Kurmisheva.ipynb`.
2. If available, choose **Runtime → Change runtime type → T4 GPU**. CPU inference can be significantly slower.
3. Choose **Runtime → Run all**. The notebook installs required packages and downloads FinBERT and Qwen on its first run.
4. When prompted, upload **`all-data.csv`**. The Kaggle dataset is required for the evaluation and Kaggle dropdown examples.
5. Review the dataset cleaning outputs and VADER/FinBERT evaluation results.
6. Open the Gradio interface displayed near the end of the notebook (or use the temporary shared link).
7. Select a sample article or paste financial text, click **Analyze Financial News**, and review FinBERT's scores and Qwen's summary and risk analysis.
8. Enter a question under **Ask Questions About the Article** and click **Ask Qwen**.

Colab sessions and temporary Gradio links are not permanent. A shared Gradio link can be opened by others who have the URL, so do not enter sensitive or confidential text.

### Requirements

The notebook includes installation cells. For an alternate compatible Jupyter environment, the main dependencies are listed in `requirements.txt` and can be installed with:

```bash
pip install -r requirements.txt
```

The notebook is designed primarily for Google Colab; it is not a separately packaged Flask or command-line application.

## Evaluation results

Both sentiment methods were evaluated on the **same 300 labeled Kaggle financial statements**, using the dataset labels as the reference. The results obtained during the project test run were:

| Model | Accuracy | Macro F1 | Weighted F1 |
| --- | ---: | ---: | ---: |
| VADER (rule-based) | 0.513 | 0.470 | 0.519 |
| FinBERT (transformer) | 0.890 | 0.878 | 0.892 |

FinBERT performed better than VADER on this sample. The comparison illustrates a difference between general-purpose lexicon-based sentiment and a model adapted for financial language. These scores describe **this evaluation sample**, not guaranteed accuracy on all financial news, and the evaluation is not a training or fine-tuning experiment.

## Screenshots and functional tests

| Screenshot | What it demonstrates |
| --- | --- |
| `screenshots/tech_stocks_sentiment.png` | Fictional tech earnings example; FinBERT predicted positive sentiment (95.53% confidence) |
| `screenshots/tech_stocks_ai_insights.png` | Qwen article summary and answer about why investors reacted positively |
| `screenshots/kaggle_sentiment.png` | Real labeled Kaggle financial statement; FinBERT predicted positive sentiment (94.82% confidence) |
| `screenshots/kaggle_ai_insights.png` | Qwen summary, risk analysis, and Q&A for the Kaggle statement |
| `screenshots/kaggle_dataset.png` | CSV loading, cleaning, usable row count, and label distribution |
| `screenshots/vader_finbert_comparison.png` | Comparison chart for accuracy and macro F1 |
| `screenshots/model_evaluation.png` | Classification reports and evaluation metrics for VADER and FinBERT |

## Business use case

A financial news analyst or aggregation platform could use this prototype to review short financial updates more efficiently. FinBERT offers an initial sentiment assessment, VADER provides a traditional NLP baseline for comparison, and Qwen summarizes statements and answers questions about their contents. These outputs could support early-stage research, but a human should verify figures, interpretation, and source credibility before making financial decisions.

## Limitations and lessons learned

- The Qwen model can generate **unsupported claims or incorrect calculations**, even when its summaries sound convincing. In one Kaggle example, sales increased from **EUR 76 million to EUR 131 million**, but Qwen generated inconsistent percentage changes and suggested risks not established by the source. The calculated increase is approximately **72.4%**.
- Qwen can overlook implications, such as treating strong earnings as positive developments without identifying any opportunities.
- VADER is a general-purpose sentiment tool and can interpret financial language differently from FinBERT.
- The Kaggle data contains mainly short statements rather than complete articles, and the evaluation uses a sample of 300, not the full dataset.
- This prototype does not retrieve live news, verify financial claims, predict prices, or provide personalized financial recommendations.
- The application is not designed as a secure production financial service.

These findings show why model outputs, especially numerical claims and financial risk assessments, require human review.

**Disclaimer:** This application is for educational and informational use only and is not financial or investment advice.

## References

- [FinancialPhraseBank dataset on Kaggle](https://www.kaggle.com/datasets/ankurzing/sentiment-analysis-for-financial-news)
- [FinBERT — Hugging Face](https://huggingface.co/ProsusAI/finbert)
- [Qwen2.5-1.5B-Instruct — Hugging Face](https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct)
- [VADER Sentiment](https://github.com/cjhutto/vaderSentiment)
- [Gradio documentation](https://www.gradio.app/docs)
- [Google Colab](https://colab.research.google.com/)
