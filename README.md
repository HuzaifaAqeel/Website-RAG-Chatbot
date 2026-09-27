# Website-RAG-Chatbot 🌐🤖

Chat with any website. Paste a URL, and this Streamlit app scrapes the page's text,
splits it into chunks, embeds them with Google Gemini, stores them in a FAISS vector
index — then answers your questions using only the website's own content, with chat
history.

> **How it differs from a multi-PDF chatbot:** instead of uploading static files, you
> point it at a **live web page**. The app fetches the page at runtime, so it answers
> from whatever the site says *right now*.

## 🙏 Credits

This project is **extended from open source** — it was not built from scratch.

- Original project: [Kainatf043/chat_with_website](https://github.com/Kainatf043/chat_with_website) by **Kainatf043**
- Original license: **Apache License 2.0** (see [LICENSE](LICENSE))
- Extended & maintained by **Muhammad Huzaifa Aqeel** ([HuzaifaAqeel](https://github.com/HuzaifaAqeel))

## 🛠 Tech stack

| Layer | Technology |
|---|---|
| UI | Streamlit (chat UI + sidebar settings) |
| Web scraping | LangChain `WebBaseLoader` + BeautifulSoup |
| Chunking | `RecursiveCharacterTextSplitter` (1000 chars, 100 overlap) |
| Embeddings | Google Gemini `models/gemini-embedding-001` |
| Vector store | FAISS (in-memory similarity search) |
| LLM | Google Gemini `gemini-2.5-flash` |
| QA chain | LangChain "stuff" chain, answers strictly from retrieved context |

## 🚀 Run it

```bash
pip install -r requirements.txt

# set your Gemini API key (or paste it in the sidebar when the app opens)
export GOOGLE_API_KEY="your-key-here"

streamlit run app.py
```

1. Open the app in your browser.
2. In the sidebar, enter the website URL and click **🔍 Process Website**.
3. Ask anything about the page in the chat box — answers come only from the site's content.

## 🔧 What was changed from the original

- **Fixed dead model names**: `gemini-pro` → `gemini-2.5-flash`, `models/embedding-001` → `models/gemini-embedding-001`
- **Fixed removed LangChain import paths** for modern `langchain` 1.x (`langchain_community`, `langchain_text_splitters`, `langchain_core`, `langchain_classic`)
- **Fixed the broken API-key line** (it contained a literal `<redacted>` placeholder): now a proper masked sidebar text input with `GOOGLE_API_KEY` env-var fallback
- **Replaced the deprecated `google.generativeai` SDK call** with a plain environment variable the LangChain Gemini integration reads
- Cleaned up `requirements.txt` (removed unused packages, added the ones actually imported)
