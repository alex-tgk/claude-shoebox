# Create Chrome Extension

Generate a complete, production-ready Chrome extension with Manifest V3, professional UI, monetization, and Chrome Web Store assets ready for submission.

## Instructions

You are tasked with creating a COMPLETE, production-ready Chrome extension. This is a one-shot command that must produce a fully functional, polished extension ready for Chrome Web Store submission and revenue generation.

### Step 1: Gather Requirements

First, ask the user these essential questions:
1. **Extension Purpose**: What does the extension do?
2. **Main Features**: What are the 3-5 key features?
3. **UI Type**: Popup, options page, side panel, or content scripts?
4. **Permissions Needed**: What Chrome APIs are needed? (storage, tabs, cookies, etc.)
5. **Target Websites**: Does it interact with specific websites?
6. **Monetization**: Free, freemium, one-time payment, or subscription?
7. **Data Storage**: Local storage, sync storage, or external API?

### Step 2: Complete Extension Structure

Create the following COMPLETE structure:

```
chrome-extension/
├── manifest.json
├── background/
│   └── service-worker.js
├── popup/
│   ├── popup.html
│   ├── popup.js
│   └── popup.css
├── options/
│   ├── options.html
│   ├── options.js
│   └── options.css
├── content/
│   ├── content.js
│   └── content.css
├── sidepanel/
│   ├── sidepanel.html
│   ├── sidepanel.js
│   └── sidepanel.css
├── lib/
│   ├── storage.js
│   ├── api.js
│   ├── analytics.js
│   └── utils.js
├── assets/
│   ├── icons/
│   │   ├── icon-16.png
│   │   ├── icon-32.png
│   │   ├── icon-48.png
│   │   └── icon-128.png
│   └── images/
├── store-assets/
│   ├── screenshots/
│   │   ├── screenshot-1.png (1280x800)
│   │   ├── screenshot-2.png
│   │   ├── screenshot-3.png
│   │   ├── screenshot-4.png
│   │   └── screenshot-5.png
│   ├── promotional/
│   │   ├── small-tile.png (440x280)
│   │   └── marquee.png (1400x560)
│   ├── description.md
│   └── privacy-policy.md
├── _locales/
│   ├── en/
│   │   └── messages.json
│   └── es/
│       └── messages.json
├── tests/
│   ├── unit/
│   └── e2e/
├── webpack.config.js
├── package.json
└── README.md
```

### Step 3: Manifest V3 Configuration

```json
// manifest.json
{
  "manifest_version": 3,
  "name": "Your Extension Name",
  "version": "1.0.0",
  "description": "Brief description of what your extension does (under 132 characters)",
  "author": "Your Name",
  "homepage_url": "https://yourextension.com",

  "icons": {
    "16": "assets/icons/icon-16.png",
    "32": "assets/icons/icon-32.png",
    "48": "assets/icons/icon-48.png",
    "128": "assets/icons/icon-128.png"
  },

  "action": {
    "default_popup": "popup/popup.html",
    "default_icon": {
      "16": "assets/icons/icon-16.png",
      "32": "assets/icons/icon-32.png"
    },
    "default_title": "Click to open"
  },

  "background": {
    "service_worker": "background/service-worker.js",
    "type": "module"
  },

  "content_scripts": [
    {
      "matches": ["<all_urls>"],
      "js": ["content/content.js"],
      "css": ["content/content.css"],
      "run_at": "document_idle"
    }
  ],

  "permissions": [
    "storage",
    "tabs",
    "activeTab",
    "scripting",
    "contextMenus",
    "alarms"
  ],

  "host_permissions": [
    "https://*/*"
  ],

  "optional_permissions": [
    "cookies",
    "history",
    "bookmarks"
  ],

  "options_page": "options/options.html",

  "side_panel": {
    "default_path": "sidepanel/sidepanel.html"
  },

  "content_security_policy": {
    "extension_pages": "script-src 'self'; object-src 'self'"
  },

  "web_accessible_resources": [
    {
      "resources": ["assets/images/*"],
      "matches": ["<all_urls>"]
    }
  ],

  "commands": {
    "_execute_action": {
      "suggested_key": {
        "default": "Ctrl+Shift+Y",
        "mac": "Command+Shift+Y"
      }
    },
    "toggle-feature": {
      "suggested_key": {
        "default": "Ctrl+Shift+F",
        "mac": "Command+Shift+F"
      },
      "description": "Toggle main feature"
    }
  },

  "default_locale": "en"
}
```

### Step 4: Background Service Worker

```javascript
// background/service-worker.js

// Extension installed/updated
chrome.runtime.onInstalled.addListener(async (details) => {
  if (details.reason === 'install') {
    // First install
    await initializeExtension();

    // Open welcome page
    chrome.tabs.create({
      url: 'https://yourextension.com/welcome'
    });

    // Track installation
    trackEvent('extension_installed', {
      version: chrome.runtime.getManifest().version
    });
  } else if (details.reason === 'update') {
    // Extension updated
    const previousVersion = details.previousVersion;
    const currentVersion = chrome.runtime.getManifest().version;

    // Show update notification
    chrome.notifications.create({
      type: 'basic',
      iconUrl: 'assets/icons/icon-128.png',
      title: 'Extension Updated',
      message: `Updated to version ${currentVersion}`,
      priority: 2
    });

    trackEvent('extension_updated', {
      from: previousVersion,
      to: currentVersion
    });
  }
});

// Initialize extension defaults
async function initializeExtension() {
  const defaults = {
    enabled: true,
    theme: 'light',
    notifications: true,
    autoStart: false,
    settings: {
      feature1: true,
      feature2: false,
      customValue: 10
    },
    stats: {
      usageCount: 0,
      lastUsed: null
    },
    premium: {
      isPremium: false,
      trialEndsAt: Date.now() + (7 * 24 * 60 * 60 * 1000) // 7 days
    }
  };

  await chrome.storage.sync.set(defaults);
}

// Listen for messages from content scripts and popup
chrome.runtime.onMessage.addListener((message, sender, sendResponse) => {
  console.log('Message received:', message);

  switch (message.type) {
    case 'GET_DATA':
      handleGetData(message.payload)
        .then(sendResponse)
        .catch(error => sendResponse({ error: error.message }));
      return true; // Keep channel open for async response

    case 'SAVE_DATA':
      handleSaveData(message.payload)
        .then(sendResponse)
        .catch(error => sendResponse({ error: error.message }));
      return true;

    case 'EXECUTE_FEATURE':
      executeFeature(sender.tab.id, message.payload)
        .then(sendResponse)
        .catch(error => sendResponse({ error: error.message }));
      return true;

    case 'CHECK_PREMIUM':
      checkPremiumStatus()
        .then(sendResponse)
        .catch(error => sendResponse({ error: error.message }));
      return true;

    default:
      sendResponse({ error: 'Unknown message type' });
  }
});

// Handle data retrieval
async function handleGetData(payload) {
  const data = await chrome.storage.sync.get(null);
  return { success: true, data };
}

// Handle data saving
async function handleSaveData(payload) {
  await chrome.storage.sync.set(payload);
  return { success: true };
}

// Execute main feature
async function executeFeature(tabId, options) {
  try {
    // Check if premium feature
    if (options.requiresPremium) {
      const { isPremium } = await checkPremiumStatus();
      if (!isPremium) {
        return {
          success: false,
          error: 'Premium feature - please upgrade'
        };
      }
    }

    // Execute content script
    const results = await chrome.scripting.executeScript({
      target: { tabId },
      func: featureFunction,
      args: [options]
    });

    // Update usage stats
    await updateStats();

    return {
      success: true,
      results: results[0].result
    };
  } catch (error) {
    console.error('Feature execution failed:', error);
    return {
      success: false,
      error: error.message
    };
  }
}

// Feature function to inject
function featureFunction(options) {
  // This runs in the page context
  console.log('Feature executing with options:', options);

  // Example: Highlight all links
  const links = document.querySelectorAll('a');
  links.forEach(link => {
    link.style.backgroundColor = options.color || 'yellow';
  });

  return { processed: links.length };
}

// Context menu
chrome.contextMenus.create({
  id: 'main-feature',
  title: 'Execute Feature',
  contexts: ['page', 'selection']
});

chrome.contextMenus.onClicked.addListener(async (info, tab) => {
  if (info.menuItemId === 'main-feature') {
    const result = await executeFeature(tab.id, {
      selectedText: info.selectionText
    });

    // Show notification
    chrome.notifications.create({
      type: 'basic',
      iconUrl: 'assets/icons/icon-128.png',
      title: 'Feature Executed',
      message: result.success ? 'Success!' : result.error
    });
  }
});

// Keyboard commands
chrome.commands.onCommand.addListener(async (command) => {
  if (command === 'toggle-feature') {
    const [tab] = await chrome.tabs.query({ active: true, currentWindow: true });
    await executeFeature(tab.id, {});
  }
});

// Alarms for periodic tasks
chrome.alarms.create('daily-sync', {
  periodInMinutes: 1440 // 24 hours
});

chrome.alarms.onAlarm.addListener(async (alarm) => {
  if (alarm.name === 'daily-sync') {
    await syncDataWithServer();
    await checkPremiumStatus();
  }
});

// Update usage statistics
async function updateStats() {
  const { stats } = await chrome.storage.sync.get('stats');
  stats.usageCount++;
  stats.lastUsed = new Date().toISOString();
  await chrome.storage.sync.set({ stats });
}

// Check premium status
async function checkPremiumStatus() {
  const { premium } = await chrome.storage.sync.get('premium');

  // Check if trial expired
  if (!premium.isPremium && Date.now() > premium.trialEndsAt) {
    return {
      isPremium: false,
      trialExpired: true,
      message: 'Trial expired - upgrade to continue'
    };
  }

  return {
    isPremium: premium.isPremium,
    trialExpired: false,
    daysLeft: Math.ceil((premium.trialEndsAt - Date.now()) / (24 * 60 * 60 * 1000))
  };
}

// Sync with server
async function syncDataWithServer() {
  try {
    const data = await chrome.storage.sync.get(null);

    const response = await fetch('https://api.yourextension.com/sync', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'X-Extension-Version': chrome.runtime.getManifest().version
      },
      body: JSON.stringify(data)
    });

    if (response.ok) {
      const serverData = await response.json();
      await chrome.storage.sync.set(serverData);
    }
  } catch (error) {
    console.error('Sync failed:', error);
  }
}

// Analytics tracking
function trackEvent(eventName, properties = {}) {
  // Send to your analytics service
  fetch('https://api.yourextension.com/analytics', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      event: eventName,
      properties: {
        ...properties,
        extensionVersion: chrome.runtime.getManifest().version,
        timestamp: new Date().toISOString()
      }
    })
  }).catch(console.error);
}
```

### Step 5: Popup UI

```html
<!-- popup/popup.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Extension Popup</title>
  <link rel="stylesheet" href="popup.css">
</head>
<body>
  <div class="container">
    <!-- Header -->
    <header class="header">
      <img src="../assets/icons/icon-48.png" alt="Logo" class="logo">
      <h1 class="title">Extension Name</h1>
      <button class="btn-icon" id="settingsBtn">
        <svg width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
          <path d="M10 6a2 2 0 110-4 2 2 0 010 4zM10 12a2 2 0 110-4 2 2 0 010 4zM10 18a2 2 0 110-4 2 2 0 010 4z"/>
        </svg>
      </button>
    </header>

    <!-- Status Banner -->
    <div class="status-banner" id="statusBanner">
      <div class="status-badge status-active">
        <span class="status-dot"></span>
        Active
      </div>
      <div class="premium-badge" id="premiumBadge">
        <span>⭐ Premium</span>
      </div>
    </div>

    <!-- Main Action -->
    <div class="main-action">
      <button class="btn btn-primary btn-large" id="mainActionBtn">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
          <path d="M8 5v14l11-7z"/>
        </svg>
        Execute Feature
      </button>
    </div>

    <!-- Stats -->
    <div class="stats-grid">
      <div class="stat-card">
        <div class="stat-value" id="usageCount">0</div>
        <div class="stat-label">Times Used</div>
      </div>
      <div class="stat-card">
        <div class="stat-value" id="daysLeft">7</div>
        <div class="stat-label">Trial Days</div>
      </div>
    </div>

    <!-- Quick Settings -->
    <div class="quick-settings">
      <h2 class="section-title">Quick Settings</h2>

      <div class="setting-item">
        <div class="setting-info">
          <div class="setting-name">Enable Feature 1</div>
          <div class="setting-desc">Description of feature 1</div>
        </div>
        <label class="toggle">
          <input type="checkbox" id="feature1Toggle">
          <span class="toggle-slider"></span>
        </label>
      </div>

      <div class="setting-item">
        <div class="setting-info">
          <div class="setting-name">Enable Feature 2</div>
          <div class="setting-desc">Description of feature 2</div>
        </div>
        <label class="toggle">
          <input type="checkbox" id="feature2Toggle">
          <span class="toggle-slider"></span>
        </label>
      </div>

      <div class="setting-item">
        <div class="setting-info">
          <div class="setting-name">Custom Value</div>
          <div class="setting-desc">Adjust the custom value</div>
        </div>
        <input type="range" id="customValueSlider" min="1" max="20" value="10" class="slider">
        <span id="customValueLabel">10</span>
      </div>
    </div>

    <!-- Upgrade CTA -->
    <div class="upgrade-section" id="upgradeSection">
      <div class="upgrade-card">
        <div class="upgrade-icon">⭐</div>
        <h3>Upgrade to Premium</h3>
        <p>Unlock all features and remove limitations</p>
        <ul class="feature-list">
          <li>✓ Unlimited usage</li>
          <li>✓ Advanced features</li>
          <li>✓ Priority support</li>
          <li>✓ No ads</li>
        </ul>
        <button class="btn btn-premium" id="upgradeBtn">
          Upgrade Now - $4.99
        </button>
      </div>
    </div>

    <!-- Footer -->
    <footer class="footer">
      <a href="#" id="helpLink">Help</a>
      <span>•</span>
      <a href="#" id="feedbackLink">Feedback</a>
      <span>•</span>
      <a href="#" id="rateLink">Rate Us</a>
    </footer>
  </div>

  <script src="popup.js"></script>
</body>
</html>
```

```css
/* popup/popup.css */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  width: 360px;
  min-height: 500px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 14px;
  color: #333;
  background: #f5f5f5;
}

.container {
  background: white;
}

/* Header */
.header {
  display: flex;
  align-items: center;
  padding: 16px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.logo {
  width: 32px;
  height: 32px;
  margin-right: 12px;
}

.title {
  flex: 1;
  font-size: 18px;
  font-weight: 600;
}

.btn-icon {
  background: rgba(255, 255, 255, 0.2);
  border: none;
  border-radius: 6px;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: white;
  transition: background 0.2s;
}

.btn-icon:hover {
  background: rgba(255, 255, 255, 0.3);
}

/* Status Banner */
.status-banner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 16px;
  background: #f8f9fa;
  border-bottom: 1px solid #e9ecef;
}

.status-badge {
  display: flex;
  align-items: center;
  font-size: 12px;
  font-weight: 500;
  padding: 4px 12px;
  border-radius: 12px;
  background: #d4edda;
  color: #155724;
}

.status-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #28a745;
  margin-right: 6px;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}

.premium-badge {
  font-size: 12px;
  font-weight: 600;
  color: #f39c12;
}

/* Main Action */
.main-action {
  padding: 24px 16px;
  text-align: center;
}

.btn {
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}

.btn-primary {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 12px 24px;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4);
}

.btn-large {
  width: 100%;
  padding: 16px;
  font-size: 16px;
}

/* Stats */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 12px;
  padding: 0 16px 24px;
}

.stat-card {
  background: #f8f9fa;
  padding: 16px;
  border-radius: 8px;
  text-align: center;
}

.stat-value {
  font-size: 28px;
  font-weight: 700;
  color: #667eea;
}

.stat-label {
  font-size: 12px;
  color: #6c757d;
  margin-top: 4px;
}

/* Quick Settings */
.quick-settings {
  padding: 0 16px 24px;
}

.section-title {
  font-size: 14px;
  font-weight: 600;
  margin-bottom: 16px;
  color: #495057;
}

.setting-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 0;
  border-bottom: 1px solid #e9ecef;
}

.setting-info {
  flex: 1;
}

.setting-name {
  font-weight: 500;
  margin-bottom: 4px;
}

.setting-desc {
  font-size: 12px;
  color: #6c757d;
}

/* Toggle Switch */
.toggle {
  position: relative;
  display: inline-block;
  width: 48px;
  height: 24px;
}

.toggle input {
  opacity: 0;
  width: 0;
  height: 0;
}

.toggle-slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  transition: 0.3s;
  border-radius: 24px;
}

.toggle-slider:before {
  position: absolute;
  content: "";
  height: 18px;
  width: 18px;
  left: 3px;
  bottom: 3px;
  background-color: white;
  transition: 0.3s;
  border-radius: 50%;
}

.toggle input:checked + .toggle-slider {
  background-color: #667eea;
}

.toggle input:checked + .toggle-slider:before {
  transform: translateX(24px);
}

/* Slider */
.slider {
  width: 100px;
  margin: 0 8px;
}

/* Upgrade Section */
.upgrade-section {
  padding: 16px;
  background: #f8f9fa;
}

.upgrade-card {
  background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
  color: white;
  padding: 24px;
  border-radius: 12px;
  text-align: center;
}

.upgrade-icon {
  font-size: 48px;
  margin-bottom: 12px;
}

.upgrade-card h3 {
  font-size: 20px;
  margin-bottom: 8px;
}

.upgrade-card p {
  opacity: 0.9;
  margin-bottom: 16px;
}

.feature-list {
  list-style: none;
  text-align: left;
  margin: 16px 0;
}

.feature-list li {
  padding: 6px 0;
  opacity: 0.95;
}

.btn-premium {
  background: white;
  color: #f5576c;
  padding: 12px 32px;
  font-size: 16px;
}

.btn-premium:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

/* Footer */
.footer {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 16px;
  font-size: 12px;
  color: #6c757d;
  background: #f8f9fa;
}

.footer a {
  color: #667eea;
  text-decoration: none;
}

.footer a:hover {
  text-decoration: underline;
}
```

```javascript
// popup/popup.js
document.addEventListener('DOMContentLoaded', async () => {
  // Load settings
  await loadSettings();

  // Setup event listeners
  setupEventListeners();

  // Check premium status
  await updatePremiumStatus();

  // Load stats
  await loadStats();
});

// Load settings from storage
async function loadSettings() {
  const data = await chrome.storage.sync.get([
    'settings',
    'stats',
    'premium'
  ]);

  // Update UI with settings
  if (data.settings) {
    document.getElementById('feature1Toggle').checked = data.settings.feature1;
    document.getElementById('feature2Toggle').checked = data.settings.feature2;
    document.getElementById('customValueSlider').value = data.settings.customValue;
    document.getElementById('customValueLabel').textContent = data.settings.customValue;
  }
}

// Setup event listeners
function setupEventListeners() {
  // Main action button
  document.getElementById('mainActionBtn').addEventListener('click', async () => {
    const btn = document.getElementById('mainActionBtn');
    btn.disabled = true;
    btn.textContent = 'Processing...';

    try {
      const response = await chrome.runtime.sendMessage({
        type: 'EXECUTE_FEATURE',
        payload: { requiresPremium: false }
      });

      if (response.success) {
        showNotification('Success!', 'Feature executed successfully');
        await loadStats(); // Refresh stats
      } else {
        showNotification('Error', response.error, 'error');
      }
    } catch (error) {
      showNotification('Error', error.message, 'error');
    } finally {
      btn.disabled = false;
      btn.innerHTML = `
        <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
          <path d="M8 5v14l11-7z"/>
        </svg>
        Execute Feature
      `;
    }
  });

  // Settings toggles
  document.getElementById('feature1Toggle').addEventListener('change', async (e) => {
    await saveSettings({ feature1: e.target.checked });
  });

  document.getElementById('feature2Toggle').addEventListener('change', async (e) => {
    await saveSettings({ feature2: e.target.checked });
  });

  document.getElementById('customValueSlider').addEventListener('input', (e) => {
    document.getElementById('customValueLabel').textContent = e.target.value;
  });

  document.getElementById('customValueSlider').addEventListener('change', async (e) => {
    await saveSettings({ customValue: parseInt(e.target.value) });
  });

  // Settings button
  document.getElementById('settingsBtn').addEventListener('click', () => {
    chrome.runtime.openOptionsPage();
  });

  // Upgrade button
  document.getElementById('upgradeBtn').addEventListener('click', () => {
    chrome.tabs.create({
      url: 'https://yourextension.com/upgrade'
    });
  });

  // Footer links
  document.getElementById('helpLink').addEventListener('click', (e) => {
    e.preventDefault();
    chrome.tabs.create({ url: 'https://yourextension.com/help' });
  });

  document.getElementById('feedbackLink').addEventListener('click', (e) => {
    e.preventDefault();
    chrome.tabs.create({ url: 'https://yourextension.com/feedback' });
  });

  document.getElementById('rateLink').addEventListener('click', (e) => {
    e.preventDefault();
    chrome.tabs.create({
      url: 'https://chrome.google.com/webstore/detail/your-extension-id'
    });
  });
}

// Save settings
async function saveSettings(newSettings) {
  const { settings } = await chrome.storage.sync.get('settings');
  const updated = { ...settings, ...newSettings };

  await chrome.storage.sync.set({ settings: updated });

  // Notify background script
  chrome.runtime.sendMessage({
    type: 'SETTINGS_CHANGED',
    payload: updated
  });
}

// Load stats
async function loadStats() {
  const { stats } = await chrome.storage.sync.get('stats');

  if (stats) {
    document.getElementById('usageCount').textContent = stats.usageCount;
  }
}

// Update premium status
async function updatePremiumStatus() {
  const response = await chrome.runtime.sendMessage({
    type: 'CHECK_PREMIUM'
  });

  const premiumBadge = document.getElementById('premiumBadge');
  const upgradeSection = document.getElementById('upgradeSection');
  const daysLeftEl = document.getElementById('daysLeft');

  if (response.isPremium) {
    premiumBadge.style.display = 'block';
    upgradeSection.style.display = 'none';
  } else {
    premiumBadge.style.display = 'none';
    upgradeSection.style.display = 'block';

    if (!response.trialExpired) {
      daysLeftEl.textContent = response.daysLeft;
    } else {
      daysLeftEl.textContent = '0';
      showNotification('Trial Expired', 'Upgrade to continue using premium features', 'warning');
    }
  }
}

// Show notification
function showNotification(title, message, type = 'success') {
  chrome.notifications.create({
    type: 'basic',
    iconUrl: '../assets/icons/icon-128.png',
    title,
    message,
    priority: 2
  });
}
```

### Step 6: Content Script

```javascript
// content/content.js

// Check if already injected
if (window.hasExtensionInjected) {
  console.log('Extension already injected');
} else {
  window.hasExtensionInjected = true;

  // Initialize
  init();
}

async function init() {
  // Get settings
  const { enabled, settings } = await chrome.storage.sync.get(['enabled', 'settings']);

  if (!enabled) return;

  // Add extension UI to page
  createExtensionUI();

  // Listen for messages
  chrome.runtime.onMessage.addListener((message, sender, sendResponse) => {
    if (message.type === 'EXECUTE_ON_PAGE') {
      executeFeature(message.payload);
      sendResponse({ success: true });
    }
  });
}

// Create floating UI
function createExtensionUI() {
  const container = document.createElement('div');
  container.id = 'extension-floating-ui';
  container.innerHTML = `
    <button class="extension-fab">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="white">
        <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/>
      </svg>
    </button>
    <div class="extension-menu">
      <div class="menu-item" data-action="feature1">Feature 1</div>
      <div class="menu-item" data-action="feature2">Feature 2</div>
      <div class="menu-item" data-action="feature3">Feature 3</div>
    </div>
  `;

  document.body.appendChild(container);

  // Event listeners
  const fab = container.querySelector('.extension-fab');
  const menu = container.querySelector('.extension-menu');

  fab.addEventListener('click', () => {
    menu.classList.toggle('open');
  });

  container.querySelectorAll('.menu-item').forEach(item => {
    item.addEventListener('click', () => {
      const action = item.dataset.action;
      executeFeature({ action });
      menu.classList.remove('open');
    });
  });
}

// Execute feature on page
function executeFeature(options) {
  console.log('Executing feature:', options);

  switch (options.action) {
    case 'feature1':
      // Implement feature 1
      highlightLinks();
      break;
    case 'feature2':
      // Implement feature 2
      extractEmails();
      break;
    case 'feature3':
      // Implement feature 3
      summarizePage();
      break;
  }
}

function highlightLinks() {
  const links = document.querySelectorAll('a');
  links.forEach(link => {
    link.style.backgroundColor = '#ffeb3b';
    link.style.padding = '2px 4px';
  });
}

function extractEmails() {
  const text = document.body.innerText;
  const emailRegex = /[\w.-]+@[\w.-]+\.\w+/g;
  const emails = text.match(emailRegex) || [];

  console.log('Emails found:', emails);

  // Show results
  alert(`Found ${emails.length} emails:\n${emails.join('\n')}`);
}

function summarizePage() {
  const headings = Array.from(document.querySelectorAll('h1, h2, h3'))
    .map(h => h.textContent.trim())
    .slice(0, 10);

  console.log('Page summary:', headings);
  alert(`Page headings:\n${headings.join('\n')}`);
}
```

### Step 7: Chrome Web Store Assets

```markdown
<!-- store-assets/description.md -->

# Extension Name

## Tagline
Brief, compelling one-liner (under 80 characters)

## Detailed Description

### What does it do?
[Extension Name] helps you [main benefit]. With just one click, you can [key action] and [result].

### Key Features:
✨ **Feature 1** - Description of feature 1
🚀 **Feature 2** - Description of feature 2
💡 **Feature 3** - Description of feature 3
⚡ **Feature 4** - Description of feature 4
🎯 **Feature 5** - Description of feature 5

### Why you'll love it:
- **Easy to Use** - Simple, intuitive interface
- **Fast & Reliable** - Instant results every time
- **Privacy First** - Your data stays on your device
- **Regular Updates** - Constantly improving

### Perfect for:
- Professionals who need to [use case]
- Students working on [use case]
- Anyone who wants to [use case]

### How it works:
1. Click the extension icon
2. Choose your settings
3. Click "Execute"
4. Done!

### Premium Features:
Upgrade to unlock:
- Unlimited usage
- Advanced features
- Priority support
- Remove all limitations

### Support:
Need help? Visit https://yourextension.com/support
Have feedback? Email support@yourextension.com

### Privacy:
We respect your privacy. Read our policy: https://yourextension.com/privacy
```

### Step 8: Analytics Integration

```javascript
// lib/analytics.js

const ANALYTICS_URL = 'https://api.yourextension.com/analytics';

class Analytics {
  constructor() {
    this.userId = null;
    this.sessionId = this.generateSessionId();
    this.init();
  }

  async init() {
    const { userId } = await chrome.storage.local.get('userId');

    if (!userId) {
      this.userId = this.generateUserId();
      await chrome.storage.local.set({ userId: this.userId });
    } else {
      this.userId = userId;
    }
  }

  generateUserId() {
    return 'user_' + Date.now() + '_' + Math.random().toString(36).substr(2, 9);
  }

  generateSessionId() {
    return 'session_' + Date.now() + '_' + Math.random().toString(36).substr(2, 9);
  }

  async track(eventName, properties = {}) {
    try {
      const payload = {
        event: eventName,
        userId: this.userId,
        sessionId: this.sessionId,
        properties: {
          ...properties,
          extensionVersion: chrome.runtime.getManifest().version,
          timestamp: new Date().toISOString(),
          url: window.location?.href
        }
      };

      await fetch(ANALYTICS_URL, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(payload)
      });
    } catch (error) {
      console.error('Analytics error:', error);
    }
  }

  // Convenience methods
  pageView(page) {
    this.track('page_view', { page });
  }

  buttonClick(button) {
    this.track('button_click', { button });
  }

  featureUse(feature, options = {}) {
    this.track('feature_use', { feature, ...options });
  }

  error(error, context = {}) {
    this.track('error', {
      message: error.message,
      stack: error.stack,
      ...context
    });
  }

  purchase(amount, product) {
    this.track('purchase', { amount, product });
  }
}

const analytics = new Analytics();
export default analytics;
```

### Step 9: Complete Documentation

```markdown
# Chrome Extension Documentation

## Overview
Production-ready Chrome extension with Manifest V3, monetization, and analytics.

## Features
✅ Manifest V3 compliant
✅ Background service worker
✅ Popup UI with settings
✅ Content scripts for page interaction
✅ Options page
✅ Context menus
✅ Keyboard shortcuts
✅ Analytics tracking
✅ Premium/freemium model
✅ Chrome Web Store ready

## Development

### Setup
\`\`\`bash
npm install
\`\`\`

### Build
\`\`\`bash
npm run build
\`\`\`

### Load Extension
1. Open Chrome
2. Go to chrome://extensions/
3. Enable "Developer mode"
4. Click "Load unpacked"
5. Select the extension directory

### Testing
\`\`\`bash
npm test
\`\`\`

## Publishing

### Prepare Assets
1. Create 1280x800 screenshots (5 images)
2. Create 440x280 small tile icon
3. Create 1400x560 marquee promo image
4. Write store description
5. Create privacy policy

### Submit to Chrome Web Store
1. Go to Chrome Web Store Developer Dashboard
2. Create new item ($5 one-time fee)
3. Upload extension ZIP
4. Upload store assets
5. Fill in description
6. Submit for review

### Review Process
- Typical review: 1-3 days
- Address any feedback
- Update and resubmit if needed

## Monetization

### Freemium Model
- Free: Basic features, 7-day trial
- Premium: $4.99, unlock all features

### Implementation
1. Check premium status in background script
2. Gate premium features
3. Show upgrade prompts
4. Process payments via Stripe/Paddle
5. Sync premium status across devices

## License
MIT
```

### Success Criteria

The command is successful when you deliver:
✅ Complete Chrome extension with Manifest V3
✅ Background service worker
✅ Professional popup UI
✅ Options page
✅ Content scripts
✅ Context menus and keyboard shortcuts
✅ Storage sync
✅ Analytics integration
✅ Premium/monetization setup
✅ Chrome Web Store assets (icons, screenshots, descriptions)
✅ Privacy policy
✅ Complete documentation
✅ Ready for Chrome Web Store submission

This should be a COMPLETE, PRODUCTION-READY Chrome extension ready for immediate submission and revenue generation.
