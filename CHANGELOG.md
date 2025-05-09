# Changelog

All notable changes to this project will be documented in this file.

## [1.6.1-beta.0] - 2025-05-09

### 🧪 Beta Release
This is a beta release that needs thorough testing before being promoted to a stable release.

### 🔄 Changed
- **[View Transitions Support]** Enhanced GTM implementation to properly handle Astro View Transitions
  - Added proper dataLayer state preservation between page transitions
  - Improved GTM script reinitialization during navigation
  - Added error handling for script injection
  - Added `newPage` flag for better transition tracking

### 🧪 Testing Needed
Please test this beta release thoroughly, especially:
1. Page transitions with View Transitions enabled
2. DataLayer event persistence
3. GTM script reinitialization
4. Analytics tracking across page navigations

### 📝 Notes
- This is a beta release addressing View Transitions compatibility
- Report any issues on GitHub
- Test in both development and production environments

## [1.6.0] - Previous Release
- Previous stable release
