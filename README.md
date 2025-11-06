# 📄 Form Data Extractor

An intelligent document processing application that extracts and structures data from forms, invoices, and other documents using OCR and AI.

![Status](https://img.shields.io/badge/status-active-success.svg)
![Node](https://img.shields.io/badge/node-%3E%3D16.0.0-brightgreen.svg)

## 🌟 Features

- **Smart OCR**: Extract text from PDFs and images using Azure Computer Vision
- **AI Structuring**: Automatically convert extracted text to structured JSON using Groq AI
- **Database Storage**: Store documents in PostgreSQL with before/after verification workflows
- **Interactive UI**: Material-UI table with inline editing capabilities
- **Batch Processing**: Upload multiple files at once
- **Production Ready**: Deployed on Render.com with environment-based configuration

## 🚀 Live Demo

- **Frontend**: [Your Frontend URL will be here]
- **Backend API**: [Your Backend URL will be here]

## 🛠️ Tech Stack

### Frontend
- React 19 with Vite
- Material-UI (MUI) & Tailwind CSS
- Material React Table
- Lucide React Icons

### Backend
- Node.js & Express
- PostgreSQL (Neon)
- Azure Computer Vision API
- Groq AI (llama-3.3-70b-versatile)
- Multer for file uploads
- pdf-poppler for PDF processing

## 📋 Prerequisites

- Node.js >= 16.0.0
- PostgreSQL database (or Neon account)
- Azure Computer Vision API key
- Groq API key

## 🔧 Local Development Setup

### 1. Clone the repository

```bash
git clone https://github.com/Santosh7131/Santosh7131-Form-Data-Extractor-Deploy.git
cd Santosh7131-Form-Data-Extractor-Deploy
```

### 2. Backend Setup

```bash
cd backend
npm install

# Create .env file (copy from .env.example)
cp .env.example .env
```

Edit `backend/.env` with your credentials:

```env
GROQ_API_KEY=your_groq_api_key
AZURE_ENDPOINT=https://your-resource.cognitiveservices.azure.com/
AZURE_API_KEY=your_azure_key
NEON_DB_URL=your_neon_database_url
NEON_AFTER_DB_URL=your_after_verification_database_url
```

Start backend server:
```bash
npm start
# Server runs on http://localhost:5000
```

### 3. Frontend Setup

```bash
cd my-react-app
npm install
npm run dev
# Frontend runs on http://localhost:5173
```

## 🌐 Deployment to Render.com

### Step 1: Push to GitHub

Ensure your `.env` files are in `.gitignore` (already configured):

```bash
git add .
git commit -m "Ready for deployment"
git push origin main
```

### Step 2: Create Render Account

1. Go to [render.com](https://render.com)
2. Sign up/login with your GitHub account
3. Authorize Render to access your repositories

### Step 3: Deploy Backend

1. Click **"New +"** → **"Blueprint"**
2. Connect your repository: `Santosh7131-Form-Data-Extractor-Deploy`
3. Render will detect `render.yaml` automatically
4. Click **"Apply"**

### Step 4: Set Environment Variables

For **form-extractor-backend** service:

Navigate to your backend service → **Environment** → Add:

```
GROQ_API_KEY=gsk_your_actual_groq_key
AZURE_ENDPOINT=https://your-resource.cognitiveservices.azure.com/
AZURE_API_KEY=your_azure_key
NEON_DB_URL=postgresql://user:pass@host/database
NEON_AFTER_DB_URL=postgresql://user:pass@host/database_after
```

For **form-extractor-frontend** service:

```
VITE_API_URL=https://form-extractor-backend.onrender.com
```

**Important**: Replace `form-extractor-backend` with your actual backend service name from Render.

### Step 5: Deploy

1. Render will automatically deploy both services
2. Backend URL: `https://form-extractor-backend.onrender.com`
3. Frontend URL: `https://form-extractor-frontend.onrender.com`

⚠️ **Note**: Free tier services sleep after 15 minutes of inactivity. First request may take 30-50 seconds to wake up.

## 🔑 Getting API Keys

### Groq API Key
1. Visit [console.groq.com](https://console.groq.com)
2. Sign up/login
3. Go to **API Keys** → **Create API Key**
4. Copy the key (starts with `gsk_`)

### Azure Computer Vision
1. Go to [Azure Portal](https://portal.azure.com)
2. Create **Computer Vision** resource
3. Go to **Keys and Endpoint**
4. Copy **KEY 1** and **Endpoint**

### Neon PostgreSQL
1. Visit [console.neon.tech](https://console.neon.tech)
2. Create project
3. Copy connection string from dashboard
4. Create two databases: `before_verify2` and `after_verify2`

## 📁 Project Structure

```
├── backend/
│   ├── server.js           # Express server
│   ├── routes/
│   │   └── uploadroutes.js # API endpoints
│   ├── extractor/
│   │   └── aiApiCall.js    # OCR & AI processing
│   ├── insert_to_pg.py     # Database insertion script
│   └── .env                # Backend environment variables
├── my-react-app/
│   ├── src/
│   │   └── App.jsx         # Main React component
│   └── .env.production     # Frontend environment variables
├── render.yaml             # Render deployment config
└── README.md
```

## 🔄 Workflow

1. **Upload**: User uploads PDF/image files
2. **OCR**: Azure extracts text from documents
3. **AI Processing**: Groq structures text into JSON
4. **Storage**: Data saved to "before_verify" database
5. **Review**: User can edit data in interactive table
6. **Verify**: Approved data moves to "after_verify" database

## 🐛 Troubleshooting

### Backend not connecting to frontend
- Check `VITE_API_URL` in frontend environment variables
- Ensure CORS is enabled in backend (already configured)
- Check backend service is running on Render

### OCR/AI not working
- Verify API keys are set correctly in Render environment
- Check Azure quota limits
- Monitor Groq API rate limits (free tier: 30 requests/min)

### Database errors
- Ensure PostgreSQL connection strings are correct
- Check database exists and is accessible
- Verify SSL settings for Neon databases

### Render deployment issues
- Check build logs in Render dashboard
- Ensure `package.json` exists in correct directories
- Verify environment variables are set

## 📝 API Endpoints

- `GET /api/health` - Health check
- `POST /api/upload-images` - Upload image files
- `POST /api/upload-scanned-pdfs` - Upload PDF files
- `GET /api/all-documents` - Fetch all documents
- `POST /api/save-verified` - Save verified documents

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 👨‍💻 Author

**Santosh Kumaar**

- GitHub: [@Santosh7131](https://github.com/Santosh7131)
- Portfolio: [Your Portfolio URL]

## 🙏 Acknowledgments

- Azure Computer Vision for OCR capabilities
- Groq for AI text structuring
- Neon for PostgreSQL hosting
- Render.com for free hosting

---

⭐ Star this repo if you find it helpful!
