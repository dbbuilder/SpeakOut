# AAC Communication App - Requirements Specification

## Document Information
- **Version**: 1.0
- **Last Updated**: 2025-10-31
- **Status**: Draft
- **Author**: Project Team

## 1. Functional Requirements

### FR-1: Image Capture and Upload
**Priority**: P0 (Critical)
**Phase**: 1

#### Description
Users must be able to capture images using their device camera or select from gallery.

#### Acceptance Criteria
- [ ] User can access device camera from app
- [ ] User can capture photo with single tap
- [ ] User can review captured image before submission
- [ ] User can retake photo if needed
- [ ] Image is uploaded to Azure Blob Storage
- [ ] Upload progress is displayed
- [ ] Error handling for camera permission denied
- [ ] Error handling for upload failures
- [ ] Supports JPEG, PNG formats
- [ ] Images optimized to max 800px dimension before upload

#### Technical Notes
- Use Navigator.mediaDevices API for web
- Use Capacitor Camera plugin for mobile
- Compress images client-side to reduce costs
- Store temporarily (24-hour auto-delete)

---

### FR-2: Object Detection
**Priority**: P0 (Critical)
**Phase**: 1

#### Description
System must detect and label objects in uploaded images with bounding boxes.

#### Acceptance Criteria
- [ ] Image sent to Azure Computer Vision API
- [ ] Objects returned with bounding boxes (x, y, width, height)
- [ ] Minimum confidence threshold of 0.6
- [ ] Common objects identified (food, people, furniture, etc.)
- [ ] Results displayed within 3 seconds
- [ ] Bounding boxes overlaid on image
- [ ] Labels displayed for each object
- [ ] User can tap on bounding box to select object
- [ ] Error handling for API failures
- [ ] Fallback to cached results if available

#### Technical Notes
- Azure Computer Vision Analyze API v3.2
- Free tier: 5,000 images/month
- Return top 10 objects per image
- Cache results for 24 hours

---

### FR-3: Object Selection
**Priority**: P0 (Critical)
**Phase**: 1

#### Description
Users must be able to select detected objects by tapping on them.

#### Acceptance Criteria
- [ ] Touch targets minimum 60px × 60px
- [ ] Visual feedback when tapping (highlight bounding box)
- [ ] Handle overlapping objects (show disambiguation menu)
- [ ] Selected object highlighted clearly
- [ ] Object name displayed prominently
- [ ] Ability to go back and select different object
- [ ] Works with touch, mouse, and keyboard
- [ ] Accessible via screen readers

---

### FR-4: Verb Suggestion
**Priority**: P0 (Critical)
**Phase**: 1

#### Description
System suggests contextually appropriate verbs based on selected object.

#### Acceptance Criteria
- [ ] Display 3-5 most relevant verbs
- [ ] Verbs have emoji icons
- [ ] Rule-based suggestions by object category
- [ ] Food/Drink → want, need, eat, drink
- [ ] Person → see, talk to, call, hug
- [ ] Place → go, go to, leave
- [ ] Thing → get, give, show, play with
- [ ] Always include common verbs (want, need, like)
- [ ] Verbs ordered by relevance score
- [ ] Touch targets minimum 60px × 60px
- [ ] Clear visual distinction between verbs

---

### FR-5: Sentence Construction
**Priority**: P0 (Critical)
**Phase**: 1

#### Description
System constructs grammatically correct sentences from selected elements.

#### Acceptance Criteria
- [ ] Support template: "I [verb] [object]"
- [ ] Support template: "[Object] please"
- [ ] Support template: "I [verb] [modifier]"
- [ ] Real-time sentence preview as building
- [ ] Grammatical correctness (articles, capitalization)
- [ ] Ability to edit/rebuild sentence
- [ ] Clear visual representation of sentence structure
- [ ] Confirmation before speaking

---

### FR-6: Text-to-Speech Output
**Priority**: P0 (Critical)
**Phase**: 1

#### Description
System speaks constructed sentences aloud using natural voice.

#### Acceptance Criteria
- [ ] Use Web Speech API
- [ ] Default to device's native TTS engine
- [ ] Natural sounding voice
- [ ] Adjustable speech rate (Phase 2)
- [ ] Adjustable pitch (Phase 2)
- [ ] Voice selection (Phase 2)
- [ ] Play/Pause/Stop controls
- [ ] Visual indicator when speaking
- [ ] Works offline (uses device TTS)

---

### FR-7: Feedback Collection
**Priority**: P0 (Critical)
**Phase**: 1

#### Description
System collects user feedback on constructed sentences for learning.

#### Acceptance Criteria
- [ ] Thumbs up/down buttons after sentence spoken
- [ ] Optional feedback (can be dismissed)
- [ ] Feedback stored with sentence context
- [ ] No interruption to communication flow
- [ ] Clear visual feedback when submitted
- [ ] Ability to change feedback

---

### FR-8: Object Library
**Priority**: P1 (High)
**Phase**: 2

#### Description
Users can browse and select objects from pre-loaded library.

#### Acceptance Criteria
- [ ] Grid view of common objects
- [ ] Categories: Food, People, Places, Things, Actions, Feelings
- [ ] Search/filter by category
- [ ] Generic icons for each object
- [ ] Favorites section
- [ ] Recently used section
- [ ] Quick access from home screen
- [ ] 100+ common objects pre-loaded

---

### FR-9: Adaptive Learning
**Priority**: P1 (High)
**Phase**: 2-3

#### Description
System learns from user feedback to personalize suggestions.

#### Acceptance Criteria
- [ ] Track: object + verb + modifier + outcome
- [ ] Update suggestion rankings based on feedback
- [ ] Positive feedback → increase rank
- [ ] Negative feedback → decrease rank
- [ ] Context-aware (time of day, recent usage)
- [ ] User-specific personalization after 50+ interactions
- [ ] Exploration vs exploitation (80/20 split)
- [ ] Transparent to user (no configuration needed)

---

### FR-10: Caregiver Dashboard
**Priority**: P2 (Medium)
**Phase**: 2

#### Description
Caregivers can view communication patterns and customize settings.

#### Acceptance Criteria
- [ ] Login as caregiver role
- [ ] View usage analytics
- [ ] See most common phrases
- [ ] View communication timeline
- [ ] Add custom objects (upload photos)
- [ ] Add custom people (family photos)
- [ ] Manage favorites
- [ ] Export communication logs
- [ ] Configure settings for user

---

## 2. Non-Functional Requirements

### NFR-1: Performance
- Page load time < 2 seconds
- Object detection < 3 seconds (cloud), < 1 second (local)
- Sentence construction < 500ms
- TTS start < 500ms
- Support 1000+ concurrent users
- Handle 100,000+ images/month

### NFR-2: Accessibility
- WCAG AAA compliance target
- Minimum touch targets 60px × 60px
- WCAG AAA contrast ratios (7:1)
- Screen reader compatible
- Keyboard navigation support
- No time-based interactions
- High contrast mode option
- Adjustable text/icon sizes
- Works without color perception
- Clear focus indicators

### NFR-3: Reliability
- 99.9% uptime (excluding maintenance)
- Graceful degradation if APIs unavailable
- Offline mode for core features (Phase 4)
- Auto-save state on connection loss
- Data persistence across sessions
- Automatic error recovery

### NFR-4: Security
- HTTPS/TLS 1.3 required
- Secrets in Azure Key Vault
- JWT authentication with refresh tokens
- Password hashing (bcrypt)
- Rate limiting (100 req/min per user)
- Input validation and sanitization
- SQL injection prevention
- XSS prevention
- CSRF protection
- Images auto-deleted after 24 hours
- COPPA compliant
- GDPR compliant data handling

### NFR-5: Privacy
- Minimal data collection
- No facial recognition without consent
- Images temporary only
- User data export capability
- User data deletion capability
- Clear privacy policy
- No third-party analytics without consent
- Encryption at rest
- Encryption in transit

### NFR-6: Usability
- Intuitive interface for non-verbal users
- Minimal cognitive load (3-5 options per screen)
- Large, clear icons and text
- Consistent UI patterns
- No required text input
- One-handed operation capable
- Works on tablets and phones
- 5-minute learning curve for caregivers

### NFR-7: Maintainability
- Modular architecture
- Code coverage > 80%
- Comprehensive API documentation
- Inline code comments
- Standardized code style
- Version control (Git)
- Automated testing
- CI/CD pipeline

### NFR-8: Scalability
- Horizontal scaling capability
- Database query optimization
- API response caching
- CDN for static assets
- Load balancing ready
- Support 10x growth without architecture changes

---

## 3. Technical Requirements

### TR-1: Frontend Technology
- Vue 3 with Composition API
- Vite build tool
- Tailwind CSS for styling
- Pinia for state management
- Vue Router for navigation
- Axios for HTTP requests
- Web Speech API for TTS
- Progressive Web App (PWA) ready

### TR-2: Backend Technology
- Python 3.11+
- FastAPI framework
- SQLAlchemy 2.0 ORM
- Alembic migrations
- Pydantic v2 validation
- pytest for testing
- JWT authentication
- Async/await patterns

### TR-3: Database
- PostgreSQL 14+
- Proper indexing for performance
- Foreign key constraints
- Database migrations (Alembic)
- Connection pooling
- Backup strategy

### TR-4: Azure Services
- Computer Vision API (F0 free tier)
- App Service (Linux, B1 tier)
- Database for PostgreSQL (Flexible Server, B1ms)
- Blob Storage (Standard LRS)
- Key Vault (Standard tier)
- Application Insights

### TR-5: API Design
- RESTful architecture
- JSON request/response
- Versioned endpoints (/api/v1/)
- OpenAPI/Swagger documentation
- Standardized error responses
- Pagination for list endpoints
- Rate limiting
- CORS configuration

---

## 4. Constraints

### C-1: Budget Constraints
- Target MVP cost: ~$26/month
- Must use Azure free tiers where possible
- Local object detection required by Phase 4 to reduce costs

### C-2: Technical Constraints
- Must work on devices 3+ years old
- Must support iOS Safari and Chrome
- Minimum browser: Chrome 90+, Safari 14+
- Internet required for MVP (offline in Phase 4)

### C-3: Time Constraints
- MVP delivery: 4 weeks
- Full Phase 1-5: 20 weeks

### C-4: Regulatory Constraints
- COPPA compliance (users may be under 13)
- GDPR compliance (European users)
- Healthcare data handling (PHI) if used in clinical settings

---

## 5. Success Criteria

### User Experience Metrics
- [ ] 95% object detection accuracy
- [ ] Average sentence construction time < 30 seconds
- [ ] 80% user satisfaction rating
- [ ] 30% improvement in suggestion accuracy after 100 uses
- [ ] 50% reduction in steps for common phrases after 1 week

### Technical Metrics
- [ ] 99.9% uptime
- [ ] < 2 second page load
- [ ] < 3 second object detection
- [ ] 80%+ test coverage
- [ ] Zero critical security vulnerabilities

### Business Metrics
- [ ] 10+ active users by end of Phase 1
- [ ] 100+ active users by end of Phase 5
- [ ] Positive caregiver feedback
- [ ] Evidence of improved communication outcomes

---

## 6. Assumptions

### A-1: User Assumptions
- Users have access to tablet or smartphone with camera
- Users can tap/touch screen
- Caregivers available for initial setup
- Users understand basic icon representations

### A-2: Technical Assumptions
- Internet connectivity available (until Phase 4)
- Azure services remain available and affordable
- Computer Vision API accuracy sufficient (90%+)
- Web Speech API works on target devices

### A-3: Environmental Assumptions
- Adequate lighting for photos
- Objects within camera view
- Relatively uncluttered environments

---

## 7. Dependencies

### D-1: External Services
- Azure Computer Vision API
- Azure infrastructure services
- Web Speech API (browser)

### D-2: Third-Party Libraries
- Vue 3 ecosystem
- FastAPI ecosystem
- SQLAlchemy
- Various npm/pip packages

### D-3: Human Resources
- Development team
- AAC specialist consultation (recommended)
- User testing with target audience

---

## 8. Risks and Mitigation

### Risk 1: Poor Object Detection Accuracy
**Likelihood**: Medium
**Impact**: High
**Mitigation**:
- Use high confidence threshold (0.6+)
- Allow manual object selection from library
- Add feedback mechanism to improve over time
- Consider local YOLO model for common objects

### Risk 2: Azure Costs Exceed Budget
**Likelihood**: Medium
**Impact**: Medium
**Mitigation**:
- Implement image compression
- Add local object detection by Phase 4
- Monitor usage closely
- Set up billing alerts

### Risk 3: User Adoption Challenges
**Likelihood**: Medium
**Impact**: High
**Mitigation**:
- Extensive user testing with target audience
- Involve caregivers early
- Simple, intuitive UI design
- Comprehensive onboarding
- AAC specialist consultation

### Risk 4: TTS Browser Compatibility
**Likelihood**: Low
**Impact**: Medium
**Mitigation**:
- Test across all target browsers
- Provide polyfills
- Consider server-side TTS as fallback

### Risk 5: Privacy/Security Breach
**Likelihood**: Low
**Impact**: Very High
**Mitigation**:
- Security-first design
- Regular security audits
- Penetration testing
- Bug bounty program (later)
- Comprehensive logging and monitoring

---

## 9. Out of Scope (For MVP)

- Multi-language support
- Real-time translation
- Video-based communication
- Integration with external AAC devices
- Advanced AI (GPT-4, etc.)
- Social features
- Commercial licensing
- Clinical trial integration

---

## 10. Future Considerations

See [FUTURE.md](FUTURE.md) for long-term vision and potential features.

---

## Appendix A: Glossary

- **AAC**: Augmentative and Alternative Communication
- **TTS**: Text-to-Speech
- **RL**: Reinforcement Learning
- **PWA**: Progressive Web App
- **WCAG**: Web Content Accessibility Guidelines
- **COPPA**: Children's Online Privacy Protection Act
- **GDPR**: General Data Protection Regulation
- **JWT**: JSON Web Token

---

## Appendix B: References

- AAC Best Practices: [Link]
- WCAG AAA Guidelines: https://www.w3.org/WAI/WCAG2AAA-Conformance
- Azure Computer Vision API: https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/
- Web Speech API: https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API

---

**Document Status**: Living document, updated as requirements evolve
