# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm start          # Start development server
npm run build      # Production build
npm test           # Run tests (Jest via react-scripts)
npm run deploy     # Build and deploy to GitHub Pages (runs predeploy/build first)
```

## Architecture

**Create React App** (React 18, no SSR). Single-page app with hash-based section navigation (`#about`, `#skills`, etc.) and smooth scrolling via `react-scroll`.

### Data Flow

All portfolio content lives in one file: `src/data/constants.js`. This exports `Bio`, `skills`, `experiences`, `education`, and `projects`. Every section component imports directly from here — updating this file is how you change the displayed content.

### Component Structure

`App.js` is the root orchestrator: it owns `darkMode` state (default `true`) and `openModal` state for the project details modal. It renders sections in order:

```
Navbar → HeroSection → Skills → Experience → Projects → Education → Contact → Footer
```

`ProjectDetails` is conditionally rendered as a floating modal when `openModal.state === true`.

### Styling Pattern

All components use **styled-components** with theme variables. The theme object is defined in `src/utils/Themes.js` (exports `darkTheme` and `lightTheme`) and provided via `ThemeProvider` in `App.js`. Access theme values inside styled-components with `${({ theme }) => theme.primary}` etc.

Responsive breakpoints are `768px` and `960px` throughout.

### Email Contact Form

`src/components/Contact/index.js` uses `@emailjs/browser`. The service ID, template ID, and public key are referenced directly — these need to be configured in an EmailJS account if the contact form is to work.

### Theme Colors

| Token | Dark | Light |
|---|---|---|
| `primary` | `#854CE6` | `#be1adb` |
| `bg` | `#1C1C27` | `#FFFFFF` |
| `text_primary` | `#F2F3F4` | `#111111` |
| `card` | `#171721` | `#FFFFFF` |
