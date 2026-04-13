# Getting Started with Vue BlockEditor

This guide covers the complete setup process for the Syncfusion Vue BlockEditor component in a Vue 3 project with Vite and Composition API.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Project Setup with Vite](#project-setup-with-vite)
- [Package Installation](#package-installation)
- [CSS Theme Configuration](#css-theme-configuration)
- [Component Registration](#component-registration)
- [Basic Implementation](#basic-implementation)
- [First Render Example](#first-render-example)
- [Running the Application](#running-the-application)
- [Troubleshooting](#troubleshooting)

## Prerequisites

Before starting, ensure you have:

- **Node.js** (v14.0 or higher) and npm/yarn installed
- Basic understanding of **Vue 3** and Composition API
- Familiarity with **Vite** build tool

**System Requirements:** Check [Syncfusion Vue System Requirements](https://ej2.syncfusion.com/vue/documentation/system-requirements)

## Project Setup with Vite

### Create a New Vite Project

Use Vite to scaffold a new Vue 3 project:

```bash
npm create vite@latest my-blockeditor-app
```

or with yarn:

```bash
yarn create vite my-blockeditor-app
```

### Configure Project Options

When prompted, select the following:

1. **Project name:** `my-blockeditor-app` (or your preferred name)
2. **Framework:** Select **Vue**
3. **Variant:** Select **JavaScript** (or TypeScript if preferred)

### Install Dependencies

Navigate to the project directory and install dependencies:

```bash
cd my-blockeditor-app
npm install
```

or with yarn:

```bash
cd my-blockeditor-app
yarn install
```

## Package Installation

Install the Syncfusion Vue BlockEditor package:

```bash
npm install @syncfusion/ej2-vue-blockeditor --save
```

or with yarn:

```bash
yarn add @syncfusion/ej2-vue-blockeditor
```

**Package Contents:**
- Core BlockEditor component
- All dependencies (ej2-base, ej2-popups, ej2-buttons, etc.)
- TypeScript definitions
- CSS themes

## CSS Theme Configuration

The BlockEditor requires CSS imports for the component and its dependencies. Syncfusion provides multiple built-in themes:

- **Material** - Google Material Design
- **Bootstrap** - Bootstrap 5 theme
- **Fabric** - Microsoft Fabric theme
- **Fluent** - Microsoft Fluent Design
- **Tailwind** - Tailwind CSS theme
- **Material 3** - Material Design 3

### Import CSS in Component

Add CSS imports to your component's `<style>` section (recommended approach):

```vue
<style>
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-blockeditor/styles/material.css';
</style>
```

### Alternative: Global CSS Import

Or import in `src/main.js` for global availability:

```javascript
import { createApp } from 'vue';
import App from './App.vue';

// Import Syncfusion CSS
import '@syncfusion/ej2-base/styles/material.css';
import '@syncfusion/ej2-popups/styles/material.css';
import '@syncfusion/ej2-buttons/styles/material.css';
import '@syncfusion/ej2-splitbuttons/styles/material.css';
import '@syncfusion/ej2-navigations/styles/material.css';
import '@syncfusion/ej2-dropdowns/styles/material.css';
import '@syncfusion/ej2-inputs/styles/material.css';
import '@syncfusion/ej2-blockeditor/styles/material.css';

createApp(App).mount('#app');
```

### Using Different Themes

To use a different theme, replace `material` with your preferred theme name:

```vue
<style>
@import '../node_modules/@syncfusion/ej2-base/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-blockeditor/styles/bootstrap5.css';
</style>
```

## Component Registration

### Composition API Registration (Recommended)

Register the BlockEditor component using Vue 3 Composition API with `<script setup>`:

```vue
<script setup>
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';
</script>
```

**Key Points:**
- Use `<script setup>` for cleaner syntax
- Import as `EjsBlockeditor` for template usage
- No need for explicit component registration in `<script setup>`

### Options API Registration (Alternative)

If using Options API:

```vue
<script>
import { BlockEditorComponent } from '@syncfusion/ej2-vue-blockeditor';

export default {
  name: 'App',
  components: {
    'ejs-blockeditor': BlockEditorComponent
  }
};
</script>
```

## Basic Implementation

### Minimal BlockEditor Setup

Create a basic BlockEditor with default configuration:

```vue
<template>
  <div class="app-container">
    <ejs-blockeditor id="blockeditor" />
  </div>
</template>

<script setup>
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';
</script>

<style>
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-blockeditor/styles/material.css';

.app-container {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
}
</style>
```

## First Render Example

### Complete Working Example

Create a functional BlockEditor with initial content:

```vue
<template>
  <div class="editor-container">
    <h1>Vue BlockEditor Demo</h1>
    <ejs-blockeditor 
      ref="blockEditor"
      :blocks="blocks"
      :height="'500px'"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor, ContentType } from '@syncfusion/ej2-vue-blockeditor';

// Reference to BlockEditor instance
const blockEditor = ref(null);

// Initial blocks data
const blocks = [
  {
    id: 'heading-block',
    blockType: 'Heading',
    properties: { level: 1 },
    content: [
      {
        id: 'heading-content',
        contentType: ContentType.Text,
        content: 'Welcome to BlockEditor'
      }
    ]
  },
  {
    id: 'intro-block',
    blockType: 'Paragraph',
    content: [
      {
        id: 'intro-content',
        contentType: ContentType.Text,
        content: 'The BlockEditor enables users to create, format, and organize content using various block types. Type / to see available commands.'
      }
    ]
  },
  {
    id: 'list-block',
    blockType: 'BulletList',
    content: [
      {
        contentType: ContentType.Text,
        content: 'Drag blocks to reorder'
      }
    ]
  },
  {
    id: 'list-block-2',
    blockType: 'BulletList',
    content: [
      {
        contentType: ContentType.Text,
        content: 'Type / for slash commands'
      }
    ]
  },
  {
    id: 'list-block-3',
    blockType: 'BulletList',
    content: [
      {
        contentType: ContentType.Text,
        content: 'Select text for inline formatting'
      }
    ]
  }
];
</script>

<style>
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-blockeditor/styles/material.css';

.editor-container {
  padding: 40px;
  max-width: 1000px;
  margin: 0 auto;
  background: #f5f5f5;
  min-height: 100vh;
}

.editor-container h1 {
  margin-bottom: 20px;
  color: #333;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>
```

## Running the Application

### Development Mode

Start the development server:

```bash
npm run dev
```

or with yarn:

```bash
yarn dev
```

The application will be available at `http://localhost:5173` (default Vite port).

### Production Build

Build the application for production:

```bash
npm run build
```

Preview the production build:

```bash
npm run preview
```

## Troubleshooting

### Common Issues and Solutions

#### Issue 1: CSS Not Loading

**Symptoms:** BlockEditor appears unstyled or broken.

**Solutions:**
- Verify all CSS imports are present and in correct order
- Check that `node_modules` path is correct in imports
- Ensure all dependency packages are installed
- Try importing CSS in `main.js` instead of component

#### Issue 2: Component Not Rendering

**Symptoms:** BlockEditor doesn't appear on page.

**Solutions:**
- Verify component is properly imported and registered
- Check browser console for errors
- Ensure `ejs-blockeditor` tag name matches registration
- Add explicit `height` prop to make editor visible

```vue
<ejs-blockeditor :height="'600px'" />
```

#### Issue 3: TypeScript Errors

**Symptoms:** Type errors with ContentType or BlockType.

**Solutions:**
- Import enums explicitly:
```typescript
import { ContentType, BlockType } from '@syncfusion/ej2-vue-blockeditor';
```

#### Issue 4: Build Errors

**Symptoms:** Build fails with module resolution errors.

**Solutions:**
- Clear `node_modules` and reinstall:
```bash
rm -rf node_modules package-lock.json
npm install
```

- Update Vite configuration if needed in `vite.config.js`:
```javascript
export default {
  optimizeDeps: {
    include: ['@syncfusion/ej2-vue-blockeditor']
  }
};
```

## Next Steps

1. **Explore Block Types** - Learn about all 14 available block types in `block-types.md`
2. **Inline Content** - Understand content formatting in `inline-content.md`
3. **Configure Menus** - Customize interactive menus in `editor-menus.md`
4. **Add Event Handlers** - Implement reactive behaviors in `events-lifecycle.md`
5. **Export Data** - Learn data export methods in `methods-api.md`

## Quick Reference

### Package Name
```bash
@syncfusion/ej2-vue-blockeditor
```

### Component Tag
```vue
<ejs-blockeditor />
```

### Import Statement
```javascript
import { BlockEditorComponent as EjsBlockeditor, ContentType } from '@syncfusion/ej2-vue-blockeditor';
```

### Minimum CSS Requirements
```css
@import '@syncfusion/ej2-base/styles/material.css';
@import '@syncfusion/ej2-blockeditor/styles/material.css';
/* + 6 other dependency CSS files */
```

---

**Ready to build?** Start with this getting-started guide, then explore block types and features in the other reference documents.
