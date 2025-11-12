# ☁️ RAG PDF Chatbot

A Retrieval-Augmented Generation (RAG) chatbot that lets you upload PDF documents and ask questions about them using AI. Built with Streamlit, LangChain, OpenAI GPT-4o-mini, and AWS.

## 🎯 Features

- 📤 Upload multiple PDFs to AWS S3
- 🔍 Semantic search with FAISS vector database
- 🤖 AI-powered Q&A using GPT-4o-mini
- 💾 Chat history stored in DynamoDB
- 🎨 Clean Streamlit interface

## 🛠️ Tech Stack

- **Frontend**: Streamlit
- **LLM**: OpenAI GPT-4o-mini
- **Vector DB**: FAISS + Sentence Transformers
- **Storage**: AWS S3
- **Database**: AWS DynamoDB
- **Framework**: LangChain

***

## 🚀 Quick Setup

### Prerequisites

- Python 3.11+
- AWS Account (free tier works)
- OpenAI API key

### 1. Clone & Install

```bash
git clone <repo-url>
cd rag-chatbot-streamlit
pip install -r requirements.txt
```

### 2. Configure AWS

#### Create S3 Bucket
1. AWS Console → S3 → **Create bucket**
2. Name: `rag-chatbot-pdfs-yourname`
3. Region: `eu-north-1` (or your choice)
4. Keep **"Block all public access"** enabled

#### Create DynamoDB Table
1. AWS Console → DynamoDB → **Create table**
2. Table name: `ChatHistory`
3. **Partition key**: `session_id` (String)
4. **Sort key**: `timestamp` (Number)
5. Table settings: **On-demand**

#### Create IAM User
1. AWS Console → IAM → Users → **Create user**
2. Username: `rag-chatbot-user`
3. Attach policies:
   - `AmazonS3FullAccess`
   - `AmazonDynamoDBFullAccess`
4. Create **Access Key** → Save the credentials

### 3. Get OpenAI API Key

1. Go to [platform.openai.com/api-keys](https://platform.openai.com/api-keys)
2. Create new secret key
3. Copy and save it (starts with `sk-proj-...`)

### 4. Create Secrets File

Create `.streamlit/secrets.toml`:

```bash
mkdir .streamlit
touch .streamlit/secrets.toml  # Mac/Linux
# OR
type nul > .streamlit\secrets.toml  # Windows
```

Edit `.streamlit/secrets.toml`:

```toml
# OpenAI
OPENAI_API_KEY = "sk-proj-your-actual-openai-api-key"

# AWS Credentials
AWS_ACCESS_KEY_ID = "AKIA..."
AWS_SECRET_ACCESS_KEY = "your-secret-key"
AWS_REGION = "eu-north-1"

# S3 Bucket
S3_BUCKET_NAME = "rag-chatbot-pdfs-yourname"
```

⚠️ **IMPORTANT**: Never commit this file to Git! It's already in `.gitignore`.

### 5. Run Locally

```bash
streamlit run app.py
```

Visit `http://localhost:8501`

***

## ☁️ Deploy to Streamlit Cloud

### 1. Push to GitHub

```bash
git add .
git commit -m "Initial commit"
git push origin main
```

### 2. Deploy

1. Go to [share.streamlit.io](https://share.streamlit.io/)
2. Click **"New app"**
3. Select your repository
4. Main file: `app.py`

### 3. Add Secrets

In **Advanced settings** → **Secrets**, paste:

```toml
OPENAI_API_KEY = "sk-proj-..."
AWS_ACCESS_KEY_ID = "AKIA..."
AWS_SECRET_ACCESS_KEY = "..."
AWS_REGION = "eu-north-1"
S3_BUCKET_NAME = "rag-chatbot-pdfs-yourname"
```

### 4. Deploy

Click **Deploy** and wait 3-5 minutes.

***

## 💡 Usage

1. **Upload PDFs**: Use sidebar file uploader
2. **Process**: Click "Upload & Process" button
3. **Ask Questions**: Type in chat input
4. **Get Answers**: AI responds with sources cited

***

## 📂 Project Structure

```
rag-chatbot-streamlit/
├── app.py                 # Main application
├── aws_utils.py          # AWS S3 & DynamoDB utilities
├── requirements.txt      # Python dependencies
├── .streamlit/
│   ├── config.toml      # UI settings
│   ├── runtime.txt      # Python 3.11
│   └── secrets.toml     # Credentials (not in Git!)
├── .gitignore
└── README.md
```

***

## 🐛 Troubleshooting

### DynamoDB Error: "ResourceNotFoundException"
- Check table name is exactly `ChatHistory`
- Verify region in secrets matches AWS Console
- Confirm table has `session_id` (String) and `timestamp` (Number)

### S3 Error: "AccessDenied"
- Verify bucket name matches secrets.toml
- Check IAM user has S3 permissions
- Confirm bucket exists in correct region

### OpenAI Error: "AuthenticationError"
- Verify API key is correct
- Check you have credits at [platform.openai.com/usage](https://platform.openai.com/usage)

### Secrets Not Found
```bash
# Verify file exists
ls -la .streamlit/secrets.toml

# Create if missing
mkdir .streamlit
touch .streamlit/secrets.toml
```

***

## 📊 Cost Estimate

- **OpenAI**: ~$1-5/month (light usage)
- **AWS S3**: ~$0.01-0.50/month
- **AWS DynamoDB**: Free tier covers typical usage
- **Streamlit Cloud**: Free

**Total**: ~$1-6/month

***

## 🔒 Security

- ✅ Secrets in `.gitignore` (never commit!)
- ✅ Use IAM least-privilege policies
- ✅ Keep S3 bucket private (block public access)
- ✅ Rotate AWS keys every 90 days

***

## 📄 License

MIT License - see [LICENSE](LICENSE) file.

***

## 🙏 Built With

- [Streamlit](https://streamlit.io/)
- [LangChain](https://langchain.com/)
- [OpenAI](https://openai.com/)
- [FAISS](https://github.com/facebookresearch/faiss)
- [AWS](https://aws.amazon.com/)

***

**Questions?** Open an issue on GitHub.

**Made with ❤️ using Streamlit + AWS**