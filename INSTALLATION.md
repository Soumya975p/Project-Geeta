# Project Geeta - Installation Guide

This document contains step-by-step instructions to set up and run the Project Geeta (Bhagavad Gita) web application.

## Prerequisites

Before starting, ensure you have the following installed on your system:

1. **Node.js** (v18 or higher) - [Download here](https://nodejs.org/)
2. **npm** (comes with Node.js) or **yarn** package manager
3. **Git** (optional, for version control)

## Step-by-Step Installation Process

### Step 1: Verify Node.js Installation

Open your terminal (PowerShell on Windows) and check if Node.js is installed:

```bash
node --version
npm --version
```

You should see version numbers (e.g., v18.x.x or higher).

### Step 2: Navigate to Project Directory

```bash
cd "C:\Users\ASUS\Desktop\ZeTheta\Project Geeta\copilot"
```

Or navigate to wherever you've cloned/downloaded the project.

### Step 3: Install Project Dependencies

Run the following command to install all required packages:

```bash
npm install
```

This will install:
- **Svelte 4.2.0** - Frontend framework
- **Vite 5.0.0** - Build tool and dev server
- **@sveltejs/vite-plugin-svelte 3.0.0** - Svelte plugin for Vite
- **axios 1.6.0** - HTTP client for API requests

### Step 4: Verify Public Assets

Ensure the following folders and files exist in the `public` directory:

```
public/
  ├── css/
  │   ├── bootstrap.css (Bootstrap 4.0.0)
  │   ├── font-awesome.css (Font Awesome 4.7.0)
  │   └── sanskrit.css (Custom styles)
  └── images/
      ├── gita_banner.png
      ├── pic1.jpg
      ├── gita_book.jpg
      ├── gita_open.png
      ├── scroll_bg.png
      ├── play_button.png
      ├── footerimg.png
      ├── footer_logo.png
      └── logo.png
```

### Step 5: Start Development Server

Run the development server:

```bash
npm run dev
```

You should see output similar to:
```
  VITE v5.0.0  ready in XXX ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h to show help
```

### Step 6: Open in Browser

Open your web browser and navigate to:
```
http://localhost:5173/
```

The application should now be running!

## Additional Build Commands

### Build for Production

To create an optimized production build:

```bash
npm run build
```

This creates a `dist` folder with production-ready files.

### Preview Production Build

To preview the production build locally:

```bash
npm run preview
```

## Included Libraries & Frameworks

This project uses the following technologies:

### Core Framework
- **Svelte 4.2.0** - Reactive UI framework
- **Vite 5.4.21** - Fast build tool and dev server

### CSS Frameworks
- **Bootstrap 4.0.0** - CSS framework for responsive design
  - Loaded via: `/public/css/bootstrap.css`
  - Documentation: https://getbootstrap.com/docs/4.0/

### Icon Libraries
- **Font Awesome 4.7.0** - Icon toolkit
  - Loaded via CDN in `index.html`
  - CDN: https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css

### Custom Fonts
- **Edensor** - Display font for headings
- **Lato** - Body text font
- **Noto Sans Devanagari** - Sanskrit text font
- Loaded via Google Fonts CDN

### HTTP Client
- **Axios 1.6.0** - Promise-based HTTP client
  - Used for future API integrations

### Custom Styling
- **sanskrit.css** - Custom CSS for Gita-specific styling
  - Located in `/public/css/sanskrit.css`

## Project Structure

```
copilot/
├── public/               # Static assets
│   ├── css/             # Stylesheets
│   └── images/          # Image assets
├── src/
│   ├── lib/             # Svelte components
│   │   ├── Header.svelte
│   │   ├── Footer.svelte
│   │   ├── GitaPage.svelte
│   │   ├── VerseGrid.svelte
│   │   └── AudioPopup.svelte
│   ├── App.svelte       # Root component
│   ├── main.js          # Entry point
│   └── app.css          # Global styles
├── index.html           # HTML entry point
├── package.json         # Dependencies
├── vite.config.js       # Vite configuration
└── svelte.config.js     # Svelte configuration
```

## Troubleshooting

### Port Already in Use

If port 5173 is already in use, Vite will automatically try the next available port (5174, 5175, etc.).

### CSS Not Loading

If styles don't appear:
1. Check that all CSS files exist in `public/css/`
2. Verify `@import` statements in `src/app.css`
3. Clear browser cache and hard reload (Ctrl+Shift+R)

### Images Not Loading

If images don't appear:
1. Ensure images exist in `public/images/`
2. Use paths starting with `/images/` (not `/public/images/`)
3. Check browser console for 404 errors

### Font Awesome Icons Not Showing

If icons don't appear:
1. Check internet connection (Font Awesome loads from CDN)
2. Verify CDN link in `index.html`
3. Check browser console for network errors

## Notes

- **No Tailwind CSS**: This project uses Bootstrap 4.0.0, not Tailwind CSS
- **No jQuery**: Modern Svelte replaces jQuery functionality
- **Development Port**: Default is 5173 (may vary if port is in use)
- **Hot Module Replacement**: Vite provides instant updates during development

## Getting Help

If you encounter issues:
1. Check the browser console for errors (F12)
2. Check the terminal for build errors
3. Verify all dependencies installed correctly: `npm list`
4. Try deleting `node_modules` and reinstalling: `rm -rf node_modules && npm install`

## License

This project is for educational purposes related to the Bhagavad Gita.

---

**Last Updated**: December 4, 2025
