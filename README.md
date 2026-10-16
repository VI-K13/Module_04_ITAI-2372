# Finance News AI Analyzer

A beginner-friendly financial news analysis prototype built in **Google Colab** using two pretrained language models: **FinBERT** for sentiment classification and **Qwen2.5-1.5B-Instruct** for article summaries, risk/opportunity analysis, and question answering. The interactive interface is built with **Gradio**.

This is an educational proof of concept, **not** an investment advisory or stock prediction tool.

## Features

- Select one of six fictional financial news examples or paste your own article.
- View positive, negative, or neutral sentiment and model confidence scores from FinBERT.
- Get a short, AI-generated article summary from Qwen.
- Ask Qwen to identify financial risks and opportunities discussed in the article.
- Ask your own questions about the article in natural language.

The program does **not** use manually written financial sentiment keyword rules or predefined answers. The pretrained models produce the predictions and responses. Basic input checks and text cleaning are performed in Python.

## Models and tools

| Component | Tool | Purpose |
| --- | --- | --- |
| Financial sentiment | `ProsusAI/finbert` | Pretrained positive/negative/neutral classifier |
| Text generation | `Qwen/Qwen2.5-1.5B-Instruct` | Pretrained small language model (SLM) |
| Interface | Gradio | Article input and AI output panels |
| Data processing | Pandas, Python regular expressions | Sample data, cleaning, basic tokenization |
| Visualization | Matplotlib | Sentiment distribution chart |
| Execution | Google Colab + PyTorch + Hugging Face Transformers | Run the notebook and models |

No paid API or API key is needed to run the pretrained models. A network connection is needed initially to install packages and download model files.

## Project structure

```text
Finance_News_AI_Analyzer_Project/
├── Finance_News_AI_Analyzer_Viktoriya_Kurmisheva.ipynb   # Complete Python notebook and Gradio app
├── README.md                                             # Project overview and instructions
├── requirements.txt                                      # Python dependencies
├── .gitignore                                            # Excludes temporary outputs/credentials
└── screenshots/
    ├── retail_sentiment.png
    ├── retail_ai_insights.png
    ├── tech_stocks_sentiment.png
    └── tech_stocks_ai_insights.png
```

**Why no `app.py` or HTML files?** The professor's Flask folder structure was an *example*. This implementation uses Gradio, so the interface, preprocessing, AI inference, and sample data are all in the `.ipynb` notebook. A separate Flask backend, `templates/`, and `static/` folders are not needed.

## How to run in Google Colab

1. Open [Google Colab](https://colab.research.google.com/) and upload `Finance_News_AI_Analyzer_Viktoriya_Kurmisheva.ipynb`.
2. If available, select **Runtime → Change runtime type → T4 GPU** for faster Qwen inference. CPU may be considerably slower, and memory limits can affect execution.
3. Select **Runtime → Run all**. Installation cells install the needed packages. The first run downloads FinBERT and Qwen from Hugging Face.
4. Wait for the final Gradio launch cell. Open the Gradio interface inside Colab or through its temporary share link.
5. Choose an article or paste financial text, click **Analyze Financial News**, and review the sentiment, summary, and risk/opportunity analysis.
6. Enter a question in the final text box and click **Ask Qwen**.

The temporary Gradio share link is public to anyone who knows it, so avoid pasting confidential financial information. Colab sessions and share links are temporary. Model downloads and inference can take time.

### Running outside Colab (optional)

Install packages using `pip install -r requirements.txt`. The supplied notebook uses Google Colab notebook commands and runs most easily there. Running locally requires a compatible Jupyter environment and enough memory for both models; the app is not packaged as an independent CLI or Flask server.

## Example tests and screenshots

The six built-in articles are *fictional examples*, not real or live financial news.

| Test | Input | What to verify | Screenshot |
| --- | --- | --- | --- |
| Negative sentiment | Article 5 (Retail) | FinBERT returned **Negative** with **97.30%** confidence | `screenshots/retail_sentiment.png` |
| Retail explanation & Q&A | Article 5; question: “What reduces customer's demand?” | Qwen linked reduced demand to higher product prices and identified falling sales as a risk | `screenshots/retail_ai_insights.png` |
| Positive sentiment | Article 1 (Tech Stocks) | FinBERT returned **Positive** with **95.53%** confidence | `screenshots/tech_stocks_sentiment.png` |
| Missing-information Q&A | Article 1; question: “Who is the CEO?” | Qwen replied that the article does not mention the CEO | `screenshots/tech_stocks_ai_insights.png` |

The screenshots document example outputs from the notebook. These tests do **not** establish model accuracy on a labeled benchmark. Qwen can still miss relevant implications or hallucinate unsupported facts. For example, it may overlook the positive business implications of strong earnings when identifying opportunities.

## Business use case

A financial news analyst or news aggregation team could use this prototype to skim short finance articles. FinBERT supplies an initial sentiment label, while Qwen helps summarize an article and answer focused questions. This could make early-stage review faster, but a human must check claims and assess the source before taking any financial action.

## Limitations

- No real-time financial news feed, verification, stock prediction, or trading recommendations.
- The sample dataset includes only six fictional articles, it is not a labeled evaluation dataset.
- Pretrained models may misclassify sentiment or generate inaccurate and unsupported explanations.
- The smaller Qwen model is less reliable than larger models on some nuanced questions.
- The application is a classroom prototype, not a secure production financial service.

**Disclaimer:** This application is for educational and informational use only and does not provide financial or investment advice.

## References

- [FinBERT model — Hugging Face](https://huggingface.co/ProsusAI/finbert)
- [Qwen2.5-1.5B-Instruct — Hugging Face](https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct)
- [Gradio documentation](https://www.gradio.app/docs)
- [Google Colab](https://colab.research.google.com/)
