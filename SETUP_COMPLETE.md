# SpeakOut AAC App - Setup Complete ✅

## Project Overview

**SpeakOut** is an AI-powered AAC (Augmentative and Alternative Communication) app designed to help non-verbal autistic individuals communicate more effectively through:
- 📸 Camera-based object recognition
- 💬 Intelligent sentence construction
- 🔊 Text-to-speech output
- 🧠 Adaptive learning from user feedback

---

## Documentation Status

### ✅ Core Planning Documents (6/6 Complete)

All planning documents have been successfully created:

| Document | Size | Status | Description |
|----------|------|--------|-------------|
| **README.md** | 19 KB | ✅ Complete | Project overview, setup instructions, tech stack |
| **PROJECT_SUMMARY.md** | 12 KB | ✅ Complete | Executive summary, architecture highlights |
| **REQUIREMENTS.md** | 14 KB | ✅ Complete | Functional & non-functional requirements |
| **TODO.md** | 20 KB | ✅ Complete | 196 tasks across 5 phases (20 weeks) |
| **FUTURE.md** | 15 KB | ✅ Complete | Long-term vision, moonshot ideas |
| **GITHUB_SETUP.md** | 18 KB | ✅ Complete | Repository setup guide |

**Total Documentation**: ~98 KB of comprehensive planning

---

## Technology Stack

### Frontend
- **Vue 3** (Composition API)
- **Vite** (Build tool)
- **Tailwind CSS** (Styling)
- **Pinia** (State management)
- **Axios** (HTTP client)
- **Web Speech API** (Text-to-speech)

### Backend
- **Python 3.11+**
- **FastAPI** (Web framework)
- **SQLAlchemy 2.0** (ORM)
- **PostgreSQL** (Database)
- **Alembic** (Migrations)
- **pytest** (Testing)

### Cloud (Azure)
- **Computer Vision API** (Object detection)
- **App Service** (Backend hosting)
- **PostgreSQL** (Managed database)
- **Blob Storage** (Image storage)
- **Key Vault** (Secrets)

### Cost Estimate
- **MVP**: ~$26/month (with free tier: 5,000 images/month)
- **With local YOLO**: ~$30/month (70-80% cost reduction)

---

## Project Structure

```
SpeakOut/
├── README.md                    # Project overview
├── PROJECT_SUMMARY.md           # Executive summary
├── REQUIREMENTS.md              # Detailed requirements
├── TODO.md                      # Development roadmap (196 tasks)
├── FUTURE.md                    # Long-term vision
├── GITHUB_SETUP.md              # Repository setup guide
├── SETUP_COMPLETE.md            # This file
├── generate_docs.py             # Documentation generator
└── extract.md                   # Original Claude conversation

Future structure (from TODO.md):
├── backend/                     # Python FastAPI backend
│   ├── app/
│   │   ├── models/             # SQLAlchemy models
│   │   ├── schemas/            # Pydantic schemas
│   │   ├── routers/            # API endpoints
│   │   ├── services/           # Business logic
│   │   └── utils/              # Helper functions
│   ├── tests/                  # Backend tests
│   └── requirements.txt        # Python dependencies
│
├── frontend/                    # Vue 3 frontend
│   ├── src/
│   │   ├── components/         # Vue components
│   │   ├── stores/             # Pinia stores
│   │   ├── views/              # Page components
│   │   └── services/           # API clients
│   └── tests/                  # Frontend tests
│
├── database/                    # Database files
│   ├── schema.sql              # PostgreSQL schema
│   ├── seed_objects.sql        # Object library seed
│   └── seed_verbs.sql          # Verb library seed
│
├── docs/                        # Technical documentation
│   ├── DATABASE.md             # Database schema
│   ├── API.md                  # API specification
│   ├── ARCHITECTURE.md         # System architecture
│   ├── DEPLOYMENT.md           # Deployment guide
│   └── DEVELOPMENT.md          # Coding standards
│
└── .github/                     # GitHub configuration
    ├── workflows/              # CI/CD pipelines
    └── ISSUE_TEMPLATE/         # Issue templates
```

---

## Development Roadmap (20 Weeks)

### Phase 1: MVP (Weeks 1-4) - 93 tasks
**Goal**: Basic functional prototype

- [x] Project setup and planning documents
- [ ] Azure infrastructure provisioning
- [ ] Database schema and migrations
- [ ] Backend API (FastAPI + Azure Computer Vision)
- [ ] Frontend UI (Vue 3 + camera + sentence builder)
- [ ] Authentication (JWT)
- [ ] Text-to-speech (Web Speech API)
- [ ] Feedback collection

**Deliverable**: Working app that captures images, detects objects, builds sentences, and speaks them.

### Phase 2: Enhanced Intelligence (Weeks 5-8) - 35 tasks
- Context-aware verb suggestions
- Favorites and recent items
- Learning from feedback
- Caregiver dashboard
- User customization

### Phase 3: Advanced Learning (Weeks 9-12) - 28 tasks
- Q-learning reinforcement learning
- User-specific personalization
- Face recognition (optional)
- Custom object library
- Usage analytics

### Phase 4: Offline & Mobile (Weeks 13-16) - 22 tasks
- Progressive Web App (PWA)
- Offline mode with local YOLO
- Native mobile apps (iOS/Android)
- Background sync

### Phase 5: Extended Features (Weeks 17-20) - 18 tasks
- Pre-made common phrases
- Emotion selection
- Schedule/routine builder
- Multi-language support

**Total**: 196 prioritized tasks

---

## Next Steps

### Immediate (Today/This Week)

1. **Review Documentation**
   - Read README.md for overview
   - Review REQUIREMENTS.md for scope
   - Check TODO.md Phase 1 tasks

2. **Set Up Development Environment**
   - Install Python 3.11+
   - Install Node.js 18+
   - Install PostgreSQL 14+
   - Set up Azure account

3. **Create GitHub Repository**
   - Follow GITHUB_SETUP.md step-by-step
   - Create repository
   - Add issue/PR templates
   - Set up CI/CD workflows

4. **Provision Azure Resources**
   ```bash
   az login
   az group create --name aac-app-rg --location eastus
   az cognitiveservices account create --name aac-cv --kind ComputerVision --sku F0 ...
   az postgres flexible-server create --name aac-postgres ...
   ```

### Week 1 (Backend Foundation)
- Create project structure
- Set up PostgreSQL database
- Create SQLAlchemy models
- Build FastAPI app skeleton
- Implement authentication
- Integrate Azure Computer Vision

### Week 2 (Core API)
- Build image upload endpoint
- Build object detection endpoint
- Build verb suggestion logic
- Build sentence construction endpoint
- Write backend tests

### Week 3 (Frontend Foundation)
- Initialize Vue 3 project
- Set up Tailwind CSS
- Create Pinia stores
- Build camera component
- Build object selector component

### Week 4 (Integration & MVP)
- Build sentence builder component
- Implement TTS
- Connect frontend to backend
- End-to-end testing
- Deploy MVP to staging
- User testing with your brother-in-law

---

## Key Features (MVP)

### User Experience
- ✅ Capture photo with device camera
- ✅ AI identifies objects with bounding boxes
- ✅ Tap to select object
- ✅ Choose verb from smart suggestions (3-5 options)
- ✅ Optionally add modifier (please, now, etc.)
- ✅ Preview sentence
- ✅ Speak sentence aloud
- ✅ Provide feedback (thumbs up/down)

### Technical
- ✅ Azure Computer Vision object detection
- ✅ Rule-based verb suggestions by object category
- ✅ Template-based sentence construction
- ✅ Web Speech API for TTS
- ✅ PostgreSQL database
- ✅ JWT authentication
- ✅ Responsive Tailwind UI
- ✅ WCAG AAA accessibility

---

## Accessibility Highlights

All features designed with accessibility in mind:

- **Visual**: 60px minimum touch targets, WCAG AAA contrast (7:1)
- **Cognitive**: 3-5 options per screen, progressive disclosure
- **Motor**: Large well-spaced buttons, no time limits
- **Auditory**: Visual alternatives for all audio

---

## Success Criteria

### User Experience
- [ ] 95% object detection accuracy
- [ ] <30 second sentence construction time
- [ ] 80% user satisfaction
- [ ] 30% suggestion improvement after 100 uses

### Technical
- [ ] 99.9% uptime
- [ ] <2 second page load
- [ ] <3 second object detection
- [ ] 80%+ test coverage

---

## Resources

### Documentation
- [README.md](README.md) - Start here
- [REQUIREMENTS.md](REQUIREMENTS.md) - Full requirements
- [TODO.md](TODO.md) - Task breakdown
- [FUTURE.md](FUTURE.md) - Long-term vision
- [GITHUB_SETUP.md](GITHUB_SETUP.md) - Repo setup

### Tools & Utilities
- `generate_docs.py` - Regenerate planning docs if needed

### External Tools
Location: `/mnt/d/dev2/claude2files/`

- **claude_artifact_extractor.py** - Extract artifacts from Claude conversations
- Can be used for future Claude conversations to extract code/docs

---

## Contact & Support

### Purpose
Building an AAC communication app for your non-verbal autistic brother-in-law to help him communicate more effectively.

### Repository
*(To be created - follow GITHUB_SETUP.md)*

---

## Quick Reference

### Start Backend (Future)
```bash
cd backend
source venv/bin/activate
uvicorn app.main:app --reload
```

### Start Frontend (Future)
```bash
cd frontend
npm run dev
```

### Run Tests (Future)
```bash
# Backend
cd backend && pytest

# Frontend
cd frontend && npm run test
```

### Deploy (Future)
```bash
./infrastructure/scripts/deploy-staging.sh
```

---

## License

MIT License

---

## Acknowledgments

- Built with ❤️ to empower non-verbal individuals
- Inspired by AAC best practices
- Thanks to the open-source community

---

**Status**: ✅ Planning Complete - Ready to Begin Development

**Next Step**: Follow GITHUB_SETUP.md to create your repository, then begin Phase 1 from TODO.md

**Last Updated**: 2025-10-31
