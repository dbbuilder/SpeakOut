# AAC Communication App - Project Summary

## Executive Summary

The AAC (Augmentative and Alternative Communication) Communication App is an AI-powered mobile and web application designed to help non-verbal autistic individuals communicate more effectively. The app enables users to take photos, identify objects and people, and construct grammatically correct sentences through an intuitive, icon-based interface with adaptive learning capabilities.

## Core Problem

Non-verbal autistic individuals face significant communication barriers despite cognitive abilities. Traditional AAC systems are often:
- Limited to pre-programmed phrases
- Require extensive setup and customization
- Don't adapt to individual communication patterns
- Lack real-world object recognition

## Our Solution

An intelligent AAC app that combines:
1. **Visual Input**: Camera-based object recognition using Azure Computer Vision
2. **Smart Construction**: AI-suggested verbs and modifiers based on context
3. **Adaptive Learning**: Reinforcement learning that personalizes to individual patterns
4. **Natural Output**: Text-to-speech with grammatically correct sentences
5. **Accessibility First**: Large touch targets, high contrast, minimal cognitive load

## Key Features

### Phase 1: MVP (Weeks 1-4)
- Camera capture and real-time object detection
- Click-to-select interface with bounding boxes
- 20-30 common verbs with emoji icons
- Basic sentence templates: "I [verb] [object]", "[Object] please"
- Web Speech API text-to-speech
- Feedback collection (thumbs up/down)

### Phase 2: Enhanced Intelligence (Weeks 5-8)
- Context-aware verb suggestions
- Modifier/request options (please, now, later, more)
- Favorites and recent items
- Frequency-based learning
- Caregiver dashboard

### Phase 3: Advanced Learning (Weeks 9-12)
- Q-learning reinforcement learning
- User-specific personalization
- Face recognition for known people
- Custom object library
- Usage analytics

### Phase 4: Offline & Mobile (Weeks 13-16)
- Progressive Web App (PWA)
- Offline mode with local object detection (YOLO)
- Native mobile app (Capacitor)
- Background sync

### Phase 5: Extended Features (Weeks 17-20)
- Pre-made common phrases
- Emotion selection
- Schedule/routine builder
- Multi-language support

## Technology Stack

### Frontend
- **Framework**: Vue 3 with Composition API
- **Build Tool**: Vite
- **Styling**: Tailwind CSS
- **State Management**: Pinia
- **Routing**: Vue Router
- **API Client**: Axios
- **TTS**: Web Speech API

### Backend
- **Framework**: FastAPI (Python 3.11+)
- **Database ORM**: SQLAlchemy 2.0
- **Migrations**: Alembic
- **Authentication**: JWT (python-jose)
- **Validation**: Pydantic v2
- **Testing**: pytest, pytest-asyncio

### Azure Services
- **Computer Vision API**: Object detection (F0 free tier: 5,000 images/month)
- **App Service**: Linux-based Python hosting
- **Database for PostgreSQL**: Flexible Server (B1ms tier)
- **Blob Storage**: Temporary image storage
- **Key Vault**: Secrets management
- **Application Insights**: Monitoring and analytics

### Database
- **Primary**: PostgreSQL 14+
- **Cache**: Redis (optional for Phase 2+)
- **Local**: SQLite (offline mode in Phase 4)

## Cost Estimate

### MVP Phase (Light Usage ~5,000 images/month)
- Computer Vision: **$0** (within free tier)
- App Service B1: **$13/month**
- PostgreSQL B1ms: **$12/month**
- Blob Storage: **$1/month**
- **Total: ~$26/month**

### Moderate Usage (20,000 images/month)
- Computer Vision: **$22.50** (5k free, 15k @ $1.50/1k)
- Infrastructure: **$26**
- **Total: ~$48.50/month**

### Cost Optimization Strategy
- Phase 4 adds local YOLO model (reduces CV API calls by 70-80%)
- Expected reduction to **~$30/month** after local model implementation

## Architecture Highlights

### Data Flow
1. User captures image → Upload to Azure Blob Storage
2. Backend calls Azure Computer Vision API → Object detection
3. Returns bounding boxes + labels → Display on frontend
4. User selects object → Backend suggests verbs (rule-based initially)
5. User selects verb → Backend suggests modifiers
6. Sentence constructed → Web Speech API speaks it
7. User provides feedback → Stored for learning algorithm

### Learning System
- **State**: (object_category, time_of_day, recent_verbs_used)
- **Action**: (verb_id, modifier_id)
- **Reward**:
  - +10: Explicit thumbs up
  - +5: Sentence spoken (implicit success)
  - +1: Sentence constructed but not used
  - -5: Thumbs down
  - -2: Dismissed without using
- **Algorithm**: Q-learning with ε-greedy exploration (80% exploit, 20% explore)

### Key Design Patterns
- **Repository Pattern**: Data access abstraction
- **Service Layer**: Business logic separation
- **Dependency Injection**: FastAPI's built-in DI
- **State Management**: Centralized Pinia stores
- **API-First Design**: OpenAPI/Swagger documentation
- **Progressive Enhancement**: Works without JS, better with it

## Database Schema

### Core Tables (12 total)
1. **users** - User accounts and profiles
2. **object_library** - Master list of recognizable objects
3. **verb_library** - Available verbs with icons
4. **modifier_library** - Request modifiers (please, now, etc.)
5. **detected_objects** - AI-detected objects from images
6. **sentence_templates** - Valid sentence structures
7. **constructed_sentences** - User-created sentences
8. **feedback_records** - Learning data from user feedback
9. **learning_state** - Q-learning state-action values
10. **user_favorites** - Frequently used combinations
11. **caregiver_users** - Caregiver accounts
12. **usage_analytics** - Communication pattern tracking

## Development Roadmap

### Phase 1: MVP (Weeks 1-4) - 41 Tasks
- Project setup and infrastructure
- Database schema and migrations
- Azure Computer Vision integration
- Core API endpoints (images, objects, verbs, sentences)
- Vue 3 frontend with camera and sentence builder
- Basic authentication
- TTS implementation

### Phase 2: Enhanced Intelligence (Weeks 5-8) - 35 Tasks
- Context-aware suggestions
- Favorites and recents
- Learning from feedback
- Caregiver dashboard
- User settings and customization

### Phase 3: Advanced Learning (Weeks 9-12) - 28 Tasks
- Q-learning implementation
- User-specific personalization
- Face recognition
- Custom object library
- Analytics and insights

### Phase 4: Offline & Mobile (Weeks 13-16) - 22 Tasks
- Progressive Web App
- Service Workers and offline mode
- Local YOLO object detection
- Native mobile app (Capacitor)
- Background sync

### Phase 5: Extended Features (Weeks 17-20) - 18 Tasks
- Common phrases library
- Emotion selection
- Schedule/routine builder
- Multi-language support
- Export and reporting

**Total: 144 prioritized tasks across 20 weeks**

## Success Criteria

### User Experience
- [ ] 95% of objects correctly identified in common environments
- [ ] Average sentence construction time <30 seconds
- [ ] 80% user satisfaction in feedback surveys
- [ ] Works offline for core features
- [ ] WCAG AAA accessibility compliance

### Technical Performance
- [ ] Object detection <3 seconds (cloud), <1 second (local)
- [ ] 99.9% uptime (excluding scheduled maintenance)
- [ ] <2 second page load time
- [ ] Works on devices 3+ years old
- [ ] Supports 1000+ concurrent users

### Learning System
- [ ] 30% improvement in suggestion accuracy after 100 interactions
- [ ] 50% reduction in steps to construct common phrases after 1 week
- [ ] Personalization accuracy >70% for frequent users

## Privacy & Security

### Principles
- **Data Minimization**: Only collect what's necessary
- **Temporary Storage**: Images deleted after 24 hours
- **User Control**: Export and delete all data anytime
- **Transparency**: Clear privacy policy in simple language
- **COPPA Compliance**: Suitable for users under 13

### Technical Measures
- HTTPS/TLS 1.3 for all communications
- Secrets in Azure Key Vault
- No facial recognition without explicit consent
- Encryption at rest (Azure Storage Encryption)
- JWT authentication with refresh tokens
- Rate limiting and DDoS protection

## Accessibility Considerations

### Visual
- Minimum 60px × 60px touch targets
- WCAG AAA contrast ratios
- High contrast mode option
- Adjustable icon sizes
- No color-only information

### Cognitive
- Show 3-5 options at a time (avoid overwhelm)
- Progressive disclosure (step-by-step)
- Clear visual feedback for all actions
- Undo/back at every step
- Consistent layouts and patterns

### Motor
- Large, well-spaced touch targets
- No time-based interactions
- Alternative input methods supported
- Sticky activation (no accidental clicks)

### Auditory
- Visual alternatives for all audio
- Adjustable speech rate and pitch
- Multiple TTS voice options

## Risk Management

### Technical Risks
- **Azure service outages** → Offline mode fallback
- **API rate limits exceeded** → Local YOLO model
- **Poor object recognition accuracy** → Manual override option
- **TTS browser compatibility** → Polyfill or fallback

### User Adoption Risks
- **Too complex for users** → Extensive user testing, simplified UI
- **Caregiver resistance** → Dashboard and analytics for buy-in
- **Privacy concerns** → Transparent policies, local-first architecture

### Financial Risks
- **Azure costs exceed budget** → Implement local models early
- **Low adoption** → Start with single user, expand gradually

## Long-Term Vision

### Year 1: Foundation
- Stable MVP with 10+ active users
- Proven learning algorithm effectiveness
- Strong accessibility compliance
- Offline-capable mobile app

### Year 2: Expansion
- Multi-language support (Spanish, Mandarin)
- Integration with therapy platforms
- Research partnerships (universities, hospitals)
- 100+ active users

### Year 3: Ecosystem
- Open-source core platform
- Third-party plugin ecosystem
- Commercial licensing for institutions
- API for AAC device manufacturers

### Moonshot Ideas
- Real-time sign language translation
- Brain-computer interface integration
- AR overlays for object identification
- Predictive intent (suggest before user knows)
- Multilingual family communication bridge

## Project Governance

### Repository Structure
- **Main branch**: Production-ready code
- **Develop branch**: Integration branch for features
- **Feature branches**: Individual feature development
- **Release branches**: Version preparation

### Development Workflow
1. Create issue from template
2. Create feature branch from develop
3. Implement with tests (TDD)
4. Submit pull request
5. Code review (1+ approvals)
6. Automated CI/CD checks pass
7. Merge to develop
8. Periodic releases to main

### Code Quality Standards
- 80%+ test coverage
- All linters pass (flake8, ESLint)
- Type hints for all Python functions
- JSDoc comments for complex logic
- No console.log in production

## Getting Started

### Prerequisites
- Python 3.11+
- Node.js 18+
- PostgreSQL 14+
- Azure account (or free trial)
- Git

### Quick Start
```bash
# Clone repository
git clone https://github.com/yourusername/aac-communication-app.git
cd aac-communication-app

# Backend setup
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
alembic upgrade head
uvicorn app.main:app --reload

# Frontend setup (new terminal)
cd frontend
npm install
npm run dev
```

### Documentation
- **README.md**: Project overview and setup
- **REQUIREMENTS.md**: Detailed requirements
- **TODO.md**: Development roadmap
- **docs/DATABASE.md**: Schema and queries
- **docs/API.md**: API endpoints and examples
- **docs/ARCHITECTURE.md**: System design
- **docs/DEPLOYMENT.md**: Azure deployment
- **docs/DEVELOPMENT.md**: Coding standards

## Contact & Support

### Project Lead
- **Name**: [Your Name]
- **Email**: [Your Email]
- **Purpose**: AAC app for brother-in-law

### Resources
- **Issues**: https://github.com/yourusername/aac-communication-app/issues
- **Discussions**: https://github.com/yourusername/aac-communication-app/discussions
- **Documentation**: https://github.com/yourusername/aac-communication-app/wiki

## License

MIT License - See LICENSE file for details

---

**Built with ❤️ to help non-verbal individuals communicate**
