# Create Mobile App

Generate a complete, production-ready mobile application with modern architecture, professional UI, monetization, and deployment setup.

## Instructions

You are tasked with creating a COMPLETE, production-ready mobile application. This is a one-shot command that must produce a fully functional, polished product ready for app store submission.

### Step 1: Gather Requirements

First, ask the user these essential questions:
1. **App Name & Description**: What is the app name and what does it do?
2. **Platform**: React Native or Flutter?
3. **Target Audience**: Who will use this app?
4. **Core Features**: What are the 5-10 key features/screens?
5. **Backend**: Does it need a backend API? (Provide endpoints or create mock)
6. **Monetization**: Ads, In-App Purchases, Subscription, or Freemium?
7. **Authentication**: Does it require user login? (Email/password, social auth)
8. **App Store**: iOS, Android, or both?

### Step 2: Complete Application Structure

Create the following COMPLETE structure:

#### Project Setup & Configuration
```
my-app/
├── src/
│   ├── screens/           # All app screens
│   ├── components/        # Reusable components
│   ├── navigation/        # Navigation setup
│   ├── services/          # API & external services
│   ├── store/             # State management (Redux/MobX/Context)
│   ├── hooks/             # Custom hooks
│   ├── utils/             # Helper functions
│   ├── constants/         # Constants & config
│   ├── assets/            # Images, fonts, icons
│   ├── theme/             # Colors, typography, spacing
│   └── types/             # TypeScript types (if TS)
├── __tests__/             # Test files
├── android/               # Android native code
├── ios/                   # iOS native code
├── app-store-assets/      # Screenshots, descriptions
├── .env.example           # Environment variables template
├── app.json               # App configuration
├── package.json           # Dependencies
└── README.md              # Complete documentation
```

#### Must Include ALL These Screens/Features:

1. **Splash Screen**
   - Animated logo with brand colors
   - Loading indicator
   - App initialization

2. **Onboarding Flow** (3-4 screens)
   - Feature highlights with illustrations
   - Swipeable carousel
   - Skip button
   - Get Started CTA

3. **Authentication Screens** (if auth required)
   - Login screen (email/password + social)
   - Registration screen with validation
   - Forgot password flow
   - Email verification
   - Error handling with user-friendly messages

4. **Home/Dashboard Screen**
   - Navigation header with menu/profile
   - Main content area
   - Quick actions or featured items
   - Pull-to-refresh functionality
   - Loading states & empty states

5. **Core Feature Screens** (5-7 screens based on app purpose)
   - List views with search & filters
   - Detail views with full information
   - Create/Edit forms with validation
   - Confirmation dialogs
   - Success/error feedback

6. **User Profile Screen**
   - Profile picture upload
   - Editable user information
   - Settings & preferences
   - Account statistics
   - Logout functionality

7. **Settings Screen**
   - App preferences
   - Notification settings
   - Privacy & security options
   - About app & version info
   - Contact/support links
   - Delete account option

8. **Additional Essential Screens**
   - Notifications list
   - Search functionality
   - Favorites/Bookmarks (if applicable)
   - Help/FAQ
   - Terms of Service & Privacy Policy

#### Navigation Setup

Implement COMPLETE navigation structure:
- **Stack Navigator** for screen flow
- **Tab Navigator** for main sections (4-5 tabs)
- **Drawer Navigator** (optional, for side menu)
- Deep linking configuration
- Navigation state persistence
- Back button handling
- Tab bar with icons

#### State Management

Implement COMPLETE state management:
- Global state setup (Redux Toolkit/MobX/Zustand)
- User authentication state
- App data/content state
- UI state (loading, errors, modals)
- Persistence with AsyncStorage
- State hydration on app start
- Actions, reducers/stores, selectors

#### API Integration

Create COMPLETE API service layer:
```javascript
// services/api.js
- Base API client with axios/fetch
- Authentication interceptors (JWT token handling)
- Request/response interceptors
- Error handling & retry logic
- Timeout configuration
- API endpoints for all features:
  * auth: login, register, logout, refresh token
  * user: profile, update, delete
  * content: list, detail, create, update, delete
  * notifications: list, mark read
  * [Other endpoints based on app features]
```

#### Professional UI Components

Create ALL necessary reusable components:
1. **Layout Components**
   - SafeAreaView wrapper
   - Screen container with status bar
   - KeyboardAvoidingView wrapper
   - ScrollView with refresh control

2. **Input Components**
   - TextInput with validation
   - Checkbox, Radio, Switch
   - DatePicker, TimePicker
   - Dropdown/Picker
   - Image picker
   - Search bar with debounce

3. **Display Components**
   - Card with variants
   - List item templates
   - Avatar with fallback
   - Badge & chip
   - Tag/Label
   - Progress indicators
   - Rating component

4. **Navigation Components**
   - Header with back/menu buttons
   - Tab bar with icons
   - Bottom sheet
   - Drawer menu

5. **Feedback Components**
   - Loading spinner & skeleton screens
   - Toast notifications
   - Alert dialogs
   - Confirmation modals
   - Empty state views
   - Error state views

6. **Interactive Components**
   - Primary, secondary, text buttons
   - Icon buttons
   - Floating action button
   - Swipeable list items
   - Pull-to-refresh

#### Theme System

Implement COMPLETE theming:
```javascript
// theme/index.js
export const theme = {
  colors: {
    primary: '#007AFF',
    secondary: '#5856D6',
    success: '#34C759',
    warning: '#FF9500',
    error: '#FF3B30',
    background: '#FFFFFF',
    surface: '#F2F2F7',
    text: '#000000',
    textSecondary: '#8E8E93',
    border: '#C6C6C8',
    // ... 20+ color definitions
  },
  typography: {
    h1: { fontSize: 34, fontWeight: 'bold' },
    h2: { fontSize: 28, fontWeight: '600' },
    h3: { fontSize: 22, fontWeight: '600' },
    body: { fontSize: 17, fontWeight: '400' },
    caption: { fontSize: 12, fontWeight: '400' },
    // ... complete typography scale
  },
  spacing: {
    xs: 4, sm: 8, md: 16, lg: 24, xl: 32, xxl: 48
  },
  borderRadius: {
    sm: 4, md: 8, lg: 12, xl: 16, round: 999
  },
  shadows: {
    // Platform-specific shadow definitions
  }
}
```

#### Push Notifications

Implement COMPLETE push notification setup:
1. **Configuration**
   - React Native Firebase or Expo Notifications
   - FCM setup for Android
   - APNs setup for iOS
   - Permission requests

2. **Implementation**
   ```javascript
   // services/notifications.js
   - Request permissions
   - Get device token
   - Register token with backend
   - Handle foreground notifications
   - Handle background notifications
   - Handle notification taps
   - Deep link navigation from notifications
   - Local notifications
   - Scheduled notifications
   - Badge count management
   ```

3. **Notification Types**
   - System notifications
   - User activity notifications
   - Promotional notifications
   - Transaction notifications

#### Analytics Integration

Implement COMPLETE analytics tracking:
1. **Setup Multiple Providers**
   - Google Analytics / Firebase Analytics
   - Mixpanel or Amplitude
   - Facebook Analytics (optional)

2. **Track Everything**
   ```javascript
   // services/analytics.js
   - Screen view tracking (auto on navigation)
   - User properties (age, location, subscription status)
   - Custom events:
     * App launch
     * User registration/login
     * Feature usage
     * Button clicks
     * Form submissions
     * Purchases
     * Errors & crashes
     * Session duration
   - Conversion funnels
   - A/B test variants
   ```

#### Error Tracking & Monitoring

Implement COMPLETE error tracking:
1. **Sentry Integration**
   - Crash reporting
   - Error boundaries
   - Breadcrumbs
   - User context
   - Release tracking

2. **Custom Error Handling**
   ```javascript
   // utils/errorHandler.js
   - Global error handler
   - Network error handling
   - API error handling
   - User-friendly error messages
   - Error retry mechanisms
   - Offline error queueing
   - Error logging
   ```

#### Monetization Implementation

Implement COMPLETE monetization based on chosen strategy:

**Option A: In-App Purchases**
```javascript
// services/iap.js
- react-native-iap integration
- Product definitions (consumable, non-consumable, subscriptions)
- Purchase flow
- Receipt validation
- Restore purchases
- Subscription management
- Products catalog UI
- Payment success/failure handling
- Revenue tracking
```

**Option B: Subscriptions**
```javascript
// services/subscriptions.js
- Subscription tiers (Free, Pro, Premium)
- Subscription UI/paywall
- Trial period handling
- Subscription status checking
- Auto-renewal management
- Upgrade/downgrade flows
- Cancellation handling
- Billing history
- Feature gating based on plan
```

**Option C: Ad Monetization**
```javascript
// services/ads.js
- Google AdMob integration
- Banner ads (bottom of screens)
- Interstitial ads (between actions)
- Rewarded video ads
- Native ads in content
- Ad placement strategy
- Ad frequency capping
- Ad-free premium option
- GDPR consent for ads
```

#### App Store Assets

Create COMPLETE app store presence:

1. **App Icons**
   - iOS: All required sizes (1024x1024, 60x60, etc.)
   - Android: All required densities (mdpi to xxxhdpi)
   - Adaptive icon for Android
   - Professional design matching brand

2. **Screenshots** (5-10 per platform)
   - iPhone 6.7" (Pro Max)
   - iPhone 6.5" (Plus)
   - iPhone 5.5"
   - iPad Pro 12.9"
   - Android Phone
   - Android Tablet
   - Localized for key markets

3. **App Store Description**
   ```
   Title: [Compelling 30-char title]
   Subtitle: [Clear value prop 30-char]

   Description:
   - Hook paragraph (problem/solution)
   - Key features (bullet points)
   - Benefits & differentiators
   - Social proof
   - Call to action

   Keywords: [Optimized keyword list]

   What's New: [Update notes]

   Promo Text: [170-char pitch]
   ```

4. **App Store Metadata**
   - Category selection (primary & secondary)
   - Age rating with accurate content
   - Privacy policy URL
   - Support URL
   - Marketing URL
   - Copyright info

5. **App Preview Videos** (specification)
   - 15-30 second video showing key features
   - Storyboard with timestamps
   - Voiceover script
   - Music selection

#### Performance Optimization

Implement ALL performance optimizations:
1. **Rendering**
   - FlatList with proper optimization
   - Image optimization & caching
   - Lazy loading
   - Memoization (React.memo, useMemo)
   - Avoid unnecessary re-renders

2. **Bundle Optimization**
   - Code splitting
   - Dynamic imports
   - Remove unused dependencies
   - Hermes engine (React Native)
   - ProGuard (Android)

3. **Network**
   - Request caching
   - Batch API requests
   - Compress images before upload
   - Prefetch critical data
   - Offline support

4. **Storage**
   - AsyncStorage best practices
   - Data persistence strategy
   - Cache invalidation
   - Storage cleanup

#### Testing

Implement COMPLETE test coverage:
1. **Unit Tests**
   - Utilities & helpers
   - Business logic
   - Reducers/stores
   - API services
   - Custom hooks

2. **Component Tests**
   - React Testing Library
   - All components
   - User interactions
   - Snapshot tests

3. **Integration Tests**
   - Navigation flows
   - Authentication flow
   - Purchase flow
   - API integration

4. **E2E Tests**
   - Detox setup
   - Critical user journeys
   - Onboarding flow
   - Main feature flows

#### Security Implementation

Implement ALL security measures:
1. **Data Security**
   - Secure storage (react-native-keychain)
   - Encrypt sensitive data
   - SSL pinning
   - Obfuscate API keys
   - Secure token storage

2. **Authentication Security**
   - JWT with refresh tokens
   - Biometric authentication
   - Session management
   - Logout on token expiry
   - Rate limiting

3. **Code Security**
   - Code obfuscation
   - API endpoint protection
   - Input validation
   - XSS prevention
   - SQL injection prevention

#### Offline Support

Implement COMPLETE offline functionality:
```javascript
// services/offline.js
- Network connectivity detection
- Offline data persistence
- Queue sync when online
- Optimistic UI updates
- Conflict resolution
- Offline banner/indicator
- Cache strategies
```

#### Accessibility

Implement COMPLETE accessibility:
- Screen reader support
- Accessible labels
- Font scaling support
- High contrast mode
- Keyboard navigation
- Focus management
- Semantic HTML/native elements

#### Internationalization (i18n)

Implement COMPLETE translation system:
```javascript
// i18n/index.js
- react-i18next or react-native-localize
- Language files (en, es, fr, de, etc.)
- All text strings externalized
- Date/time localization
- Number formatting
- Currency formatting
- RTL support
- Language switcher in settings
```

#### Documentation

Create COMPLETE documentation:

1. **README.md**
   ```markdown
   # App Name

   ## Overview
   [Description, features, screenshots]

   ## Tech Stack
   [All technologies used]

   ## Prerequisites
   [System requirements]

   ## Installation
   [Step-by-step setup]

   ## Configuration
   [Environment variables]

   ## Running the App
   [Dev, iOS, Android commands]

   ## Building for Production
   [iOS and Android build steps]

   ## Testing
   [How to run tests]

   ## Deployment
   [App store submission process]

   ## Troubleshooting
   [Common issues]

   ## Contributing
   [Guidelines]

   ## License
   ```

2. **ARCHITECTURE.md**
   - Project structure explanation
   - Design patterns used
   - State management flow
   - Navigation structure
   - API integration approach
   - Component hierarchy

3. **DEPLOYMENT.md**
   - iOS deployment guide
   - Android deployment guide
   - Environment setup
   - Certificate management
   - Store submission checklist

4. **API_DOCUMENTATION.md**
   - All API endpoints
   - Request/response formats
   - Authentication flow
   - Error codes

#### Build & Deployment Setup

Create COMPLETE build configuration:

1. **Environment Configuration**
   ```javascript
   // .env.example
   API_BASE_URL=https://api.example.com
   GOOGLE_ANALYTICS_ID=UA-XXXXX
   SENTRY_DSN=https://xxx@sentry.io/xxx
   STRIPE_PUBLIC_KEY=pk_test_xxx
   ADMOB_APP_ID=ca-app-pub-xxx
   // ... all keys
   ```

2. **iOS Build Setup**
   - Xcode project configuration
   - Provisioning profiles
   - Signing certificates
   - App Store Connect setup
   - Fastlane configuration
   - Build scripts

3. **Android Build Setup**
   - Gradle configuration
   - Signing key setup
   - Google Play Console setup
   - Fastlane configuration
   - Build scripts

4. **CI/CD Pipeline**
   ```yaml
   # .github/workflows/deploy.yml
   - Automated testing on push
   - Build on release branch
   - Deploy to TestFlight/Play Store Beta
   - Screenshot generation
   - Version bumping
   ```

5. **Release Process**
   - Version bump script
   - Changelog generation
   - App store submission checklist
   - Beta testing process

### Step 3: Code Quality

Ensure ALL code follows best practices:
- **TypeScript** (if chosen): Full type coverage
- **ESLint**: Configured and passing
- **Prettier**: Consistent formatting
- **PropTypes** (if JS): All components
- **Comments**: Complex logic explained
- **Error Handling**: Comprehensive try-catch
- **Loading States**: Every async operation
- **Empty States**: Every list/data view
- **Validation**: All user inputs

### Step 4: Final Deliverables

Provide these COMPLETE outputs:

1. **All Source Code** (production-ready)
2. **Complete Documentation** (README, ARCHITECTURE, DEPLOYMENT)
3. **App Store Assets** (icons, screenshots, descriptions)
4. **Environment Setup Guide** (step-by-step)
5. **Build & Deploy Scripts** (automated)
6. **Testing Coverage Report** (>80% coverage)
7. **Performance Audit** (load times, bundle size)
8. **Security Checklist** (completed)
9. **Accessibility Audit** (WCAG compliance)
10. **Launch Checklist** (pre-submission review)

### Important Guidelines

- **Production-Ready**: All code must be clean, tested, and deployable
- **No Placeholders**: Every feature must be fully implemented
- **Professional UI**: Polished, modern design
- **Error Handling**: Comprehensive coverage
- **User Experience**: Smooth, intuitive, delightful
- **Performance**: Optimized for speed
- **Security**: Protected against common vulnerabilities
- **Monetization**: Revenue streams properly integrated
- **Analytics**: Track everything for optimization
- **Documentation**: Clear, comprehensive guides

### Revenue Focus

Ensure the app is optimized for revenue:
- **Conversion Optimization**: Clear CTAs, minimal friction
- **Retention Features**: Push notifications, personalization, gamification
- **Monetization**: Properly implemented and tested
- **Analytics**: Track funnel, LTV, churn
- **A/B Testing**: Setup for optimization
- **Viral Features**: Sharing, referrals, social proof
- **Premium Features**: Clear value proposition

## Success Criteria

The command is successful when you deliver:
✅ Complete, production-ready mobile app
✅ All screens and features fully implemented
✅ Professional UI with consistent design
✅ Backend integration (or comprehensive mocks)
✅ Monetization fully integrated and tested
✅ Push notifications working
✅ Analytics tracking all key events
✅ Error tracking with Sentry
✅ App store assets ready for submission
✅ Complete documentation for developers and users
✅ Build scripts for iOS and Android
✅ Deployment guide for app stores
✅ 80%+ test coverage
✅ Performance optimized
✅ Security hardened
✅ Accessibility compliant

This should be a COMPLETE, POLISHED product ready for immediate app store submission and revenue generation.
