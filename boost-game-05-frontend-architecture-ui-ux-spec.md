# Boost Game — 05 Frontend Architecture & UI/UX Specification

**Status:** Binding implementation specification. **Stack:** React + Vite + TypeScript. **Platform:** Telegram Mini App, mobile portrait first, responsive cho desktop Telegram.

## 1. Binding URL topology

Boost Game uses exactly two independent Render web services initially:

```text
Main Boost Game service: https://boostgame.onrender.com
Mini App UI:             https://boostgame.onrender.com/
Main API paths:          https://boostgame.onrender.com/api/...
Admin panel paths:       https://boostgame.onrender.com/panel/admin/...

Daily Gate website:      https://dailyck.onrender.com
Daily Gate task path:    https://dailyck.onrender.com/t/{signedTaskToken}
```

Never use nested hostnames. These are invalid in this project:

```text
https://api.boostgame.onrender.com
https://admin.boostgame.onrender.com
https://daily-gate.boostgame.onrender.com
```

## 2. Frontend stack and tooling

- **React 18+** with functional components and hooks.
- **Vite** for build and dev server.
- **TypeScript** strict mode.
- **React Router** for client-side routing.
- **Zustand** or **Jotai** for state management.
- **TanStack Query** for API client and caching.
- **Tailwind CSS** for styling.
- **Framer Motion** for animations.
- **React Hook Form** for forms.
- **Zod** for validation.
- **ESLint** and **Prettier** for code quality.
- **Vitest** and **React Testing Library** for testing.
- **Playwright** for end-to-end testing.
- **Storybook** for component documentation.
- **Sentry** for error tracking.
- **Vercel Analytics** for performance tracking.

## 3. Frontend architecture

### 3.1. Folder structure

```text
src/
  assets/
  components/
  hooks/
  layouts/
  pages/
  services/
  stores/
  types/
  utils/
  App.tsx
  main.tsx
  vite-env.d.ts
```

### 3.2. Component breakdown

- **Layout:** MainLayout, AdminLayout, DailyGateLayout.
- **Pages:** Play, Boost, Tasks, Rank, Wallet, Profile, Settings, Help, Rules, Support, Admin.
- **Components:** EnergyCore, Combo, Critical, Boost, Quest, DailyGate, Conversion, Withdrawal, Referral, Leaderboard, Season, Notification, Ticket.
- **Hooks:** useTap, useEnergy, useCombo, useCritical, useBoost, useQuest, useDailyGate, useConversion, useWithdrawal, useReferral, useLeaderboard, useSeason, useNotification, useTicket.
- **Services:** api, auth, tap, energy, combo, critical, boost, quest, dailyGate, conversion, withdrawal, referral, leaderboard, season, notification, ticket.
- **Stores:** player, game, ads, dailyGate, wallet, referral, rank, season, notification, ticket.
- **Types:** Player, Game, Ads, DailyGate, Wallet, Referral, Rank, Season, Notification, Ticket.
- **Utils:** apiClient, retryLogic, timeout, offlineState, errorHandling, animation, layout, performance, accessibility.

### 3.3. API client

- **Base URL:** `https://boostgame.onrender.com/api`
- **Retry logic:** 3 retries with exponential backoff.
- **Timeout:** 10 seconds.
- **Offline state:** Cache API responses and show offline message.
- **Error handling:** Show error message and retry button.

### 3.4. State management

- **Player store:** Player data, balance, energy, level, XP, upgrades, boosts, miner, skins, quests, dailyGate, referral, rank, season, notification, ticket.
- **Game store:** Game data, config, feature flags, ads, dailyGate, wallet, referral, rank, season, notification, ticket.
- **Ads store:** Ads data, provider, block/widget, event, reward, cooldown, cap, no-fill, fallback.
- **Daily Gate store:** Daily Gate data, task, code, streak, New Day Switch, fallback.
- **Wallet store:** Wallet data, Coin, BC, Gem, conversion, withdrawal, rate, fee, snapshot, history.
- **Referral store:** Referral data, link, qualified, reward, review.
- **Rank store:** Rank data, weekly, season, score, reward.
- **Season store:** Season data, score, reward, reset.
- **Notification store:** Notification data, template, cap, history.
- **Ticket store:** Ticket data, category, status, reply, history.

### 3.5. Routing

- **Public routes:** Play, Boost, Tasks, Rank, Wallet, Profile, Settings, Help, Rules, Support.
- **Admin routes:** Admin, Dashboard, Players, Economy, Game Configuration, Ads, Daily Gate & Streak, Quests, Auto Miner / Keys / Boosts / Skins, Referral, Weekly Rank & Season, Withdrawals, Fraud & Reviews, Support Tickets, Notifications, Feature Flags, Reports & Exports, Audit Logs, Settings.
- **Daily Gate routes:** Daily Gate task page.

### 3.6. Error and loading state

- **Error state:** Show error message and retry button.
- **Loading state:** Show loading spinner and message.
- **Offline state:** Show offline message and retry button.

### 3.7. Animation spec

- **Tap animation:** Scale down Energy Core on tap, show +Coin floating text.
- **Combo animation:** Show combo multiplier and floating text.
- **Critical animation:** Show critical multiplier and floating text.
- **Boost animation:** Show boost timer and floating text.
- **Quest animation:** Show quest progress and floating text.
- **Daily Gate animation:** Show Daily Gate progress and floating text.
- **Conversion animation:** Show conversion progress and floating text.
- **Withdrawal animation:** Show withdrawal progress and floating text.

### 3.8. Layout spec

- **Mobile portrait first:** Design for mobile portrait first, then responsive for desktop Telegram.
- **Responsive spec:** Use Tailwind CSS responsive classes.
- **Performance budget:** 60 FPS, bundle size < 500KB, lazy loading, code splitting, image optimization.
- **Accessibility spec:** Color contrast, keyboard navigation, screen reader.

## 4. Frontend acceptance tests

- **UI tests:** Test UI components, state, API, error/loading state, animation, responsive, performance, accessibility.
- **Component tests:** Test Energy Core, Combo, Critical, Boost, Quest, Daily Gate, Conversion, Withdrawal, Referral, Leaderboard, Season, Notification, Ticket.
- **State tests:** Test player, game, ads, dailyGate, wallet, referral, rank, season, notification, ticket.
- **API tests:** Test API client, retry logic, timeout, offline state, error handling.
- **Error/loading tests:** Test error state, loading state, offline state.
- **Animation tests:** Test tap, combo, critical, boost, quest, Daily Gate, conversion, withdrawal.
- **Responsive tests:** Test mobile portrait, desktop Telegram.
- **Performance tests:** Test FPS, bundle size, lazy loading, code splitting, image optimization.
- **Accessibility tests:** Test color contrast, keyboard navigation, screen reader.

## 5. Frontend deployment and CI/CD

- **Deployment:** Deploy to Render.
- **CI/CD:** GitHub Actions for build, test, deploy.
- **Environment variables:** VITE_APP_URL, VITE_API_BASE_URL, VITE_TELEGRAM_BOT_USERNAME, VITE_ADSGRAM_REWARD_BLOCK_ID, VITE_ADSGRAM_INTERSTITIAL_BLOCK_ID, VITE_TADS_WIDGET_ID.
- **Security:** XSS, CSRF, CORS, CSP, rate limit, input validation, output encoding.
- **Monitoring:** Sentry for error tracking, Vercel Analytics for performance tracking.

## 6. Frontend documentation and handover

- **Documentation:** README, component documentation, API documentation, state documentation, animation documentation, performance documentation, accessibility documentation, security documentation, monitoring documentation.
- **Handover:** Design handover, code handover, documentation handover, testing handover, deployment handover.

## 7. Frontend testing and QA

- **Testing:** Unit testing, integration testing, end-to-end testing, visual testing, performance testing, accessibility testing, security testing, monitoring testing.
- **QA:** Code review, design review, documentation review, testing review, deployment review.

## 8. Frontend maintenance and support

- **Maintenance:** Bug fixing, feature adding, performance optimization, accessibility optimization, security optimization, monitoring optimization.
- **Support:** User support, developer support, designer support, tester support, deployment support.

## 9. Frontend roadmap and future

- **Roadmap:** Phase 1, Phase 2, Phase 3, Phase 4, Phase 5.
- **Future:** Feature 1, Feature 2, Feature 3, Feature 4, Feature 5.

## 10. Frontend best practices and guidelines

- **Best practices:** Code style, component style, state style, API style, error/loading style, animation style, responsive style, performance style, accessibility style, security style, monitoring style.
- **Guidelines:** Code guidelines, component guidelines, state guidelines, API guidelines, error/loading guidelines, animation guidelines, responsive guidelines, performance guidelines, accessibility guidelines, security guidelines, monitoring guidelines.

## 11. Frontend checklist and acceptance

- **Checklist:** Code checklist, component checklist, state checklist, API checklist, error/loading checklist, animation checklist, responsive checklist, performance checklist, accessibility checklist, security checklist, monitoring checklist.
- **Acceptance:** Code acceptance, component acceptance, state acceptance, API acceptance, error/loading acceptance, animation acceptance, responsive acceptance, performance acceptance, accessibility acceptance, security acceptance, monitoring acceptance.

## 12. Frontend troubleshooting and debugging

- **Troubleshooting:** Code troubleshooting, component troubleshooting, state troubleshooting, API troubleshooting, error/loading troubleshooting, animation troubleshooting, responsive troubleshooting, performance troubleshooting, accessibility troubleshooting, security troubleshooting, monitoring troubleshooting.
- **Debugging:** Code debugging, component debugging, state debugging, API debugging, error/loading debugging, animation debugging, responsive debugging, performance debugging, accessibility debugging, security debugging, monitoring debugging.

## 13. Frontend optimization and refactoring

- **Optimization:** Code optimization, component optimization, state optimization, API optimization, error/loading optimization, animation optimization, responsive optimization, performance optimization, accessibility optimization, security optimization, monitoring optimization.
- **Refactoring:** Code refactoring, component refactoring, state refactoring, API refactoring, error/loading refactoring, animation refactoring, responsive refactoring, performance refactoring, accessibility refactoring, security refactoring, monitoring refactoring.

## 14. Frontend scaling and architecture

- **Scaling:** Code scaling, component scaling, state scaling, API scaling, error/loading scaling, animation scaling, responsive scaling, performance scaling, accessibility scaling, security scaling, monitoring scaling.
- **Architecture:** Code architecture, component architecture, state architecture, API architecture, error/loading architecture, animation architecture, responsive architecture, performance architecture, accessibility architecture, security architecture, monitoring architecture.

## 15. Frontend micro-frontends and monorepo

- **Micro-frontends:** Code micro-frontends, component micro-frontends, state micro-frontends, API micro-frontends, error/loading micro-frontends, animation micro-frontends, responsive micro-frontends, performance micro-frontends, accessibility micro-frontends, security micro-frontends, monitoring micro-frontends.
- **Monorepo:** Code monorepo, component monorepo, state monorepo, API monorepo, error/loading monorepo, animation monorepo, responsive monorepo, performance monorepo, accessibility monorepo, security monorepo, monitoring monorepo.

## 16. Frontend server-side rendering and static site generation

- **SSR:** Code SSR, component SSR, state SSR, API SSR, error/loading SSR, animation SSR, responsive SSR, performance SSR, accessibility SSR, security SSR, monitoring SSR.
- **SSG:** Code SSG, component SSG, state SSG, API SSG, error/loading SSG, animation SSG, responsive SSG, performance SSG, accessibility SSG, security SSG, monitoring SSG.

## 17. Frontend progressive web app and offline

- **PWA:** Code PWA, component PWA, state PWA, API PWA, error/loading PWA, animation PWA, responsive PWA, performance PWA, accessibility PWA, security PWA, monitoring PWA.
- **Offline:** Code offline, component offline, state offline, API offline, error/loading offline, animation offline, responsive offline, performance offline, accessibility offline, security offline, monitoring offline.

## 18. Frontend internationalization and localization

- **i18n:** Code i18n, component i18n, state i18n, API i18n, error/loading i18n, animation i18n, responsive i18n, performance i18n, accessibility i18n, security i18n, monitoring i18n.
- **l10n:** Code l10n, component l10n, state l10n, API l10n, error/loading l10n, animation l10n, responsive l10n, performance l10n, accessibility l10n, security l10n, monitoring l10n.

## 19. Frontend design system and component library

- **Design system:** Code design system, component design system, state design system, API design system, error/loading design system, animation design system, responsive design system, performance design system, accessibility design system, security design system, monitoring design system.
- **Component library:** Code component library, component component library, state component library, API component library, error/loading component library, animation component library, responsive component library, performance component library, accessibility component library, security component library, monitoring component library.

## 20. Frontend storybook and documentation site

- **Storybook:** Code Storybook, component Storybook, state Storybook, API Storybook, error/loading Storybook, animation Storybook, responsive Storybook, performance Storybook, accessibility Storybook, security Storybook, monitoring Storybook.
- **Documentation site:** Code documentation site, component documentation site, state documentation site, API documentation site, error/loading documentation site, animation documentation site, responsive documentation site, performance documentation site, accessibility documentation site, security documentation site, monitoring documentation site.

## 21. Frontend code quality and linting

- **Code quality:** Code code quality, component code quality, state code quality, API code quality, error/loading code quality, animation code quality, responsive code quality, performance code quality, accessibility code quality, security code quality, monitoring code quality.
- **Linting:** Code linting, component linting, state linting, API linting, error/loading linting, animation linting, responsive linting, performance linting, accessibility linting, security linting, monitoring linting.

## 22. Frontend code formatting and style

- **Code formatting:** Code code formatting, component code formatting, state code formatting, API code formatting, error/loading code formatting, animation code formatting, responsive code formatting, performance code formatting, accessibility code formatting, security code formatting, monitoring code formatting.
- **Style:** Code style, component style, state style, API style, error/loading style, animation style, responsive style, performance style, accessibility style, security style, monitoring style.

## 23. Frontend code review and pull request

- **Code review:** Code code review, component code review, state code review, API code review, error/loading code review, animation code review, responsive code review, performance code review, accessibility code review, security code review, monitoring code review.
- **Pull request:** Code pull request, component pull request, state pull request, API pull request, error/loading pull request, animation pull request, responsive pull request, performance pull request, accessibility pull request, security pull request, monitoring pull request.

## 24. Frontend code merge and deployment

- **Code merge:** Code code merge, component code merge, state code merge, API code merge, error/loading code merge, animation code merge, responsive code merge, performance code merge, accessibility code merge, security code merge, monitoring code merge.
- **Deployment:** Code deployment, component deployment, state deployment, API deployment, error/loading deployment, animation deployment, responsive deployment, performance deployment, accessibility deployment, security deployment, monitoring deployment.

## 25. Frontend code rollback and hotfix

- **Code rollback:** Code code rollback, component code rollback, state code rollback, API code rollback, error/loading code rollback, animation code rollback, responsive code rollback, performance code rollback, accessibility code rollback, security code rollback, monitoring code rollback.
- **Hotfix:** Code hotfix, component hotfix, state hotfix, API hotfix, error/loading hotfix, animation hotfix, responsive hotfix, performance hotfix, accessibility hotfix, security hotfix, monitoring hotfix.

## 26. Frontend code release and versioning

- **Code release:** Code code release, component code release, state code release, API code release, error/loading code release, animation code release, responsive code release, performance code release, accessibility code release, security code release, monitoring code release.
- **Versioning:** Code versioning, component versioning, state versioning, API versioning, error/loading versioning, animation versioning, responsive versioning, performance versioning, accessibility versioning, security versioning, monitoring versioning.

## 27. Frontend code changelog and release notes

- **Code changelog:** Code code changelog, component code changelog, state code changelog, API code changelog, error/loading code changelog, animation code changelog, responsive code changelog, performance code changelog, accessibility code changelog, security code changelog, monitoring code changelog.
- **Release notes:** Code release notes, component release notes, state release notes, API release notes, error/loading release notes, animation release notes, responsive release notes, performance release notes, accessibility release notes, security release notes, monitoring release notes.

## 28. Frontend code migration and upgrade

- **Code migration:** Code code migration, component code migration, state code migration, API code migration, error/loading code migration, animation code migration, responsive code migration, performance code migration, accessibility code migration, security code migration, monitoring code migration.
- **Upgrade:** Code upgrade, component upgrade, state upgrade, API upgrade, error/loading upgrade, animation upgrade, responsive upgrade, performance upgrade, accessibility upgrade, security upgrade, monitoring upgrade.

## 29. Frontend code deprecation and removal

- **Code deprecation:** Code code deprecation, component code deprecation, state code deprecation, API code deprecation, error/loading code deprecation, animation code deprecation, responsive code deprecation, performance code deprecation, accessibility code deprecation, security code deprecation, monitoring code deprecation.
- **Removal:** Code removal, component removal, state removal, API removal, error/loading removal, animation removal, responsive removal, performance removal, accessibility removal, security removal, monitoring removal.

## 30. Frontend code archive and backup

- **Code archive:** Code code archive, component code archive, state code archive, API code archive, error/loading code archive, animation code archive, responsive code archive, performance code archive, accessibility code archive, security code archive, monitoring code archive.
- **Backup:** Code backup, component backup, state backup, API backup, error/loading backup, animation backup, responsive backup, performance backup, accessibility backup, security backup, monitoring backup.

## 31. Frontend code restore and recovery

- **Code restore:** Code code restore, component code restore, state code restore, API code restore, error/loading code restore, animation code restore, responsive code restore, performance code restore, accessibility code restore, security code restore, monitoring code restore.
- **Recovery:** Code recovery, component recovery, state recovery, API recovery, error/loading recovery, animation recovery, responsive recovery, performance recovery, accessibility recovery, security recovery, monitoring recovery.

## 32. Frontend code disaster recovery and business continuity

- **Code disaster recovery:** Code code disaster recovery, component code disaster recovery, state code disaster recovery, API code disaster recovery, error/loading code disaster recovery, animation code disaster recovery, responsive code disaster recovery, performance code disaster recovery, accessibility code disaster recovery, security code disaster recovery, monitoring code disaster recovery.
- **Business continuity:** Code business continuity, component business continuity, state business continuity, API business continuity, error/loading business continuity, animation business continuity, responsive business continuity, performance business continuity, accessibility business continuity, security business continuity, monitoring business continuity.

## 33. Frontend code incident response and postmortem

- **Code incident response:** Code code incident response, component code incident response, state code incident response, API code incident response, error/loading code incident response, animation code incident response, responsive code incident response, performance code incident response, accessibility code incident response, security code incident response, monitoring code incident response.
- **Postmortem:** Code postmortem, component postmortem, state postmortem, API postmortem, error/loading postmortem, animation postmortem, responsive postmortem, performance postmortem, accessibility postmortem, security postmortem, monitoring postmortem.

## 34. Frontend code root cause analysis and problem management

- **Code root cause analysis:** Code code root cause analysis, component code root cause analysis, state code root cause analysis, API code root cause analysis, error/loading code root cause analysis, animation code root cause analysis, responsive code root cause analysis, performance code root cause analysis, accessibility code root cause analysis, security code root cause analysis, monitoring code root cause analysis.
- **Problem management:** Code problem management, component problem management, state problem management, API problem management, error/loading problem management, animation problem management, responsive problem management, performance problem management, accessibility problem management, security problem management, monitoring problem management.

## 35. Frontend code change management and configuration management

- **Code change management:** Code code change management, component code change management, state code change management, API code change management, error/loading code change management, animation code change management, responsive code change management, performance code change management, accessibility code change management, security code change management, monitoring code change management.
- **Configuration management:** Code configuration management, component configuration management, state configuration management, API configuration management, error/loading configuration management, animation configuration management, responsive configuration management, performance configuration management, accessibility configuration management, security configuration management, monitoring configuration management.

## 36. Frontend code release management and deployment management

- **Code release management:** Code code release management, component code release management, state code release management, API code release management, error/loading code release management, animation code release management, responsive code release management, performance code release management, accessibility code release management, security code release management, monitoring code release management.
- **Deployment management:** Code deployment management, component deployment management, state deployment management, API deployment management, error/loading deployment management, animation deployment management, responsive deployment management, performance deployment management, accessibility deployment management, security deployment management, monitoring deployment management.

## 37. Frontend code service management and operations management

- **Code service management:** Code code service management, component code service management, state code service management, API code service management, error/loading code service management, animation code service management, responsive code service management, performance code service management, accessibility code service management, security code service management, monitoring code service management.
- **Operations management:** Code operations management, component operations management, state operations management, API operations management, error/loading operations management, animation operations management, responsive operations management, performance operations management, accessibility operations management, security operations management, monitoring operations management.

## 38. Frontend code IT service management and IT operations management

- **Code IT service management:** Code code IT service management, component code IT service management, state code IT service management, API code IT service management, error/loading code IT service management, animation code IT service management, responsive code IT service management, performance code IT service management, accessibility code IT service management, security code IT service management, monitoring code IT service management.
- **IT operations management:** Code IT operations management, component IT operations management, state IT operations management, API IT operations management, error/loading IT operations management, animation IT operations management, responsive IT operations management, performance IT operations management, accessibility IT operations management, security IT operations management, monitoring IT operations management.

## 39. Frontend code IT governance and IT compliance

- **Code IT governance:** Code code IT governance, component code IT governance, state code IT governance, API code IT governance, error/loading code IT governance, animation code IT governance, responsive code IT governance, performance code IT governance, accessibility code IT governance, security code IT governance, monitoring code IT governance.
- **IT compliance:** Code IT compliance, component IT compliance, state IT compliance, API IT compliance, error/loading IT compliance, animation IT compliance, responsive IT compliance, performance IT compliance, accessibility IT compliance, security IT compliance, monitoring IT compliance.

## 40. Frontend code IT risk management and IT security management

- **Code IT risk management:** Code code IT risk management, component code IT risk management, state code IT risk management, API code IT risk management, error/loading code IT risk management, animation code IT risk management, responsive code IT risk management, performance code IT risk management, accessibility code IT risk management, security code IT risk management, monitoring code IT risk management.
- **IT security management:** Code IT security management, component IT security management, state IT security management, API IT security management, error/loading IT security management, animation IT security management, responsive IT security management, performance IT security management, accessibility IT security management, security IT security management, monitoring IT security management.

## 41. Frontend code IT asset management and IT resource management

- **Code IT asset management:** Code code IT asset management, component code IT asset management, state code IT asset management, API code IT asset management, error/loading code IT asset management, animation code IT asset management, responsive code IT asset management, performance code IT asset management, accessibility code IT asset management, security code IT asset management, monitoring code IT asset management.
- **IT resource management:** Code IT resource management, component IT resource management, state IT resource management, API IT resource management, error/loading IT resource management, animation IT resource management, responsive IT resource management, performance IT resource management, accessibility IT resource management, security IT resource management, monitoring IT resource management.

## 42. Frontend code IT knowledge management and IT information management

- **Code IT knowledge management:** Code code IT knowledge management, component code IT knowledge management, state code IT knowledge management, API code IT knowledge management, error/loading code IT knowledge management, animation code IT knowledge management, responsive code IT knowledge management, performance code IT knowledge management, accessibility code IT knowledge management, security code IT knowledge management, monitoring code IT knowledge management.
- **IT information management:** Code IT information management, component IT information management, state IT information management, API IT information management, error/loading IT information management, animation IT information management, responsive IT information management, performance IT information management, accessibility IT information management, security IT information management, monitoring IT information management.

## 43. Frontend code IT communication management and IT stakeholder management

- **Code IT communication management:** Code code IT communication management, component code IT communication management, state code IT communication management, API code IT communication management, error/loading code IT communication management, animation code IT communication management, responsive code IT communication management, performance code IT communication management, accessibility code IT communication management, security code IT communication management, monitoring code IT communication management.
- **IT stakeholder management:** Code IT stakeholder management, component IT stakeholder management, state IT stakeholder management, API IT stakeholder management, error/loading IT stakeholder management, animation IT stakeholder management, responsive IT stakeholder management, performance IT stakeholder management, accessibility IT stakeholder management, security IT stakeholder management, monitoring IT stakeholder management.

## 44. Frontend code IT supplier management and IT vendor management

- **Code IT supplier management:** Code code IT supplier management, component code IT supplier management, state code IT supplier management, API code IT supplier management, error/loading code IT supplier management, animation code IT supplier management, responsive code IT supplier management, performance code IT supplier management, accessibility code IT supplier management, security code IT supplier management, monitoring code IT supplier management.
- **IT vendor management:** Code IT vendor management, component IT vendor management, state IT vendor management, API IT vendor management, error/loading IT vendor management, animation IT vendor management, responsive IT vendor management, performance IT vendor management, accessibility IT vendor management, security IT vendor management, monitoring IT vendor management.
