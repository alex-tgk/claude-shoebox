# UI/UX Prompts

A collection of prompt templates for design, user experience, component creation, and interface development.

---

## Component Design

### 1. Design Component Specification

**Purpose:** Create comprehensive specification for a UI component.

**Prompt:**
```
Create a component specification for [COMPONENT_NAME]:

Component purpose:
[DESCRIPTION]

Specification should include:
- Component overview and use cases
- Visual design description
- States (default, hover, focus, disabled, loading, error)
- Variants (sizes, styles, themes)
- Props/attributes and their types
- Behavior and interactions
- Accessibility requirements (ARIA, keyboard navigation)
- Responsive considerations
- Content guidelines (character limits, text wrapping)
- Examples of usage (do's and don'ts)
- Related components
- Technical considerations

Write for designers and developers.
```

**Example:**
```
Component specification for Button component:

Purpose: Primary interactive element for user actions

Specification:

Overview:
Buttons trigger actions, submit forms, or navigate. Used throughout the app for primary, secondary, and tertiary actions.

Visual Design:
- Rounded corners (8px border-radius)
- Padding: 12px horizontal, 8px vertical (medium)
- Typography: 16px, semi-bold, sentence case
- Colors: Primary (blue), Secondary (gray), Destructive (red)
- Drop shadow on hover: 0 2px 4px rgba(0,0,0,0.1)

States:
- Default: Solid background, white text
- Hover: 10% darker background, shadow, cursor pointer
- Focus: 2px blue outline, 2px offset
- Active/pressed: 15% darker, slight scale down (0.98)
- Disabled: 50% opacity, no pointer, no hover
- Loading: Spinner replaces text, button disabled

Variants:
- Size: Small (32px), Medium (40px), Large (48px)
- Style: Filled, Outline, Ghost (text only)
- Width: Auto, Full-width
- Icon: Leading icon, trailing icon, icon-only

Props:
- label (string, required for non-icon buttons)
- onClick (function, required)
- variant (primary|secondary|destructive, default: primary)
- size (small|medium|large, default: medium)
- disabled (boolean, default: false)
- loading (boolean, default: false)
- icon (component, optional)
- fullWidth (boolean, default: false)

Behavior:
- Click triggers onClick handler
- Keyboard: Enter or Space activates
- Loading state prevents multiple submissions
- Disabled state blocks all interactions

Accessibility:
- role="button" (or use <button> element)
- aria-disabled="true" when disabled
- aria-busy="true" when loading
- Sufficient color contrast (4.5:1 minimum)
- Visible focus indicator
- Label required (aria-label for icon-only)

Responsive:
- Touch target minimum 44x44px (mobile)
- Full-width on mobile for primary CTAs

Content:
- Labels: 1-3 words, action verbs ("Save", "Delete", "Learn More")
- Avoid "Click Here" or "Submit"
- Max length: 20 characters recommended

Examples:
✓ Do: "Save Changes", "Delete Account", "Add to Cart"
✗ Don't: "Click Here", "SUBMIT", "OK"

Related: IconButton, Link, MenuButton

Technical:
- Ensure button doesn't grow with loading state (fixed width)
- Prevent double-click with loading state
- Use semantic <button> element, not <div>
```

---

### 2. Generate Component Code

**Purpose:** Generate code for a UI component based on design specs.

**Prompt:**
```
Generate [FRAMEWORK] component code for [COMPONENT_NAME]:

Design specifications:
[DESIGN_SPECS or COMPONENT_DESCRIPTION]

Requirements:
- Framework: [REACT/VUE/ANGULAR/SVELTE/WEB_COMPONENTS]
- Styling approach: [CSS_MODULES/STYLED_COMPONENTS/TAILWIND/ETC]
- TypeScript: [YES/NO]
- Accessibility: WCAG [A/AA/AAA] compliant
- Props/API: [SPECIFY_PROPS]
- States: [REQUIRED_STATES]
- Responsive: [BREAKPOINTS]

Include:
- Component code
- Type definitions
- Styles
- Usage examples
- Accessibility features
- Unit test suggestions

Follow [STYLE_GUIDE] conventions.
```

**Example:**
```
Generate React component for Modal/Dialog:

Design specs:
- Overlay with centered content box
- Close button (X) in top-right
- Optional header, body, footer sections
- Click outside or Escape key to close
- Scrollable body if content overflows
- Smooth fade-in/out animation

Requirements:
- React 18 with TypeScript
- Tailwind CSS for styling
- WCAG AA compliant
- Props: isOpen, onClose, title, children, footer
- States: Opening, open, closing, closed
- Responsive: Full-screen on mobile, centered modal on desktop

Include:
- Modal component with TypeScript
- Portal rendering (to body)
- Focus trap and focus management
- Scroll lock on body when open
- ESC key handler
- Click outside handler
- Tailwind classes with animations
- Example: Confirmation dialog, Form modal
- Accessibility: role="dialog", aria-labelledby, focus management
- Test: Opening, closing, keyboard navigation, click outside

Follow Airbnb React style guide.

[Generate complete component code with all features]
```

---

### 3. Component Library Setup

**Purpose:** Set up structure for a component library.

**Prompt:**
```
Create a component library structure for [LIBRARY_NAME]:

Library details:
- Framework: [REACT/VUE/WEB_COMPONENTS/ETC]
- Components to include: [COMPONENT_LIST]
- Target: [INTERNAL/OPEN_SOURCE]
- Documentation: [STORYBOOK/DOCUSAURUS/ETC]

Provide:
- Project structure (folders, files)
- Build configuration
- Component template/boilerplate
- Documentation setup
- Testing setup
- Styling architecture
- Versioning strategy
- Publishing process (if applicable)
- Getting started guide

Include package.json, build scripts, and tooling configuration.
```

**Example:**
```
Component library structure: React design system for company products

Library:
- React 18 with TypeScript
- Components: Button, Input, Select, Modal, Card, Tabs, Table, etc. (20 total)
- Internal use across 5 products
- Storybook for documentation

Structure:
```
design-system/
├── src/
│   ├── components/
│   │   ├── Button/
│   │   │   ├── Button.tsx
│   │   │   ├── Button.test.tsx
│   │   │   ├── Button.stories.tsx
│   │   │   ├── Button.module.css
│   │   │   └── index.ts
│   │   └── [other components]
│   ├── styles/
│   │   ├── tokens.css (design tokens)
│   │   ├── globals.css
│   │   └── themes/
│   ├── hooks/
│   ├── utils/
│   └── index.ts (main export)
├── .storybook/
├── package.json
├── tsconfig.json
├── rollup.config.js
└── README.md
```

Build: Rollup for ESM/CJS bundles, TypeScript for types
Template: Component generator script (npm run generate:component)
Docs: Storybook with Docs addon, auto-generate props tables
Testing: Jest + React Testing Library, 80% coverage
Styles: CSS Modules with design tokens, theme support
Versioning: Semantic versioning, conventional commits
Publishing: npm private registry, automated via CI
Getting started: README with installation, usage, development guide

[Provide complete package.json, rollup config, component template script]
```

---

## User Experience

### 4. User Flow Design

**Purpose:** Design user flows for features or tasks.

**Prompt:**
```
Design a user flow for [TASK/FEATURE]:

Context:
- User goal: [WHAT_USER_WANTS_TO_ACCOMPLISH]
- Entry point: [WHERE_FLOW_STARTS]
- Success criteria: [WHAT_DEFINES_SUCCESS]
- User type: [PERSONA]

Flow should include:
- Step-by-step sequence
- Decision points (conditions, branches)
- User actions at each step
- System responses
- Error paths and recovery
- Alternative paths
- Exit points
- Estimated time to complete
- Screen/page descriptions for each step

Present as flowchart description or numbered steps.
Identify friction points and optimization opportunities.
```

**Example:**
```
User flow for Password Reset:

Context:
- Goal: User wants to reset forgotten password and regain account access
- Entry: "Forgot password?" link on login page
- Success: User logged in with new password
- User: Returning user who forgot password

Flow:

1. Login Page
   - User clicks "Forgot password?"
   - → Navigates to Reset Request page

2. Reset Request Page
   - User enters email address
   - User clicks "Send reset link"
   - System validates email format

   Decision: Email valid?
   - NO → Show error "Please enter a valid email", stay on page
   - YES → Continue

3. System Processing
   - System checks if email exists in database

   Decision: Email exists?
   - NO → Still show success message (security: don't reveal non-existent accounts)
   - YES → Generate reset token, send email with link

4. Confirmation Page
   - Show "Check your email for reset instructions"
   - Display email address (partially masked: j***@example.com)
   - Offer "Didn't receive email?" link
   - Exit: User checks email

5. Email
   - User receives email (within 2 minutes)
   - User clicks reset link in email
   - → Opens Reset Password page with token in URL

   Decision: Token valid?
   - NO → Show "Link expired or invalid" + Request new link button
   - YES → Show password reset form

6. Reset Password Page
   - User enters new password
   - Show password strength indicator (weak/medium/strong)
   - User confirms new password
   - User clicks "Reset Password"

   Validation:
   - Password meets requirements (8+ chars, etc.)?
   - Passwords match?
   - NO → Show error, stay on page
   - YES → Continue

7. System Processing
   - Hash new password
   - Update database
   - Invalidate reset token
   - Create new session
   - → Redirect to Dashboard

8. Success
   - User lands on dashboard
   - Show success toast: "Password reset successfully"
   - User is now logged in

Alternative Paths:
- Token expired (step 5): Request new reset link → Back to step 2
- Didn't receive email (step 4): Resend email → Back to step 3
- Cancel at any point → Return to login

Error Paths:
- Network error sending email → Show error, retry button
- Database error → Generic error message, log for investigation

Estimated Time: 3-5 minutes

Friction Points:
- Email delivery delay (user anxiety) → Show "This may take a few minutes"
- Password requirements not clear → Show requirements upfront
- Token expiration (15 min) might be too short → Consider 30 min

Optimizations:
- Add "Show password" toggle for easier entry
- Allow paste in password fields
- Auto-login after successful reset (don't make them login again)
- Send confirmation email after reset
```

---

### 5. Wireframe Description

**Purpose:** Describe wireframes for screens or pages.

**Prompt:**
```
Create wireframe descriptions for [SCREEN/FEATURE]:

Context:
- Purpose: [WHAT_THIS_SCREEN_DOES]
- User: [PERSONA]
- Entry point: [HOW_USER_ARRIVES]
- Device: [MOBILE/TABLET/DESKTOP/RESPONSIVE]

For each screen describe:
- Layout structure (header, main, sidebar, footer)
- Content sections (in order, top to bottom)
- UI components and their purpose
- Content hierarchy (headings, body text, etc.)
- Interactive elements (buttons, links, forms)
- Navigation elements
- States to consider (empty, loading, error, success)
- Responsive behavior
- Annotations for interactions

Describe in enough detail for a designer to create mockups.
```

**Example:**
```
Wireframe: E-commerce Product Details Page (Desktop)

Context:
- Purpose: Display product information, enable purchase
- User: Shopper evaluating product
- Entry: From search results, category page, or direct link
- Device: Desktop (responsive variant needed for mobile)

Layout:
- Header: Logo (left), search bar (center), cart icon (right)
- Breadcrumb navigation below header
- Main content area: 2-column layout
- Footer: Standard site footer

Main Content (Left Column - 60%):

1. Product Image Gallery
   - Large main image (600x600px)
   - Thumbnail strip below (5-6 images)
   - Zoom on hover
   - Lightbox on click
   - Image: Product from multiple angles, lifestyle photos

2. Product Reviews Section (below images)
   - Heading: "Customer Reviews" + average star rating (4.5/5)
   - Filter/sort controls (Most Helpful, Newest)
   - Review cards (3 visible, "Load more" button)
   - Each review: Stars, title, text, reviewer name, date, helpful count

Main Content (Right Column - 40%):

3. Product Information
   - Breadcrumb path: Home > Category > Product
   - Product title (H1): "Premium Wireless Headphones"
   - Star rating + review count: "★★★★☆ (247 reviews)" (link to reviews below)
   - Price: Large, bold "$199.99"
   - Availability: "In Stock" (green) or "Out of Stock" (red)

4. Product Options
   - Color selector: Color swatches (Black, White, Gray selected)
   - Size/variant (if applicable)
   - Quantity selector: [-] [1] [+] buttons

5. Call-to-Action Buttons
   - Primary button: "Add to Cart" (large, blue, full-width)
   - Secondary button: "Add to Wishlist" (outline, heart icon)
   - Link: "View in AR" (if supported)

6. Key Features
   - Bulleted list (5-7 items)
   - Icons next to each (e.g., battery icon, checkmark)
   - Example: "40-hour battery life", "Active noise cancellation"

7. Shipping & Returns
   - Free shipping icon + "Free delivery on orders over $50"
   - Returns icon + "30-day return policy"
   - Estimated delivery: "Arrives Dec 15-18"

8. Product Details Tabs (below)
   - Tabs: Description | Specifications | Shipping
   - Description: Full product description, 2-3 paragraphs
   - Specifications: Table with technical details
   - Shipping: Delivery options, international shipping info

Interactive Elements:
- Image gallery: Click to zoom, arrow keys to navigate
- Color swatches: Click to select, updates main image
- Quantity: +/- buttons, or direct input (max 10)
- Add to Cart: Adds product, shows cart modal
- Star rating: Click to filter reviews
- Tabs: Click to switch content

States:
- Loading: Skeleton loaders for images and content
- Out of Stock: Disable Add to Cart, show "Notify When Available" button
- Error: Show error message if product not found
- Success: Show "Added to cart" toast message

Responsive (Mobile):
- Single column layout
- Image gallery stacks above product info
- Sticky "Add to Cart" button at bottom
- Tabs become accordion

Annotations:
- Clicking thumbnail should update main image
- Price should be dynamic based on options selected
- Reviews should lazy-load
- Add to Cart should update header cart count
- Breadcrumbs should be clickable navigation
```

---

### 6. Interaction Design Specification

**Purpose:** Define interaction patterns and micro-interactions.

**Prompt:**
```
Define interaction design for [FEATURE/COMPONENT]:

Feature:
[DESCRIPTION]

Specify interactions:
- Trigger (what initiates the interaction)
- Action (what happens)
- Feedback (visual, audio, haptic response)
- Timing (duration, easing, delays)
- States before and after
- Edge cases (interrupted, repeated actions)
- Accessibility considerations

For animations provide:
- Duration (milliseconds)
- Easing function
- Properties that change
- Performance considerations

Focus on delightful, intuitive interactions that provide clear feedback.
```

**Example:**
```
Interaction design for "Like" button (social media post):

Feature: Button that allows users to like/unlike posts

Interactions:

1. Hover (Desktop)
   - Trigger: Mouse enters button area
   - Action: Scale button to 1.05x
   - Feedback: Color lightens 10%, cursor: pointer
   - Timing: 150ms, ease-out
   - State: Idle → Hover
   - Edge: Hover during animation → Complete current, start hover

2. Click/Tap to Like
   - Trigger: User clicks unliked button
   - Action:
     - Icon changes from outline to filled heart
     - Heart scales to 1.3x then back to 1x (pop effect)
     - Color changes from gray to red
     - Count increments (+1)
     - Particle burst animation (small hearts emanate)
   - Feedback:
     - Visual: Animation sequence
     - Haptic: Light tap (mobile)
     - Audio: Optional subtle "pop" sound
   - Timing:
     - Heart fill: 0ms (instant)
     - Scale up: 200ms, ease-out
     - Scale down: 150ms, ease-in-out
     - Particles: 400ms, fade and rise, ease-out
     - Total: 400ms
   - State: Unliked → Liked
   - Properties: scale, color, opacity (particles)
   - Performance: Use CSS transforms (GPU-accelerated), limit particles to 8

3. Click/Tap to Unlike
   - Trigger: User clicks liked button
   - Action:
     - Icon changes from filled to outline
     - Simple fade transition (no pop animation)
     - Color changes from red to gray
     - Count decrements (-1)
   - Feedback: Subtle fade, no particles
   - Timing: 200ms, ease-in-out
   - State: Liked → Unliked

4. Loading State (API call in progress)
   - Trigger: Click sent to server
   - Action: Button pulses slightly
   - Feedback: Subtle opacity animation (0.7 → 1.0 → 0.7)
   - Timing: 1s loop until response
   - State: Liked/Unliked → Loading → Liked/Unliked
   - Edge: Prevent additional clicks during loading

5. Error State (API call failed)
   - Trigger: Server returns error
   - Action: Revert to previous state, shake animation
   - Feedback: Red shake (3px left-right × 3), show error toast
   - Timing: 400ms for shake, toast for 3s
   - State: Loading → Previous state (with error indication)

6. Optimistic Update
   - Trigger: Immediate on click (don't wait for server)
   - Action: Update UI instantly, send API request in background
   - Feedback: Immediate visual change
   - Timing: Instant UI, ~200ms API roundtrip
   - Edge: If API fails, revert and show error (rare)

Edge Cases:
- Double-click: Ignore second click if within 500ms
- Rapid clicking: Queue actions, process sequentially
- Interrupted animation: Complete to final state, don't leave partial
- Network offline: Show warning, queue action for later

Accessibility:
- Keyboard: Space or Enter triggers like/unlike
- Focus: Clear focus ring (2px blue outline)
- Screen reader: Announce "Liked" or "Unliked" on change
- Label: aria-label="Like post" changes to "Unlike post"
- No reliance on color alone (icon shape changes)
- Reduced motion: Skip scale/particle animations, instant transition

Performance:
- Use requestAnimationFrame for smooth 60fps
- CSS transforms (scale) not width/height
- Particles as CSS, not canvas (simpler for 8 particles)
- Debounce API calls (don't send if un-liking within 1s)
```

---

## Design Systems

### 7. Design Tokens Definition

**Purpose:** Define design tokens for a design system.

**Prompt:**
```
Create design tokens for [DESIGN_SYSTEM_NAME]:

Token categories:
- Colors (brand, semantic, neutral, feedback)
- Typography (font families, sizes, weights, line heights)
- Spacing (margins, paddings, gaps)
- Sizing (component dimensions)
- Border radius (corner rounding)
- Shadows (elevation levels)
- Transitions (duration, easing)
- Z-index (layering)
- Breakpoints (responsive)

For each token provide:
- Token name (semantic naming convention)
- Value
- Usage guidance
- Platform-specific values if needed (web, iOS, Android)

Format: [JSON/CSS_VARIABLES/SASS/STYLE_DICTIONARY]

Ensure tokens are semantic, not prescriptive (use "primary" not "blue").
```

**Example:**
```
Design tokens for SaaS product design system:

Format: CSS Custom Properties

Colors:
```css
/* Brand Colors */
--color-brand-primary: #0066FF;
--color-brand-primary-dark: #0052CC;
--color-brand-primary-light: #4D94FF;
--color-brand-secondary: #6E56CF;

/* Semantic Colors */
--color-background-primary: #FFFFFF;
--color-background-secondary: #F8F9FA;
--color-background-tertiary: #E9ECEF;

--color-text-primary: #1A202C;
--color-text-secondary: #4A5568;
--color-text-tertiary: #A0AEC0;

--color-border-default: #E2E8F0;
--color-border-hover: #CBD5E0;
--color-border-focus: var(--color-brand-primary);

/* Feedback Colors */
--color-success: #10B981;
--color-warning: #F59E0B;
--color-error: #EF4444;
--color-info: #3B82F6;

/* Usage: backgrounds, text, borders with semantic meaning */
```

Typography:
```css
/* Font Families */
--font-family-sans: 'Inter', -apple-system, sans-serif;
--font-family-mono: 'JetBrains Mono', monospace;

/* Font Sizes */
--font-size-xs: 0.75rem;    /* 12px */
--font-size-sm: 0.875rem;   /* 14px */
--font-size-base: 1rem;     /* 16px */
--font-size-lg: 1.125rem;   /* 18px */
--font-size-xl: 1.25rem;    /* 20px */
--font-size-2xl: 1.5rem;    /* 24px */
--font-size-3xl: 1.875rem;  /* 30px */
--font-size-4xl: 2.25rem;   /* 36px */

/* Font Weights */
--font-weight-normal: 400;
--font-weight-medium: 500;
--font-weight-semibold: 600;
--font-weight-bold: 700;

/* Line Heights */
--line-height-tight: 1.25;
--line-height-normal: 1.5;
--line-height-relaxed: 1.75;

/* Usage: body text uses base size, headings use xl-4xl */
```

Spacing (4px base unit):
```css
--spacing-1: 0.25rem;  /* 4px */
--spacing-2: 0.5rem;   /* 8px */
--spacing-3: 0.75rem;  /* 12px */
--spacing-4: 1rem;     /* 16px */
--spacing-5: 1.25rem;  /* 20px */
--spacing-6: 1.5rem;   /* 24px */
--spacing-8: 2rem;     /* 32px */
--spacing-10: 2.5rem;  /* 40px */
--spacing-12: 3rem;    /* 48px */
--spacing-16: 4rem;    /* 64px */

/* Usage: margin, padding, gap - use 4px multiples */
```

Sizing:
```css
--size-icon-sm: 1rem;      /* 16px */
--size-icon-base: 1.25rem; /* 20px */
--size-icon-lg: 1.5rem;    /* 24px */

--size-button-sm: 2rem;    /* 32px height */
--size-button-base: 2.5rem; /* 40px height */
--size-button-lg: 3rem;    /* 48px height */

--size-input-height: 2.5rem; /* 40px */
```

Border Radius:
```css
--radius-sm: 0.25rem;  /* 4px - tags */
--radius-base: 0.5rem; /* 8px - buttons, inputs */
--radius-lg: 0.75rem;  /* 12px - cards */
--radius-xl: 1rem;     /* 16px - modals */
--radius-full: 9999px; /* Pills, avatars */
```

Shadows (elevation):
```css
--shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
--shadow-base: 0 1px 3px rgba(0, 0, 0, 0.1);
--shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
--shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
--shadow-xl: 0 20px 25px rgba(0, 0, 0, 0.1);

/* Usage: sm=buttons, md=dropdowns, lg=modals */
```

Transitions:
```css
--transition-fast: 150ms;
--transition-base: 250ms;
--transition-slow: 350ms;

--ease-in: cubic-bezier(0.4, 0, 1, 1);
--ease-out: cubic-bezier(0, 0, 0.2, 1);
--ease-in-out: cubic-bezier(0.4, 0, 0.2, 1);

/* Usage: transition: all var(--transition-base) var(--ease-out); */
```

Z-index (layering):
```css
--z-index-dropdown: 1000;
--z-index-sticky: 1100;
--z-index-modal: 1200;
--z-index-popover: 1300;
--z-index-tooltip: 1400;
--z-index-toast: 1500;
```

Breakpoints:
```css
--breakpoint-sm: 640px;
--breakpoint-md: 768px;
--breakpoint-lg: 1024px;
--breakpoint-xl: 1280px;
--breakpoint-2xl: 1536px;

/* Usage: @media (min-width: var(--breakpoint-md)) */
```

Platform-specific (if needed):
- Web: Use CSS variables above
- iOS: Export to Swift constants
- Android: Export to XML resources
- React Native: Export to JavaScript object

Tool: Style Dictionary for multi-platform export

Naming Convention:
- Category-Variant-State: --color-background-primary
- Semantic, not prescriptive: --color-error not --color-red
- Consistent scale: 1-12 for spacing, xs-4xl for sizes
```

---

### 8. Accessibility Audit

**Purpose:** Audit design or implementation for accessibility issues.

**Prompt:**
```
Perform an accessibility audit on [PAGE/COMPONENT]:

Context:
- Target: [DESCRIPTION or URL]
- WCAG Level: [A/AA/AAA]
- User groups: [DISABILITIES_TO_CONSIDER]

Audit areas:
- Perceivable (text alternatives, color contrast, adaptable content)
- Operable (keyboard accessible, timing, navigation)
- Understandable (readable, predictable, input assistance)
- Robust (compatible with assistive technologies)

For each issue found:
- Issue description
- WCAG criterion violated (e.g., 1.4.3 Contrast)
- Severity (Critical/High/Medium/Low)
- User impact
- How to reproduce
- Recommended fix
- Code example (if applicable)

Test with:
- Keyboard navigation
- Screen reader ([NVDA/JAWS/VOICEOVER])
- Color contrast checker
- Automated tools ([AXE/LIGHTHOUSE/WAVE])
```

**Example:**
```
Accessibility audit: Login page (WCAG 2.1 AA)

Context:
- Page: User login form
- Target: AA compliance
- Users: Blind (screen readers), low vision, motor disabilities, keyboard-only

Findings:

1. Insufficient Color Contrast
   - Issue: "Forgot password?" link is light gray (#999) on white background
   - WCAG: 1.4.3 Contrast (Minimum) - Level AA
   - Severity: HIGH
   - Impact: Low vision users can't read link
   - Reproduce: Check contrast ratio, shows 2.8:1 (need 4.5:1)
   - Fix: Change to darker gray (#595959) for 7:1 ratio
   - Code: `color: #595959;` instead of `#999999`

2. Missing Form Labels
   - Issue: Email and password inputs have placeholder text but no <label>
   - WCAG: 1.3.1 Info and Relationships, 3.3.2 Labels or Instructions
   - Severity: CRITICAL
   - Impact: Screen readers can't identify input purpose
   - Reproduce: Remove placeholder, fields become unlabeled
   - Fix: Add visible labels or aria-label
   - Code:
     ```html
     <label for="email">Email Address</label>
     <input id="email" type="email" placeholder="you@example.com">
     ```

3. No Focus Indicator
   - Issue: Focus outline removed with `outline: none`
   - WCAG: 2.4.7 Focus Visible - Level AA
   - Severity: HIGH
   - Impact: Keyboard users can't see where focus is
   - Reproduce: Tab through form, no visual focus indication
   - Fix: Add custom focus style with 2px outline
   - Code:
     ```css
     input:focus, button:focus {
       outline: 2px solid #0066FF;
       outline-offset: 2px;
     }
     ```

4. Form Validation Errors Not Announced
   - Issue: Error messages appear visually but not announced to screen readers
   - WCAG: 3.3.1 Error Identification, 4.1.3 Status Messages
   - Severity: HIGH
   - Impact: Blind users don't know form submission failed
   - Reproduce: Submit invalid form, screen reader doesn't announce errors
   - Fix: Add aria-live region and aria-invalid on inputs
   - Code:
     ```html
     <div role="alert" aria-live="polite">
       Please enter a valid email address
     </div>
     <input aria-invalid="true" aria-describedby="email-error">
     ```

5. Button Has Generic Label
   - Issue: Submit button says "Submit" without context
   - WCAG: 2.4.6 Headings and Labels - Level AA
   - Severity: MEDIUM
   - Impact: Screen reader users hear "Submit" without knowing what it submits
   - Reproduce: Navigate with screen reader, button context unclear
   - Fix: Change to "Sign In" or add aria-label
   - Code: `<button>Sign In</button>` or `<button aria-label="Sign in to account">Submit</button>`

6. Not Keyboard Accessible
   - Issue: "Show password" is a <div> with onClick, not keyboard accessible
   - WCAG: 2.1.1 Keyboard - Level A
   - Severity: CRITICAL
   - Impact: Keyboard users can't toggle password visibility
   - Reproduce: Tab through form, can't reach show password control
   - Fix: Use <button> element or add tabindex and keyboard handler
   - Code:
     ```html
     <button type="button" aria-label="Show password" onclick="togglePassword()">
       👁
     </button>
     ```

7. No Skip Link
   - Issue: No "Skip to main content" link
   - WCAG: 2.4.1 Bypass Blocks - Level A
   - Severity: MEDIUM
   - Impact: Keyboard users must tab through entire header/nav
   - Reproduce: Tab from top, many focusable elements before form
   - Fix: Add visually hidden skip link at top
   - Code:
     ```html
     <a href="#main" class="skip-link">Skip to main content</a>
     <!-- CSS makes it visible only on focus -->
     ```

8. Images Missing Alt Text
   - Issue: Company logo has no alt attribute
   - WCAG: 1.1.1 Non-text Content - Level A
   - Severity: MEDIUM
   - Impact: Screen readers announce "image" without context
   - Reproduce: Screen reader reads "Image" for logo
   - Fix: Add alt="Company Name"
   - Code: `<img src="logo.png" alt="Acme Corp">`

Summary:
- Critical: 2 (missing labels, keyboard access)
- High: 3 (contrast, focus, errors)
- Medium: 3 (button label, skip link, alt text)
- Total: 8 issues

Testing Tools Used:
- axe DevTools: Caught 5/8 issues
- Keyboard navigation: Manual testing
- NVDA screen reader: Manual testing
- Contrast checker: WebAIM tool

Recommendations:
1. Fix critical issues immediately (labels, keyboard)
2. Add automated accessibility testing to CI (jest-axe, Cypress + axe)
3. Conduct screen reader testing for all new features
4. Train developers on WCAG basics
```

---

## Responsive Design

### 9. Responsive Layout Strategy

**Purpose:** Define responsive behavior for layouts.

**Prompt:**
```
Create a responsive layout strategy for [PAGE/COMPONENT]:

Layout context:
- Desktop design: [DESCRIPTION]
- Content types: [TEXT/IMAGES/FORMS/DATA/ETC]
- Priority content: [WHAT_MUST_BE_VISIBLE]
- Breakpoints: [MOBILE/TABLET/DESKTOP_RANGES]

Define for each breakpoint:
- Layout structure (grid, flex, stack)
- Content visibility (hide/show/collapse)
- Navigation pattern (how users navigate)
- Typography scale adjustments
- Image/media handling
- Interactive element sizing (touch targets)
- Performance considerations

Provide:
- Breakpoint-specific layouts
- CSS/media query strategy
- Content prioritization approach
- Loading strategy (progressive enhancement, mobile-first)
```

**Example:**
```
Responsive strategy for Blog Article Page:

Desktop Layout (1024px+):
```
┌─────────────────────────────────────────────┐
│ Header: Logo, Nav, Search                   │
├────────────┬────────────────────┬───────────┤
│            │                    │           │
│  Sidebar   │   Article Content  │  Related  │
│  (TOC)     │                    │  Articles │
│            │                    │           │
│  200px     │      60%           │   25%     │
└────────────┴────────────────────┴───────────┘
```

Content: Article title/meta, body, images, code blocks, related articles

Priority: Article content is primary, TOC helps navigation, related articles for engagement

Breakpoints:
- Mobile: 0-639px
- Tablet: 640-1023px
- Desktop: 1024px+
- Wide: 1280px+

Mobile (0-639px):
```
┌─────────────────┐
│  Header         │
│  (hamburger)    │
├─────────────────┤
│                 │
│  Article        │
│  Content        │
│  (full width)   │
│                 │
├─────────────────┤
│  Jump to Top    │
├─────────────────┤
│  Related        │
│  (carousel)     │
└─────────────────┘
```

Layout: Single column, stacked
Content:
- Hide: Desktop nav (→ hamburger menu), sidebar TOC (→ sticky button), right sidebar initially
- Show: Full-width article, hamburger menu, sticky "Jump to section" button
- Collapse: Header on scroll (show on scroll up)

Navigation:
- Hamburger menu for main nav
- Floating action button for TOC (opens overlay)
- Back to top button (appears after 50% scroll)

Typography:
- Title: 28px → 24px
- Body: 18px → 16px (readability on mobile)
- Line height: 1.6 → 1.5

Images:
- Full width (not fixed)
- Lazy loading for performance
- Responsive images (<picture> with srcset)

Touch Targets:
- Minimum 44x44px for all interactive elements
- Increased padding on buttons, links

Performance:
- Mobile-first CSS (base styles for mobile, @media for desktop)
- Defer non-critical CSS (related articles, comments)
- Prioritize above-the-fold content

CSS Example:
```css
/* Mobile-first base styles */
.article-layout {
  display: flex;
  flex-direction: column;
}

.article-sidebar,
.article-related {
  display: none; /* Hidden on mobile */
}

.article-content {
  padding: 1rem;
  font-size: 16px;
}

/* Tablet: 640px+ */
@media (min-width: 640px) {
  .article-content {
    padding: 2rem;
    font-size: 18px;
  }

  .article-related {
    display: block; /* Show related articles */
    margin-top: 2rem;
  }
}

/* Desktop: 1024px+ */
@media (min-width: 1024px) {
  .article-layout {
    display: grid;
    grid-template-columns: 200px 1fr 300px;
    gap: 2rem;
  }

  .article-sidebar {
    display: block; /* Show TOC */
    position: sticky;
    top: 2rem;
  }

  .article-content {
    font-size: 18px;
    max-width: 65ch; /* Optimal reading width */
  }
}
```

Tablet (640-1023px):
```
┌──────────────────────────────┐
│  Header (full nav)           │
├──────────────────────────────┤
│                              │
│   Article Content            │
│   (centered, max-width)      │
│                              │
├──────────────────────────────┤
│   Related Articles (grid)    │
└──────────────────────────────┘
```

Layout: Single column, centered content
Content: Show nav, article, related; hide sidebar TOC (sticky button instead)
Typography: Between mobile and desktop (16-18px)

Desktop (1024px+):
Full 3-column layout as shown in header

Wide (1280px+):
Wider content area, margins increase

Content Prioritization:
1. Article content (always visible, full-width on mobile)
2. Navigation (hamburger on mobile, full on desktop)
3. Table of Contents (sticky button on mobile/tablet, sidebar on desktop)
4. Related articles (bottom on mobile, side on desktop)
5. Comments (lazy loaded on all devices)

Progressive Enhancement:
- Base: Readable article on any device
- Enhanced: TOC navigation, related articles
- Advanced: Sticky elements, advanced typography

Loading Strategy:
- Critical: Article content, header
- Deferred: Related articles, comments, analytics
- Lazy: Images below fold, author bio

Testing:
- Chrome DevTools responsive mode
- Real devices: iPhone, iPad, Android
- Slow 3G network throttling
```

---

### 10. Mobile-First Component Design

**Purpose:** Design component with mobile-first approach.

**Prompt:**
```
Design a mobile-first [COMPONENT]:

Component: [NAME and PURPOSE]

Mobile design (start here):
- Screen size: 320px-428px
- Layout: [STRUCTURE]
- Interactions: [TOUCH_GESTURES]
- Content: [WHAT_TO_SHOW]
- Performance: [LOADING_STRATEGY]

Then scale up to:
- Tablet (768px-1024px): [CHANGES]
- Desktop (1024px+): [ENHANCEMENTS]

For each size define:
- Visual changes
- Interaction changes
- Additional features
- Performance considerations

Follow mobile-first CSS approach (base styles are mobile, @media for larger screens).
```

**Example:**
```
Mobile-first Data Table Component:

Component: Responsive data table showing user list with actions

Mobile (320px-639px):

Design:
- Card-based layout (not traditional table)
- Each row becomes a card
- Stacked key fields (name, email, role)
- Expand/collapse for additional fields
- Swipe left on card reveals actions (Edit, Delete)
- 5 cards per page, pagination at bottom

Layout:
```
┌──────────────────────┐
│ [Avatar] John Doe    │
│          john@ex.com │
│          Role: Admin │
│ [ ⋯ More ]           │
└──────────────────────┘
```

Interactions:
- Tap card to expand full details
- Swipe left to reveal action buttons
- Pull to refresh list
- Long-press for multi-select mode
- Touch target: 44x44px minimum

Content Priority:
1. Name (most important)
2. Email
3. Role
4. Status (visible)
5. Created date (hidden, shown in expanded view)
6. Actions (swipe to reveal)

Performance:
- Virtualized scrolling for long lists
- Lazy load images (avatars)
- Infinite scroll or pagination (pagination easier on mobile)

CSS (Base styles):
```css
.data-table {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.data-row {
  background: white;
  border-radius: 8px;
  padding: 1rem;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.data-cell {
  display: block;
  margin-bottom: 0.5rem;
}

.data-cell-label {
  font-weight: 600;
  font-size: 0.75rem;
  color: #666;
  text-transform: uppercase;
}

.data-actions {
  /* Hidden, revealed on swipe */
  position: absolute;
  right: 0;
  transform: translateX(100%);
  transition: transform 0.3s;
}

.data-row.swiped .data-actions {
  transform: translateX(0);
}
```

Tablet (640px-1023px):

Design:
- Hybrid: Card layout but more compact
- 2-column grid of cards
- More info visible per card (no expand needed)
- Actions visible on hover (no swipe)

Changes from mobile:
```css
@media (min-width: 640px) {
  .data-table {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1.5rem;
  }

  .data-row {
    display: grid;
    grid-template-columns: 1fr auto;
  }

  .data-actions {
    position: static;
    transform: none;
    opacity: 0;
    transition: opacity 0.2s;
  }

  .data-row:hover .data-actions {
    opacity: 1;
  }
}
```

Additional features:
- Show more fields without expansion
- Hover actions instead of swipe
- Keyboard navigation (Tab, Enter)

Desktop (1024px+):

Design:
- Traditional table layout
- Fixed header with sortable columns
- Visible actions column
- Bulk actions (checkbox + toolbar)
- Density options (compact/comfortable/spacious)

Changes from tablet:
```css
@media (min-width: 1024px) {
  .data-table {
    display: table;
    width: 100%;
    border-collapse: collapse;
  }

  .data-header {
    display: table-header-group;
    position: sticky;
    top: 0;
    background: white;
    z-index: 10;
  }

  .data-row {
    display: table-row;
    border-bottom: 1px solid #e0e0e0;
  }

  .data-cell {
    display: table-cell;
    padding: 1rem;
    vertical-align: middle;
  }

  .data-actions {
    opacity: 0;
  }

  .data-row:hover .data-actions {
    opacity: 1;
  }

  /* Bulk actions toolbar */
  .bulk-actions {
    display: flex;
    gap: 0.5rem;
    padding: 1rem;
    background: #f5f5f5;
  }
}
```

Additional features:
- Column sorting (click header)
- Column resizing (drag edge)
- Column visibility toggle
- Bulk selection (shift-click for range)
- Keyboard shortcuts (⌘A select all, Delete for delete)
- Export to CSV
- Advanced filters sidebar

Enhancements:
- Hover states on rows
- Tooltips for truncated content
- Right-click context menu
- Persistent column width preferences

Wide Desktop (1280px+):
- More columns visible
- Side panel for details (instead of modal)
- Multi-pane layout option

Mobile-First Approach Benefits:
1. Forces content prioritization (what's essential?)
2. Better performance (load less by default)
3. Easier to enhance than simplify
4. Touch-first interactions work everywhere

Progressive Enhancement:
- Core: Data accessible as cards (works everywhere)
- Enhanced: Sorting, filtering (tablet+)
- Advanced: Bulk actions, keyboard shortcuts (desktop)

Testing:
- Test touch interactions on real devices
- Test keyboard navigation on desktop
- Ensure table is usable at 320px width
- Test with large datasets (1000+ rows)
```

---

## Visual Design

### 11. Design Mockup Specification

**Purpose:** Specify requirements for a design mockup.

**Prompt:**
```
Create a design mockup specification for [SCREEN/FEATURE]:

Context:
- Purpose: [WHAT_IT_DOES]
- User: [PERSONA]
- Brand: [STYLE_ATTRIBUTES]
- Inspirations: [REFERENCES]

Mockup requirements:
- Artboard size: [DIMENSIONS]
- Design tool: [FIGMA/SKETCH/ADOBE_XD]
- Fidelity: [LOW/HIGH]
- States to show: [STATES]
- Responsive variants: [MOBILE/TABLET/DESKTOP]
- Dark mode: [YES/NO]

Visual elements:
- Color palette: [COLORS]
- Typography: [FONTS]
- Iconography: [STYLE]
- Imagery: [PHOTO_STYLE/ILLUSTRATIONS]
- Spacing system: [GRID]
- Components to use: [EXISTING_COMPONENTS]

Deliverables:
- Main mockup
- Interaction states
- Developer handoff specs
- Assets export (icons, images)
```

**Example:**
```
Design mockup specification: Dashboard Analytics Page

Context:
- Purpose: Display key metrics and charts for business analytics
- User: Marketing manager, needs quick overview of performance
- Brand: Modern, professional, data-driven SaaS
- Inspirations: Stripe Dashboard, Mixpanel, clean data visualization

Mockup Requirements:

Artboard: 1440x900px (desktop), 375x812px (mobile)
Tool: Figma with auto-layout and components
Fidelity: High-fidelity (production-ready)
States: Default, loading (skeleton), empty state, error state
Variants: Desktop and mobile
Dark mode: Yes (both light and dark themes)

Visual Elements:

Color Palette:
- Background: #FFFFFF (light), #1A1A1A (dark)
- Surface: #F8F9FA (light), #2A2A2A (dark)
- Primary: #0066FF
- Success: #10B981 (positive metrics)
- Danger: #EF4444 (negative metrics)
- Text: #1A202C (light), #E5E5E5 (dark)
- Text secondary: #6B7280

Typography:
- Headings: Inter, 600 weight, 24px/20px/16px
- Body: Inter, 400 weight, 14px
- Numbers/metrics: Inter, 700 weight, 32px for big numbers
- Labels: Inter, 500 weight, 12px uppercase

Iconography:
- Style: Outline icons, 24x24px
- Library: Heroicons or Feather
- Usage: Navigation, metric indicators, empty states

Imagery:
- Charts: Clean line/bar/pie charts, not 3D
- Illustrations: For empty states (simple, 2-color)
- Brand colors in visualizations

Spacing System:
- 8px base unit
- 16px between cards
- 24px section spacing
- 32px page margins
- 12-column grid, 16px gutters

Components (from design system):
- Card component
- Button (primary, secondary)
- Date range picker
- Dropdown menu
- Tooltip
- Chart components (line, bar, donut)

Layout:

Desktop (1440x900):
```
┌───────────────────────────────────────────────────────┐
│  Sidebar Nav  │  Dashboard                           │
│               │  ┌──────────────────────────────────┐│
│  [Overview]   │  │ Date Range: [Last 7 days ▼]      ││
│   Metrics     │  └──────────────────────────────────┘│
│   Reports     │  ┌───────┐ ┌───────┐ ┌───────┐     │
│   Users       │  │ Card  │ │ Card  │ │ Card  │     │
│   Settings    │  │ $42.5k│ │ 1,234 │ │ 89%   │     │
│               │  └───────┘ └───────┘ └───────┘     │
│               │  ┌────────────────┐┌───────────────┐│
│               │  │ Revenue Chart  ││ Traffic Chart ││
│               │  │ [Line Chart]   ││ [Bar Chart]   ││
│               │  └────────────────┘└───────────────┘│
└───────────────────────────────────────────────────────┘
```

Mobile (375x812):
```
┌─────────────────┐
│  Header + Menu  │
├─────────────────┤
│Date: Last 7 days│
├─────────────────┤
│  ┌───────────┐  │
│  │   Card    │  │
│  │  $42.5k   │  │
│  └───────────┘  │
│  ┌───────────┐  │
│  │   Card    │  │
│  │   1,234   │  │
│  └───────────┘  │
│  ┌───────────┐  │
│  │ Rev Chart │  │
│  └───────────┘  │
└─────────────────┘
```

Metric Cards:
- Metric title (e.g., "Total Revenue")
- Big number ($42,567)
- Trend indicator: ↑ 12% vs last period (green if up, red if down)
- Mini sparkline chart (optional)
- Card shadow: subtle, 2px blur

Charts:
- Clean axis labels
- Grid lines (subtle)
- Tooltips on hover (show exact values)
- Legend if multiple data series
- Responsive to container size

States to Design:

1. Default (with data): As shown above
2. Loading: Skeleton screens (gray rectangles pulse)
3. Empty state: Illustration + "No data yet" + "Connect your data source" button
4. Error state: Error icon + message + "Try again" button
5. Mobile navigation: Hamburger menu expanded

Dark Mode:
- Invert colors (dark background, light text)
- Chart colors remain vibrant
- Reduce contrast slightly for comfort
- Shadows: Use lighter shadows or borders

Deliverables:

1. Main mockup (Figma file):
   - Desktop and mobile artboards
   - Light and dark mode
   - All states (default, loading, empty, error)
   - Organized layers and named properly

2. Interaction states:
   - Hover states for buttons, cards
   - Focus states for accessibility
   - Active/pressed states
   - Tooltip examples

3. Developer handoff (Figma Inspect):
   - CSS values export
   - Spacing measurements
   - Color hex codes
   - Font sizes and weights
   - Component variants documented

4. Assets export:
   - Icons (SVG, 24x24px)
   - Illustrations (SVG for empty state)
   - Logo (SVG, multiple sizes)
   - Favicon (PNG, 16x16, 32x32)

Annotations:
- Add notes for interactions ("Clicking card drills down to details")
- Indicate responsive behavior ("Stacks vertically on mobile")
- Specify animations ("Fade in 200ms on load")

Review Checklist:
- [ ] All text is readable (contrast ≥ 4.5:1)
- [ ] Touch targets are 44x44px minimum (mobile)
- [ ] Consistent spacing (8px multiples)
- [ ] Design system components used
- [ ] Dark mode variant complete
- [ ] All states designed
- [ ] Interactions documented
- [ ] Developer handoff ready
```

---

## Additional Resources

- **Related:** See [prompt-engineering-guide.md](./prompt-engineering-guide.md) for writing effective UI/UX prompts
- **Components:** See [coding-prompts.md](./coding-prompts.md) for implementing components
- **Testing:** See [testing-prompts.md](./testing-prompts.md) for accessibility and visual testing
- **Business:** See [business-prompts.md](./business-prompts.md) for user research and product requirements
