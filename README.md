# AAC Communication App

> An AI-powered communication app for non-verbal autistic individuals using computer vision, intelligent sentence construction, and adaptive learning.

## Overview

This application helps non-verbal individuals communicate by:
1. **Taking photos** of their environment
2. **Identifying objects and people** using AI
3. **Building sentences** with smart verb/modifier suggestions
4. **Speaking** the sentences aloud with text-to-speech
5. **Learning** from feedback to personalize suggestions over time

## Key Features

### Core Functionality
- 📸 **Camera Integration**: Capture images from phone/tablet camera
- 🔍 **Object Detection**: Azure Computer Vision API identifies objects with bounding boxes
- 👆 **Touch Selection**: Click on detected objects to start sentence building
- 💬 **Smart Suggestions**: Context-aware verb and modifier recommendations
- 🔊 **Text-to-Speech**: Natural voice output via Web Speech API
- 📊 **Adaptive Learning**: Reinforcement learning personalizes to user patterns

### User Experience
- 🎨 **Icon-Based Interface**: Emojis for verbs, pictures for objects
- ♿ **Accessibility First**: WCAG AAA compliant, large touch targets (60px+)
- 🌙 **High Contrast Mode**: Optimized for visual clarity
- 📱 **Mobile Optimized**: Designed for tablets and phones
- ⚡ **Offline Capable**: PWA with local object detection (Phase 4)

### For Caregivers
- 📈 **Dashboard**: Track communication patterns
- ⭐ **Custom Library**: Add family photos and personal items
- 📊 **Analytics**: Insights into commonly used phrases
- 👥 **Multiple Users**: Manage multiple individuals
- 📤 **Data Export**: Download communication logs for therapy

## Technology Stack

### Frontend
- **Framework**: Vue 3 (Composition API)
- **Build**: Vite
- **Styling**: Tailwind CSS
- **State**: Pinia
- **Router**: Vue Router
- **HTTP**: Axios
- **TTS**: Web Speech API

### Backend
- **Framework**: FastAPI (Python 3.11+)
- **ORM**: SQLAlchemy 2.0
- **Migrations**: Alembic
- **Auth**: JWT (python-jose)
- **Validation**: Pydantic v2
- **Testing**: pytest

### Cloud Infrastructure (Azure)
- **Computer Vision API**: Object detection (5,000 free images/month)
- **App Service**: Backend hosting
- **PostgreSQL**: Flexible Server database
- **Blob Storage**: Temporary image storage
- **Key Vault**: Secrets management
- **Application Insights**: Monitoring

### Database
- **Production**: PostgreSQL 14+
- **Development**: PostgreSQL or SQLite
- **Cache**: Redis (optional)

## Project Structure

```
aac-communication-app/
├── backend/                      # Python FastAPI backend
│   ├── alembic/                 # Database migrations
│   │   └── versions/            # Migration files
│   ├── app/
│   │   ├── main.py             # FastAPI application entry
│   │   ├── config.py           # Settings and configuration
│   │   ├── models/             # SQLAlchemy models
│   │   │   ├── __init__.py
│   │   │   ├── user.py
│   │   │   ├── object.py
│   │   │   ├── verb.py
│   │   │   ├── sentence.py
│   │   │   └── learning.py
│   │   ├── schemas/            # Pydantic schemas
│   │   │   ├── __init__.py
│   │   │   ├── user.py
│   │   │   ├── object.py
│   │   │   ├── verb.py
│   │   │   └── sentence.py
│   │   ├── routers/            # API endpoints
│   │   │   ├── __init__.py
│   │   │   ├── auth.py
│   │   │   ├── images.py
│   │   │   ├── objects.py
│   │   │   ├── verbs.py
│   │   │   ├── sentences.py
│   │   │   ├── feedback.py
│   │   │   └── caregiver.py
│   │   ├── services/           # Business logic
│   │   │   ├── __init__.py
│   │   │   ├── vision_service.py      # Azure CV integration
│   │   │   ├── verb_service.py        # Verb suggestions
│   │   │   ├── sentence_service.py    # Sentence construction
│   │   │   ├── learning_service.py    # RL algorithm
│   │   │   └── feedback_service.py    # Feedback processing
│   │   └── utils/              # Helper functions
│   │       ├── __init__.py
│   │       ├── auth.py
│   │       └── logging.py
│   ├── tests/                  # Backend tests
│   │   ├── test_api/
│   │   ├── test_services/
│   │   └── test_models/
│   ├── requirements.txt        # Python dependencies
│   ├── pyproject.toml         # Python project config
│   ├── .env.example           # Environment variables template
│   └── alembic.ini            # Alembic configuration
│
├── frontend/                    # Vue 3 frontend
│   ├── public/                 # Static assets
│   │   ├── icons/             # App icons for PWA
│   │   └── robots.txt
│   ├── src/
│   │   ├── assets/            # Images, fonts, etc.
│   │   │   ├── icons/         # Emoji/icon library
│   │   │   └── images/
│   │   ├── components/        # Vue components
│   │   │   ├── common/        # Reusable components
│   │   │   │   ├── Button.vue
│   │   │   │   ├── Icon.vue
│   │   │   │   └── Modal.vue
│   │   │   ├── camera/        # Camera components
│   │   │   │   ├── CameraCapture.vue
│   │   │   │   └── ImageViewer.vue
│   │   │   ├── objects/       # Object selection
│   │   │   │   ├── ObjectSelector.vue
│   │   │   │   ├── ObjectGrid.vue
│   │   │   │   └── ObjectLibrary.vue
│   │   │   ├── sentence/      # Sentence building
│   │   │   │   ├── SentenceBuilder.vue
│   │   │   │   ├── VerbSelector.vue
│   │   │   │   └── ModifierSelector.vue
│   │   │   ├── speech/        # TTS components
│   │   │   │   └── SpeechOutput.vue
│   │   │   └── caregiver/     # Caregiver dashboard
│   │   │       ├── Dashboard.vue
│   │   │       ├── Analytics.vue
│   │   │       └── Settings.vue
│   │   ├── composables/       # Composition API composables
│   │   │   ├── useCamera.js
│   │   │   ├── useSpeech.js
│   │   │   └── useAuth.js
│   │   ├── stores/            # Pinia stores
│   │   │   ├── auth.js
│   │   │   ├── communication.js
│   │   │   ├── objects.js
│   │   │   └── learning.js
│   │   ├── services/          # API clients
│   │   │   ├── api.js         # Axios instance
│   │   │   ├── auth.service.js
│   │   │   ├── object.service.js
│   │   │   └── sentence.service.js
│   │   ├── views/             # Page components
│   │   │   ├── Home.vue
│   │   │   ├── Camera.vue
│   │   │   ├── Build.vue
│   │   │   └── Settings.vue
│   │   ├── router/            # Vue Router config
│   │   │   └── index.js
│   │   ├── utils/             # Helper functions
│   │   │   └── helpers.js
│   │   ├── App.vue            # Root component
│   │   └── main.js            # Application entry
│   ├── tests/                 # Frontend tests
│   │   └── unit/
│   ├── index.html             # HTML entry point
│   ├── package.json           # NPM dependencies
│   ├── vite.config.js         # Vite configuration
│   ├── tailwind.config.js     # Tailwind configuration
│   ├── postcss.config.js      # PostCSS configuration
│   └── .env.example           # Environment variables template
│
├── database/                    # Database files
│   ├── schema.sql              # PostgreSQL schema
│   ├── seed_objects.sql        # Object library seed data
│   └── seed_verbs.sql          # Verb library seed data
│
├── infrastructure/             # IaC and deployment
│   ├── bicep/                 # Azure Bicep templates
│   │   ├── main.bicep
│   │   ├── app-service.bicep
│   │   ├── database.bicep
│   │   └── storage.bicep
│   └── scripts/               # Deployment scripts
│       ├── deploy-dev.sh
│       ├── deploy-staging.sh
│       └── deploy-prod.sh
│
├── docs/                        # Documentation
│   ├── DATABASE.md             # Database schema docs
│   ├── API.md                  # API documentation
│   ├── ARCHITECTURE.md         # System architecture
│   ├── DEPLOYMENT.md           # Deployment guide
│   └── DEVELOPMENT.md          # Development standards
│
├── .github/                     # GitHub configuration
│   ├── workflows/              # GitHub Actions
│   │   ├── backend-ci.yml
│   │   ├── frontend-ci.yml
│   │   ├── deploy-staging.yml
│   │   └── deploy-production.yml
│   ├── ISSUE_TEMPLATE/         # Issue templates
│   │   ├── bug_report.md
│   │   └── feature_request.md
│   └── pull_request_template.md
│
├── .gitignore                   # Git ignore rules
├── LICENSE                      # MIT License
├── README.md                    # This file
├── REQUIREMENTS.md              # Detailed requirements
├── TODO.md                      # Development roadmap
├── FUTURE.md                    # Long-term vision
├── PROJECT_SUMMARY.md           # Executive summary
├── GITHUB_SETUP.md              # GitHub setup guide
├── CODE_OF_CONDUCT.md           # Code of conduct
├── CONTRIBUTING.md              # Contribution guidelines
├── SECURITY.md                  # Security policy
└── CHANGELOG.md                 # Version history
```

## Quick Start

### Prerequisites
- **Python**: 3.11 or higher
- **Node.js**: 18 or higher
- **PostgreSQL**: 14 or higher
- **Azure Account**: Free trial or paid subscription
- **Git**: Version control

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/aac-communication-app.git
cd aac-communication-app
```

### 2. Backend Setup

```bash
# Navigate to backend
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On macOS/Linux:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Copy environment template
cp .env.example .env

# Edit .env with your configuration
# Required: DATABASE_URL, AZURE_CV_KEY, AZURE_CV_ENDPOINT, SECRET_KEY

# Run database migrations
alembic upgrade head

# Start development server
uvicorn app.main:app --reload --port 8000
```

Backend will be available at: http://localhost:8000
API documentation: http://localhost:8000/docs

### 3. Frontend Setup

```bash
# Open new terminal, navigate to frontend
cd frontend

# Install dependencies
npm install

# Copy environment template
cp .env.example .env

# Edit .env with your configuration
# Required: VITE_API_BASE_URL

# Start development server
npm run dev
```

Frontend will be available at: http://localhost:5173

### 4. Database Setup

```bash
# Create database
createdb aac_db

# Run schema (from database/ directory)
psql aac_db < database/schema.sql

# Load seed data
psql aac_db < database/seed_objects.sql
psql aac_db < database/seed_verbs.sql
```

## Azure Setup

### 1. Create Azure Resources

```bash
# Login to Azure
az login

# Create resource group
az group create --name aac-app-rg --location eastus

# Create Computer Vision (free tier: 5,000 images/month)
az cognitiveservices account create \
  --name aac-computer-vision \
  --resource-group aac-app-rg \
  --kind ComputerVision \
  --sku F0 \
  --location eastus

# Get Computer Vision key and endpoint
az cognitiveservices account keys list \
  --name aac-computer-vision \
  --resource-group aac-app-rg

# Create PostgreSQL server
az postgres flexible-server create \
  --name aac-postgres-server \
  --resource-group aac-app-rg \
  --location eastus \
  --admin-user aacadmin \
  --admin-password <your-secure-password> \
  --sku-name Standard_B1ms \
  --tier Burstable \
  --storage-size 32

# Create storage account
az storage account create \
  --name aacstorageaccount \
  --resource-group aac-app-rg \
  --location eastus \
  --sku Standard_LRS

# Create Key Vault
az keyvault create \
  --name aac-keyvault \
  --resource-group aac-app-rg \
  --location eastus
```

### 2. Store Secrets in Key Vault

```bash
# Store database connection string
az keyvault secret set \
  --vault-name aac-keyvault \
  --name DATABASE-URL \
  --value "<your-connection-string>"

# Store Computer Vision key
az keyvault secret set \
  --vault-name aac-keyvault \
  --name AZURE-CV-KEY \
  --value "<your-cv-key>"

# Store secret key for JWT
az keyvault secret set \
  --vault-name aac-keyvault \
  --name SECRET-KEY \
  --value "<your-secret-key>"
```

## Configuration

### Backend Environment Variables (.env)

```env
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/aac_db

# Azure Computer Vision
AZURE_CV_KEY=your_computer_vision_key
AZURE_CV_ENDPOINT=https://your-endpoint.cognitiveservices.azure.com/

# Azure Storage
AZURE_STORAGE_CONNECTION_STRING=your_connection_string
AZURE_STORAGE_CONTAINER=images

# Security
SECRET_KEY=your_secret_key_for_jwt
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30

# Environment
ENVIRONMENT=development
DEBUG=True
```

### Frontend Environment Variables (.env)

```env
VITE_API_BASE_URL=http://localhost:8000
VITE_APP_TITLE=AAC Communication App
VITE_ENABLE_OFFLINE=false
```

## API Documentation

Once the backend is running, visit:
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

### Key Endpoints

#### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login and get JWT token
- `POST /api/auth/refresh` - Refresh access token

#### Images
- `POST /api/images/upload` - Upload image for analysis
- `GET /api/images/{image_id}` - Get image details
- `DELETE /api/images/{image_id}` - Delete image

#### Objects
- `GET /api/objects/library` - Get object library
- `GET /api/objects/favorites` - Get user favorites
- `GET /api/objects/recent` - Get recently used objects
- `POST /api/objects/custom` - Add custom object

#### Verbs
- `GET /api/verbs/library` - Get verb library
- `POST /api/verbs/suggest` - Get verb suggestions for object
- `GET /api/verbs/{verb_id}` - Get verb details

#### Sentences
- `POST /api/sentences/construct` - Construct sentence
- `POST /api/sentences/speak` - Mark sentence as spoken
- `GET /api/sentences/history` - Get user's sentence history
- `POST /api/sentences/feedback` - Submit feedback

#### Learning
- `GET /api/learning/stats` - Get learning statistics
- `POST /api/learning/update` - Update learning model

See [API.md](docs/API.md) for complete documentation.

## Development

### Running Tests

#### Backend Tests
```bash
cd backend
pytest
pytest --cov=app tests/  # With coverage
```

#### Frontend Tests
```bash
cd frontend
npm run test:unit
npm run test:e2e
```

### Code Quality

#### Backend
```bash
cd backend

# Format code
black app/

# Lint code
flake8 app/

# Type checking
mypy app/
```

#### Frontend
```bash
cd frontend

# Lint
npm run lint

# Format
npm run format
```

### Database Migrations

```bash
cd backend

# Create new migration
alembic revision --autogenerate -m "Description of changes"

# Apply migrations
alembic upgrade head

# Rollback migration
alembic downgrade -1
```

## Deployment

### Staging Deployment
```bash
./infrastructure/scripts/deploy-staging.sh
```

### Production Deployment
```bash
./infrastructure/scripts/deploy-prod.sh
```

See [DEPLOYMENT.md](docs/DEPLOYMENT.md) for detailed deployment instructions.

## Cost Estimate

### MVP Phase (~5,000 images/month)
- Computer Vision: **$0** (free tier)
- App Service B1: **$13/month**
- PostgreSQL B1ms: **$12/month**
- Blob Storage: **$1/month**
- **Total: ~$26/month**

### With Local Model (Phase 4)
- Computer Vision: **$3-5/month** (70-80% reduction)
- Infrastructure: **$26/month**
- **Total: ~$30/month**

## Troubleshooting

### Backend won't start
1. Check Python version: `python --version` (need 3.11+)
2. Verify database connection in `.env`
3. Ensure virtual environment is activated
4. Run migrations: `alembic upgrade head`

### Frontend won't start
1. Check Node version: `node --version` (need 18+)
2. Delete `node_modules` and run `npm install` again
3. Verify `.env` has correct API URL
4. Clear Vite cache: `rm -rf node_modules/.vite`

### Azure Computer Vision errors
1. Verify API key is correct
2. Check endpoint URL format
3. Ensure free tier quota (5,000/month) not exceeded
4. Verify image format (JPEG, PNG, GIF, BMP)

### Database connection issues
1. Verify PostgreSQL is running: `pg_isready`
2. Check connection string format
3. Ensure database exists: `psql -l`
4. Verify firewall rules (Azure PostgreSQL)

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Development Workflow
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Write/update tests
5. Ensure all tests pass
6. Commit your changes (`git commit -m 'Add amazing feature'`)
7. Push to branch (`git push origin feature/amazing-feature`)
8. Open a Pull Request

### Code of Conduct
Please read [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) before contributing.

## Documentation

- **[REQUIREMENTS.md](REQUIREMENTS.md)** - Detailed functional and non-functional requirements
- **[TODO.md](TODO.md)** - Development roadmap with 144 prioritized tasks
- **[FUTURE.md](FUTURE.md)** - Long-term vision and potential features
- **[PROJECT_SUMMARY.md](PROJECT_SUMMARY.md)** - Executive summary
- **[docs/DATABASE.md](docs/DATABASE.md)** - Database schema and relationships
- **[docs/API.md](docs/API.md)** - Complete API reference
- **[docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)** - System architecture and design patterns
- **[docs/DEPLOYMENT.md](docs/DEPLOYMENT.md)** - Deployment procedures
- **[docs/DEVELOPMENT.md](docs/DEVELOPMENT.md)** - Development standards and practices

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built for non-verbal autistic individuals to communicate more effectively
- Inspired by AAC best practices and user-centered design
- Thanks to the open-source community for the amazing tools and frameworks

## Support

- **Issues**: https://github.com/yourusername/aac-communication-app/issues
- **Discussions**: https://github.com/yourusername/aac-communication-app/discussions
- **Email**: your-email@example.com

---

**Built with ❤️ to empower communication**
