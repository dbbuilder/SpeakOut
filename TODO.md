# AAC Communication App - Development Roadmap

## Overview

This document outlines the complete development roadmap for the AAC Communication App across 5 phases spanning 20 weeks.

**Total Tasks**: 144
**Timeline**: 20 weeks
**Priority Levels**: P0 (Critical), P1 (High), P2 (Medium), P3 (Low)
**Effort Estimates**: S (Small: 1-4 hours), M (Medium: 4-8 hours), L (Large: 1-2 days), XL (Extra Large: 2+ days)

---

## Phase 1: MVP (Weeks 1-4)

**Goal**: Basic functional prototype with camera, object detection, sentence building, and TTS

### 1.1 Project Setup
- [ ] **[P0, S]** Create GitHub repository with proper .gitignore
- [ ] **[P0, S]** Set up branch protection rules (main, develop)
- [ ] **[P0, S]** Create issue templates (bug, feature request)
- [ ] **[P0, S]** Create pull request template
- [ ] **[P0, M]** Set up project board with milestones
- [ ] **[P0, S]** Add LICENSE (MIT)
- [ ] **[P0, S]** Create CODE_OF_CONDUCT.md
- [ ] **[P0, S]** Create CONTRIBUTING.md
- [ ] **[P0, S]** Create SECURITY.md

### 1.2 Azure Infrastructure
- [ ] **[P0, M]** Create Azure resource group
- [ ] **[P0, M]** Provision Computer Vision API (F0 free tier)
- [ ] **[P0, M]** Provision PostgreSQL Flexible Server (B1ms)
- [ ] **[P0, M]** Provision Blob Storage account
- [ ] **[P0, M]** Create Key Vault for secrets
- [ ] **[P0, M]** Set up Application Insights
- [ ] **[P0, L]** Configure networking and firewall rules
- [ ] **[P1, M]** Set up billing alerts

### 1.3 Database Design
- [ ] **[P0, L]** Design complete database schema
- [ ] **[P0, M]** Create users table with auth fields
- [ ] **[P0, M]** Create object_library table
- [ ] **[P0, M]** Create verb_library table
- [ ] **[P0, M]** Create modifier_library table
- [ ] **[P0, M]** Create detected_objects table
- [ ] **[P0, M]** Create sentence_templates table
- [ ] **[P0, M]** Create constructed_sentences table
- [ ] **[P0, M]** Create feedback_records table
- [ ] **[P0, M]** Add indexes for performance
- [ ] **[P0, M]** Add foreign key constraints
- [ ] **[P0, L]** Seed object_library with 100+ common objects
- [ ] **[P0, L]** Seed verb_library with 30+ common verbs
- [ ] **[P0, M]** Seed modifier_library with common modifiers

### 1.4 Backend Core
- [ ] **[P0, M]** Initialize FastAPI project structure
- [ ] **[P0, M]** Set up SQLAlchemy models matching schema
- [ ] **[P0, M]** Configure Alembic for migrations
- [ ] **[P0, M]** Create initial migration
- [ ] **[P0, M]** Set up Pydantic schemas for validation
- [ ] **[P0, M]** Configure environment variables (.env)
- [ ] **[P0, M]** Set up logging (stdout + Application Insights)
- [ ] **[P0, S]** Create health check endpoint (/health)
- [ ] **[P0, M]** Set up CORS middleware
- [ ] **[P0, M]** Configure database connection pooling

### 1.5 Authentication
- [ ] **[P0, L]** Implement user registration endpoint
- [ ] **[P0, L]** Implement login endpoint with JWT
- [ ] **[P0, M]** Implement refresh token logic
- [ ] **[P0, M]** Create authentication dependencies
- [ ] **[P0, M]** Hash passwords with bcrypt
- [ ] **[P0, S]** Add rate limiting middleware
- [ ] **[P1, M]** Create password reset flow

### 1.6 Azure Computer Vision Integration
- [ ] **[P0, L]** Create vision_service.py with Azure SDK
- [ ] **[P0, M]** Implement image upload to Blob Storage
- [ ] **[P0, L]** Implement object detection API call
- [ ] **[P0, M]** Parse and format detection results
- [ ] **[P0, M]** Handle confidence thresholds (0.6+)
- [ ] **[P0, M]** Implement error handling and retries
- [ ] **[P0, M]** Add result caching (Redis or in-memory)
- [ ] **[P0, S]** Set up automatic image deletion (24 hours)

### 1.7 Core API Endpoints
- [ ] **[P0, L]** POST /api/images/upload - Upload and analyze image
- [ ] **[P0, M]** GET /api/images/{id} - Get image with detected objects
- [ ] **[P0, M]** DELETE /api/images/{id} - Delete image
- [ ] **[P0, M]** GET /api/objects/library - Get object library
- [ ] **[P0, M]** GET /api/verbs/library - Get verb library
- [ ] **[P0, L]** POST /api/verbs/suggest - Get verb suggestions for object
- [ ] **[P0, M]** GET /api/modifiers/library - Get modifier library
- [ ] **[P0, L]** POST /api/sentences/construct - Construct sentence
- [ ] **[P0, M]** POST /api/sentences/speak - Log spoken sentence
- [ ] **[P0, M]** POST /api/feedback - Submit feedback
- [ ] **[P0, M]** GET /api/sentences/history - Get user's history

### 1.8 Backend Testing
- [ ] **[P0, L]** Set up pytest configuration
- [ ] **[P0, L]** Write tests for authentication endpoints
- [ ] **[P0, L]** Write tests for image upload and detection
- [ ] **[P0, M]** Write tests for verb suggestion logic
- [ ] **[P0, M]** Write tests for sentence construction
- [ ] **[P1, M]** Set up test coverage reporting
- [ ] **[P1, L]** Achieve 80%+ test coverage

### 1.9 Frontend Setup
- [ ] **[P0, M]** Initialize Vue 3 + Vite project
- [ ] **[P0, M]** Install and configure Tailwind CSS
- [ ] **[P0, M]** Set up Pinia for state management
- [ ] **[P0, M]** Set up Vue Router
- [ ] **[P0, M]** Create Axios instance with interceptors
- [ ] **[P0, M]** Set up environment variables
- [ ] **[P0, S]** Configure Tailwind for accessibility (large text, high contrast)

### 1.10 Frontend Components - Common
- [ ] **[P0, M]** Create Button component (large, accessible)
- [ ] **[P0, M]** Create Icon component (emoji + custom icons)
- [ ] **[P0, M]** Create Modal component
- [ ] **[P0, S]** Create Loading spinner component
- [ ] **[P0, M]** Create Alert/Toast component

### 1.11 Frontend Components - Camera
- [ ] **[P0, L]** Create CameraCapture.vue (access camera, take photo)
- [ ] **[P0, M]** Create ImageViewer.vue (display image)
- [ ] **[P0, M]** Handle camera permissions
- [ ] **[P0, M]** Add image preview before upload
- [ ] **[P0, M]** Implement client-side image compression

### 1.12 Frontend Components - Objects
- [ ] **[P0, L]** Create ObjectSelector.vue (display bounding boxes)
- [ ] **[P0, M]** Create ObjectGrid.vue (browse object library)
- [ ] **[P0, M]** Render clickable bounding boxes over image
- [ ] **[P0, M]** Handle object selection
- [ ] **[P0, M]** Handle overlapping objects (disambiguation)

### 1.13 Frontend Components - Sentence Building
- [ ] **[P0, L]** Create SentenceBuilder.vue (main component)
- [ ] **[P0, L]** Create VerbSelector.vue (display verb options)
- [ ] **[P0, M]** Create ModifierSelector.vue (display modifier options)
- [ ] **[P0, M]** Display real-time sentence preview
- [ ] **[P0, M]** Allow back/undo in sentence building
- [ ] **[P0, M]** Confirmation UI before speaking

### 1.14 Frontend Components - Speech
- [ ] **[P0, L]** Create SpeechOutput.vue with Web Speech API
- [ ] **[P0, M]** Implement speak functionality
- [ ] **[P0, M]** Add play/pause/stop controls
- [ ] **[P0, M]** Visual indicator when speaking
- [ ] **[P0, M]** Handle browser compatibility

### 1.15 Frontend Components - Feedback
- [ ] **[P0, M]** Create FeedbackButtons.vue (thumbs up/down)
- [ ] **[P0, M]** Submit feedback to backend
- [ ] **[P0, M]** Visual confirmation of feedback
- [ ] **[P0, M]** Allow dismissing feedback prompt

### 1.16 Frontend Views
- [ ] **[P0, M]** Create Home.vue (main landing page)
- [ ] **[P0, L]** Create Camera.vue (camera capture flow)
- [ ] **[P0, L]** Create Build.vue (sentence building flow)
- [ ] **[P0, M]** Create Settings.vue (basic user settings)
- [ ] **[P0, M]** Create Login.vue
- [ ] **[P0, M]** Create Register.vue

### 1.17 Frontend State Management
- [ ] **[P0, M]** Create auth store (login, logout, token management)
- [ ] **[P0, L]** Create communication store (objects, verbs, sentence state)
- [ ] **[P0, M]** Create objects store (library, favorites, recents)
- [ ] **[P0, M]** Implement persistent state (localStorage)

### 1.18 Frontend Testing
- [ ] **[P1, L]** Set up Vitest for unit tests
- [ ] **[P1, L]** Write tests for Pinia stores
- [ ] **[P1, L]** Write tests for key components
- [ ] **[P1, M]** Set up Playwright for E2E tests
- [ ] **[P1, L]** Write E2E test for full flow

### 1.19 CI/CD Setup
- [ ] **[P0, L]** Create GitHub Actions workflow for backend CI
- [ ] **[P0, L]** Create GitHub Actions workflow for frontend CI
- [ ] **[P0, M]** Set up linting (flake8, ESLint)
- [ ] **[P0, M]** Set up formatting checks (black, prettier)
- [ ] **[P1, L]** Create deployment workflow for staging
- [ ] **[P1, L]** Create deployment workflow for production

### 1.20 Documentation
- [ ] **[P0, M]** Complete README.md with setup instructions
- [ ] **[P0, M]** Document all API endpoints in OpenAPI/Swagger
- [ ] **[P1, M]** Create user guide for caregivers
- [ ] **[P1, S]** Add inline code comments

### 1.21 MVP Testing & Launch
- [ ] **[P0, XL]** End-to-end testing of complete flow
- [ ] **[P0, L]** Accessibility audit (WCAG compliance)
- [ ] **[P0, M]** Performance testing and optimization
- [ ] **[P0, M]** Security audit
- [ ] **[P0, S]** Fix critical bugs
- [ ] **[P0, M]** Deploy to staging environment
- [ ] **[P0, L]** User testing with target audience
- [ ] **[P0, M]** Incorporate feedback and iterate
- [ ] **[P0, M]** Deploy to production
- [ ] **[P0, S]** Monitor for errors and issues

**Phase 1 Complete**: 93 tasks

---

## Phase 2: Enhanced Intelligence (Weeks 5-8)

**Goal**: Context-aware suggestions, learning from feedback, caregiver dashboard

### 2.1 Context-Aware Suggestions
- [ ] **[P1, L]** Implement time-of-day context (morning, afternoon, evening, night)
- [ ] **[P1, L]** Implement recent usage context (last 5 objects/verbs)
- [ ] **[P1, M]** Adjust verb rankings based on context
- [ ] **[P1, M]** Add location context (if available)

### 2.2 Favorites and Recents
- [ ] **[P1, M]** Create user_favorites table
- [ ] **[P1, M]** API endpoint: POST /api/favorites - Add to favorites
- [ ] **[P1, M]** API endpoint: GET /api/favorites - Get user favorites
- [ ] **[P1, M]** API endpoint: DELETE /api/favorites/{id} - Remove favorite
- [ ] **[P1, M]** Track recently used objects/verbs
- [ ] **[P1, M]** API endpoint: GET /api/recent - Get recent items
- [ ] **[P1, M]** Frontend: Favorites view
- [ ] **[P1, M]** Frontend: Recents view

### 2.3 Learning from Feedback
- [ ] **[P1, L]** Implement frequency-based ranking
- [ ] **[P1, L]** Track success rate per (object, verb, modifier) combination
- [ ] **[P1, M]** Update suggestion scores based on feedback
- [ ] **[P1, M]** Implement decay for old feedback (time-weighted)
- [ ] **[P1, M]** Create learning_state table for Q-values

### 2.4 Caregiver Dashboard - Backend
- [ ] **[P2, M]** Create caregiver_users table
- [ ] **[P2, M]** Implement caregiver authentication
- [ ] **[P2, M]** API endpoint: GET /api/caregiver/analytics - Usage stats
- [ ] **[P2, M]** API endpoint: GET /api/caregiver/phrases - Common phrases
- [ ] **[P2, M]** API endpoint: GET /api/caregiver/timeline - Communication history
- [ ] **[P2, M]** API endpoint: POST /api/caregiver/custom-object - Add custom object
- [ ] **[P2, M]** API endpoint: POST /api/caregiver/export - Export data

### 2.5 Caregiver Dashboard - Frontend
- [ ] **[P2, L]** Create Dashboard.vue component
- [ ] **[P2, M]** Create Analytics.vue (charts, stats)
- [ ] **[P2, M]** Create Timeline.vue (chronological communication log)
- [ ] **[P2, M]** Create CustomObjects.vue (upload photos, label objects)
- [ ] **[P2, M]** Create Export.vue (download CSV/JSON)
- [ ] **[P2, M]** Add charts library (Chart.js or similar)

### 2.6 User Settings
- [ ] **[P2, M]** API endpoint: PUT /api/settings - Update settings
- [ ] **[P2, M]** Frontend: Settings page with preferences
- [ ] **[P2, M]** TTS voice selection
- [ ] **[P2, M]** TTS speech rate adjustment
- [ ] **[P2, M]** High contrast mode toggle
- [ ] **[P2, M]** Icon size adjustment

### 2.7 Modifiers System
- [ ] **[P1, M]** Expand modifier library (please, now, later, more, less, etc.)
- [ ] **[P1, M]** Context-aware modifier suggestions
- [ ] **[P1, M]** Frontend: Enhanced ModifierSelector with categories

### 2.8 Phase 2 Testing
- [ ] **[P1, L]** Test context-aware suggestions
- [ ] **[P1, M]** Test favorites and recents
- [ ] **[P1, L]** Test caregiver dashboard
- [ ] **[P1, M]** End-to-end testing
- [ ] **[P1, M]** Deploy to staging
- [ ] **[P1, M]** User testing
- [ ] **[P1, M]** Deploy to production

**Phase 2 Total**: 35 tasks

---

## Phase 3: Advanced Learning (Weeks 9-12)

**Goal**: Q-learning reinforcement learning, personalization, face recognition

### 3.1 Reinforcement Learning
- [ ] **[P1, XL]** Implement Q-learning algorithm
- [ ] **[P1, L]** Define state representation (object_cat, time, context)
- [ ] **[P1, L]** Define action space (verb_id, modifier_id)
- [ ] **[P1, M]** Implement reward function (+10 thumbs up, +5 spoken, -5 thumbs down)
- [ ] **[P1, L]** Implement Q-value update rule
- [ ] **[P1, M]** Implement ε-greedy exploration (80/20)
- [ ] **[P1, L]** Store Q-values in learning_state table
- [ ] **[P1, M]** Background job to update model periodically

### 3.2 User-Specific Personalization
- [ ] **[P1, L]** Track per-user learning state
- [ ] **[P1, M]** Enable personalization after 50+ interactions
- [ ] **[P1, M]** Blend global model with user model
- [ ] **[P1, M]** API endpoint: GET /api/learning/stats - Get learning progress

### 3.3 Face Recognition
- [ ] **[P2, L]** Create people table for known individuals
- [ ] **[P2, L]** Integrate Azure Face API
- [ ] **[P2, M]** API endpoint: POST /api/people - Add person with photos
- [ ] **[P2, L]** Detect faces in uploaded images
- [ ] **[P2, M]** Match detected faces to known people
- [ ] **[P2, M]** Display person's name instead of generic "person"
- [ ] **[P2, M]** Consent management for face data
- [ ] **[P2, M]** Delete face data on request

### 3.4 Custom Object Library
- [ ] **[P2, M]** Allow uploading custom object photos
- [ ] **[P2, M]** Label custom objects
- [ ] **[P2, M]** Associate custom objects with user
- [ ] **[P2, M]** Display custom objects alongside detected objects
- [ ] **[P2, M]** API endpoint: POST /api/objects/custom - Upload custom object
- [ ] **[P2, M]** API endpoint: DELETE /api/objects/custom/{id} - Delete custom object

### 3.5 Usage Analytics
- [ ] **[P2, M]** Create usage_analytics table
- [ ] **[P2, M]** Track daily usage patterns
- [ ] **[P2, M]** Track most common objects/verbs
- [ ] **[P2, M]** Track session duration
- [ ] **[P2, M]** API endpoint: GET /api/analytics - Get usage analytics
- [ ] **[P2, M]** Frontend: Analytics charts for caregivers

### 3.6 Phase 3 Testing
- [ ] **[P1, XL]** Test Q-learning algorithm effectiveness
- [ ] **[P1, L]** Validate personalization accuracy
- [ ] **[P2, L]** Test face recognition
- [ ] **[P1, M]** End-to-end testing
- [ ] **[P1, M]** Deploy to staging
- [ ] **[P1, M]** User testing
- [ ] **[P1, M]** Deploy to production

**Phase 3 Total**: 28 tasks

---

## Phase 4: Offline & Mobile (Weeks 13-16)

**Goal**: Progressive Web App, offline mode, local object detection, native mobile app

### 4.1 Progressive Web App (PWA)
- [ ] **[P1, L]** Configure service worker with Workbox
- [ ] **[P1, M]** Create manifest.json
- [ ] **[P1, M]** Add app icons (multiple sizes)
- [ ] **[P1, M]** Implement offline-first caching strategy
- [ ] **[P1, M]** Cache API responses
- [ ] **[P1, M]** Queue failed requests for background sync
- [ ] **[P1, M]** Display offline indicator

### 4.2 IndexedDB for Offline Storage
- [ ] **[P1, L]** Set up IndexedDB schema
- [ ] **[P1, M]** Store object library offline
- [ ] **[P1, M]** Store verb library offline
- [ ] **[P1, M]** Store user favorites offline
- [ ] **[P1, M]** Store recent items offline
- [ ] **[P1, M]** Sync with server when online

### 4.3 Local Object Detection (YOLO)
- [ ] **[P1, XL]** Research YOLO v8 for web (TensorFlow.js or ONNX)
- [ ] **[P1, XL]** Train or fine-tune YOLO model for common objects
- [ ] **[P1, L]** Implement client-side YOLO inference
- [ ] **[P1, M]** Fall back to Azure CV for low confidence or unusual objects
- [ ] **[P1, M]** Optimize model size for mobile (< 10MB)
- [ ] **[P1, L]** Test performance on various devices

### 4.4 Native Mobile App (Capacitor)
- [ ] **[P1, L]** Install and configure Capacitor
- [ ] **[P1, M]** Configure iOS project
- [ ] **[P1, M]** Configure Android project
- [ ] **[P1, M]** Use Capacitor Camera plugin
- [ ] **[P1, M]** Use Capacitor Storage plugin
- [ ] **[P1, M]** Test on iOS device
- [ ] **[P1, M]** Test on Android device
- [ ] **[P1, M]** App store preparation (screenshots, descriptions)

### 4.5 Background Sync
- [ ] **[P2, L]** Implement Background Sync API
- [ ] **[P2, M]** Queue offline actions
- [ ] **[P2, M]** Sync when connection restored
- [ ] **[P2, M]** Conflict resolution strategy

### 4.6 Phase 4 Testing
- [ ] **[P1, L]** Test PWA offline functionality
- [ ] **[P1, L]** Test local YOLO accuracy and performance
- [ ] **[P1, L]** Test mobile apps on multiple devices
- [ ] **[P1, M]** End-to-end testing
- [ ] **[P1, M]** Deploy to staging
- [ ] **[P1, M]** User testing
- [ ] **[P1, M]** Deploy to production
- [ ] **[P1, L]** Submit to app stores (iOS, Android)

**Phase 4 Total**: 22 tasks

---

## Phase 5: Extended Features (Weeks 17-20)

**Goal**: Pre-made phrases, emotion selection, routines, multi-language

### 5.1 Pre-made Common Phrases
- [ ] **[P2, M]** Create phrases table
- [ ] **[P2, M]** Seed common phrases ("I'm hungry", "I need bathroom", etc.)
- [ ] **[P2, M]** API endpoint: GET /api/phrases - Get phrase library
- [ ] **[P2, M]** Frontend: Quick phrases on home screen
- [ ] **[P2, M]** Allow custom phrases

### 5.2 Emotion Selection
- [ ] **[P2, M]** Create emotions library (happy, sad, angry, tired, etc.)
- [ ] **[P2, M]** API endpoint: GET /api/emotions - Get emotions
- [ ] **[P2, M]** Frontend: Emotion selector component
- [ ] **[P2, M]** Sentence templates for emotions ("I feel [emotion]")

### 5.3 Schedule and Routine Builder
- [ ] **[P2, L]** Create routines table
- [ ] **[P2, M]** API endpoint: POST /api/routines - Create routine
- [ ] **[P2, M]** API endpoint: GET /api/routines - Get user routines
- [ ] **[P2, M]** Frontend: Routine builder UI
- [ ] **[P2, M]** Schedule-based suggestions (breakfast time → food phrases)

### 5.4 Multi-Language Support
- [ ] **[P3, L]** Set up i18n (vue-i18n)
- [ ] **[P3, L]** Translate UI to Spanish
- [ ] **[P3, L]** Translate object/verb libraries to Spanish
- [ ] **[P3, M]** TTS support for multiple languages
- [ ] **[P3, M]** Language selector in settings

### 5.5 Export and Reporting
- [ ] **[P2, M]** API endpoint: GET /api/export/csv - Export as CSV
- [ ] **[P2, M]** API endpoint: GET /api/export/json - Export as JSON
- [ ] **[P2, M]** API endpoint: GET /api/export/pdf - Generate PDF report
- [ ] **[P2, M]** Frontend: Export button in caregiver dashboard

### 5.6 Phase 5 Testing
- [ ] **[P2, L]** Test all new features
- [ ] **[P2, M]** End-to-end testing
- [ ] **[P2, M]** Deploy to staging
- [ ] **[P2, M]** User testing
- [ ] **[P2, M]** Deploy to production

**Phase 5 Total**: 18 tasks

---

## Summary

| Phase | Weeks | Tasks | Goal |
|-------|-------|-------|------|
| Phase 1 | 1-4 | 93 | MVP: Camera, object detection, sentence building, TTS |
| Phase 2 | 5-8 | 35 | Enhanced intelligence, caregiver dashboard |
| Phase 3 | 9-12 | 28 | Advanced RL, personalization, face recognition |
| Phase 4 | 13-16 | 22 | Offline mode, PWA, local YOLO, mobile apps |
| Phase 5 | 17-20 | 18 | Extended features (emotions, routines, multi-language) |
| **Total** | **20** | **196** | **Full-featured AAC communication app** |

---

## Definition of Done

A task is considered "Done" when:
- [ ] Code implemented and follows style guide
- [ ] Unit tests written and passing
- [ ] Integration tests passing (if applicable)
- [ ] Code reviewed and approved
- [ ] Documentation updated
- [ ] No critical bugs
- [ ] Accessibility checked (WCAG AAA)
- [ ] Performance acceptable
- [ ] Merged to develop branch

---

## Priority Definitions

- **P0 (Critical)**: Must have for MVP or phase completion. Blocker if not done.
- **P1 (High)**: Important for user experience and core functionality.
- **P2 (Medium)**: Enhances experience but not critical.
- **P3 (Low)**: Nice to have, can be deferred.

---

## Tracking Progress

- Use GitHub Projects board with columns: Backlog, To Do, In Progress, In Review, Done
- Link tasks to issues and pull requests
- Update this document as tasks are completed
- Hold weekly sprint planning and retrospectives

---

**Last Updated**: 2025-10-31
