# Changelog

All notable changes to this project will be documented in this file.

## [1.6.1-beta.1] - 2025-05-09

### 🔄 Changed
- Improved GTM implementation to work seamlessly in all scenarios:
  - Standard GTM initialization for regular page loads
  - Virtual pageview tracking for View Transitions
  - Added page title to virtual pageview data
  - Improved error handling

### 🧪 Testing Needed
Please test this beta release thoroughly, especially:
1. Regular page navigation (without View Transitions)
2. Page navigation with View Transitions enabled
3. Virtual pageview tracking in GTM
4. Page titles in GTM events

## [1.6.1-beta.0] - 2025-05-09

### 🧪 Beta Release
This is a beta release that needs thorough testing before being promoted to a stable release.

### 🔄 Changed
- **[Universal Compatibility]** Enhanced GTM implementation to work with both View Transitions and regular navigation:
  - Standard GTM initialization for regular page loads
  - Automatic View Transitions detection and support
  - Smart script injection to prevent duplicates
  - Virtual pageview tracking for View Transitions
  - Improved error handling

### 🧪 Testing Needed
Please test this beta release thoroughly, especially:
1. Regular page navigation (without View Transitions)
2. Page navigation with View Transitions enabled
3. DataLayer event tracking in both modes
4. Virtual pageview tracking during View Transitions
5. GTM Debug mode in both navigation types

### 📝 Notes
- This is a beta release addressing View Transitions compatibility
- Report any issues on GitHub
- Test in both development and production environments

## [1.6.0] - Previous Release
- Previous stable release
