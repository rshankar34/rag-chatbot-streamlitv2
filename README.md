```markdown
# ☁️ RAG PDF Chatbot

A Retrieval-Augmented Generation (RAG) chatbot to upload PDF documents, ask questions about their contents, and receive AI-powered answers with cited sources—built with Streamlit, LangChain, OpenAI GPT-4o-mini, FAISS, and AWS.

---

## 🚀 Features

- **Multi-PDF Upload**: Upload and process multiple PDFs.
- **Semantic Search**: Contextual lookup using FAISS vector DB.
- **AI Q&A**: Leverages GPT-4o-mini for contextual question answering.
- **Persistent Chat History**: Session chat is stored in DynamoDB.
- **Cloud Native**: AWS S3 for storage, Streamlit UI.

---

## 🛠️ Tech Stack

| Component      | Technology           |
| -------------- | ------------------- |
| Frontend       | Streamlit           |
| LLM            | OpenAI GPT-4o-mini  |
| Vector DB      | FAISS + SentenceTransformers |
| Storage        | AWS S3              |
| Database       | AWS DynamoDB        |
| Framework      | LangChain           |
| Language       | Python 3.11+        |

---

## 📦 Quickstart

### Prerequisites

- Python 3.11+
- AWS account with S3 & DynamoDB (free tier is sufficient)
- OpenAI API key

### 1. Clone and Install

```
git clone <your-repo-url>
cd rag-chatbot-streamlit
pip install -r requirements.txt
```

---

### 2. AWS Setup

#### S3 Bucket

- Name: `rag-chatbot-pdfs-yourname`
- Region: `eu-north-1` (or your preferred region)
- Block all public access

#### DynamoDB Table

- Name: `ChatHistory`
- Partition key: `session_id` (String)
- Sort key: `timestamp` (Number)
- Billing: On-demand

#### IAM User

- Create an IAM user for programmatic access.
- Attach: `AmazonS3FullAccess`, `AmazonDynamoDBFullAccess`.
- Save Access Key ID and Secret.

---

### 3. OpenAI API Key

- Get your key at [OpenAI API Keys](https://platform.openai.com/api-keys).

---

### 4. Create `.streamlit/secrets.toml`

Create `.streamlit/secrets.toml` in your repo root:

```
# OpenAI
OPENAI_API_KEY = "sk-proj-...your-openai-key..."

# AWS
AWS_ACCESS_KEY_ID = "AKIA..."
AWS_SECRET_ACCESS_KEY = "your-secret-aws-key"
AWS_REGION = "eu-north-1"

# S3
S3_BUCKET_NAME = "rag-chatbot-pdfs-yourname"
```

**Never commit `secrets.toml` to your repository!** (It's in `.gitignore`.)

---

### 5. Run Locally

```
streamlit run app.py
```
Go to http://localhost:8501.

---

## ☁️ Streamlit Cloud Deployment

1. **Push to GitHub:**
    ```
    git add .
    git commit -m "Initial commit"
    git push
    ```
2. **Deploy:**
    - Go to [Streamlit Community Cloud](https://share.streamlit.io/)
    - "New app" → select repo → file: `app.py`
3. **Add Secrets:**
    - In **Advanced settings > Secrets**, paste the full content of `.streamlit/secrets.toml`.
4. **Deploy and open your app!**

---

## 💡 Usage

- **Upload PDFs**: Use the sidebar file uploader.
- **Process**: Click "Upload & Process" to embed new PDFs.
- **Chat**: Type and send questions about your documents.
- **Get Sources**: Answers include document citations.
- **Show S3 PDFs / Clear Chat**: Use sidebar controls for file management and session cleanup.

---

## 🐛 Troubleshooting

- **DynamoDB error:** Check table name, partition/sort keys, and region.
- **S3 error:** Check bucket name/region and AWS credentials.
- **OpenAI authentication:** Verify your key in `secrets.toml`.
- **Dependency errors:** Use the exact `requirements.txt` provided.

For debugging, add this snippet in the sidebar to check installed versions:

```
import importlib.metadata
st.sidebar.write(f"openai: {importlib.metadata.version('openai')}")
st.sidebar.write(f"langchain: {importlib.metadata.version('langchain')}")
```
Expected output:
```
openai: 1.6.1
langchain: 0.1.0
```

---

## 📂 Project Layout

```
rag-chatbot-streamlit/
├── app.py
├── aws_utils.py
├── requirements.txt
├── .streamlit/
│   ├── config.toml
│   ├── runtime.txt
│   └── secrets.toml (never commit!)
├── .gitignore
└── README.md
```

---

## 🔒 Security Checklist

- No secrets or API keys will ever be committed to Git.
- IAM user has minimum required permissions.
- S3 bucket is not public.
- Chat history only—no sensitive data—goes into DynamoDB.

---

## 📊 Cost Estimate

| Service        | Typical Monthly Cost  |
| -------------- | -------------------- |
| OpenAI         | $1–5 (light usage)   |
| S3             | <$1                  |
| DynamoDB       | Free in free tier    |
| Streamlit Cloud| Free                 |
| **Total**      | $1–6/month           |

---

## 📄 License

MIT License – see the [LICENSE](LICENSE) file.

---

## 🙏 Acknowledgments

- [Streamlit](https://streamlit.io/)
- [LangChain](https://langchain.com/)
- [OpenAI](https://openai.com/)
- [FAISS](https://github.com/facebookresearch/faiss)
- [AWS](https://aws.amazon.com/)

---

**Questions?** Open an issue on GitHub.

---

_Made with ❤️ using Streamlit + AWS_
```