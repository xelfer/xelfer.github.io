# SubTrack - Product Roadmap

## Phase 1: PWA & App Store Validation
- [ ] Add service worker for true offline support
- [ ] Add web app manifest for "Add to Home Screen"
- [ ] Wrap in Capacitor or Expo web view for iOS + Android app store submission
- [ ] Screen wake lock during active game (prevent phone sleeping on sideline)
- [ ] Haptic feedback on sub alerts (native, not just Vibration API)
- [ ] Test with real teams, gather feedback

## Phase 2: Backend & Sync
- [ ] Set up AWS infrastructure (CDK/Terraform)
  - [ ] RDS PostgreSQL (t4g.micro to start)
  - [ ] ECS Fargate or Lambda for API
  - [ ] S3 + CloudFront for web app
  - [ ] Route53 for custom domain (subtrakt.app or similar)
  - [ ] GitHub Actions CI/CD pipeline
- [ ] Auth: Cognito or Auth0 (invite-based team access)
- [ ] API: Node.js or Python FastAPI
- [ ] Data model migration from localStorage to PostgreSQL
  ```
  organizations (clubs)
    └── teams
          ├── seasons
          ├── players (jersey numbers, positions, photo)
          ├── games
          │     ├── game_events (sub_on, sub_off, injury, goal, card)
          │     ├── game_players (per-player stats per game)
          │     └── game_halves (actual duration, stoppage)
          └── formations (saved presets per team)
  ```
- [ ] Event-sourced game state: every action is an immutable event with timestamp
  - Enables: full replay, undo, analytics
- [ ] Offline-first sync: queue actions locally, sync when online
- [ ] Team sharing: multiple coaches/parents can view via invite link

## Phase 3: Native Features & Analytics
- [ ] Apple Watch / Wear OS companion app
  - Haptic tap on wrist for sub alerts (killer feature)
  - Quick confirm/snooze from watch
- [ ] Push notifications
  - Coach: sub reminders even if app backgrounded
  - Parents: "Your child just subbed on"
- [ ] Season fairness dashboard
  - Cumulative playing time across all games in a season
  - Fairness score / visualizations
  - Smart sub suggestions based on season-long data, not just current game
- [ ] Real-time game view via WebSocket (API Gateway)
  - Parents can watch subs happening live from home
  - Share link, read-only
- [ ] Post-game summary auto-shared to team group chat (Slack, WhatsApp, etc.)

## Phase 4: League & Monetization
- [ ] League/club admin panel
  - Multi-team management
  - League compliance (minimum playing time rules)
  - Export reports for league requirements
- [ ] Paid tier for clubs/leagues
  - Free: single team, basic features
  - Pro: multi-team, season analytics, watch app, live sharing
- [ ] Pre-game lineup builder with drag-and-drop
- [ ] Goal/card/assist tracking during games
- [ ] Player availability management (RSVPs for upcoming games)

## Technical Notes
- Offline-first is critical: games happen on fields with bad signal
- Zero-friction start: works in 30 seconds with no account (like current POC), account optional for sync/history
- Event sourcing gives free replay, undo, and analytics
- Early stage cost estimate: ~$50/month on AWS (RDS t4g.micro, Fargate spot, S3+CloudFront)
- Current POC costs $0 on GitHub Pages
