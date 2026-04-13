# Features and Configuration in Vue BlockEditor

## Table of Contents
- [Overview](#overview)
- [Drag and Drop](#drag-and-drop)
  - [Enable Drag and Drop](#enable-drag-and-drop)
  - [Drag Handle Configuration](#drag-handle-configuration)
- [Paste Cleanup](#paste-cleanup)
  - [PasteCleanupSettings](#pastecleanupsettings)
  - [Allowed Styles](#allowed-styles)
  - [Denied Tags](#denied-tags)
  - [Keep Format Options](#keep-format-options)
  - [Plain Text Mode](#plain-text-mode)
- [Undo Redo](#undo-redo)
  - [UndoRedoStack Configuration](#undoredostack-configuration)
  - [Stack Limit](#stack-limit)
- [Keyboard Configuration](#keyboard-configuration)
  - [KeyConfig Customization](#keyconfig-customization)
  - [Custom Shortcuts](#custom-shortcuts)
- [Read-Only Mode](#read-only-mode)
- [Persistence](#persistence)
  - [EnablePersistence](#enablepersistence)
- [Styling Configuration](#styling-configuration)
  - [CssClass](#cssclass)
  - [Height and Width](#height-and-width)
- [Complete Examples](#complete-examples)

## Overview

The BlockEditor provides extensive configuration options for drag-and-drop, paste cleanup, undo/redo functionality, keyboard shortcuts, read-only mode, state persistence, and custom styling. These features enable you to customize the editor to match your application requirements.

## Drag and Drop

### Enable Drag and Drop

Enable dragging and dropping of blocks:

```vue
<template>
  <div>
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :enableDragAndDrop="true"
      :height="500"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [{ text: 'Drag this block', type: 'Text' }]
  },
  {
    id: 'block2',
    type: 'Paragraph',
    content: [{ text: 'Drop it here', type: 'Text' }]
  },
  {
    id: 'block3',
    type: 'Paragraph',
    content: [{ text: 'Or here', type: 'Text' }]
  }
]);
</script>
```

### Drag Handle Configuration

Configure drag handle with block action menu:

```vue
<template>
  <div>
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :enableDragAndDrop="true"
      :blockActionMenuSettings="blockActionMenuSettings"
      :height="500"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);

const blockActionMenuSettings = ref({
  enable: true,
  items: ['DragHandle', 'Delete', 'Duplicate', 'MoveUp', 'MoveDown'],
  position: 'left'
});

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [{ text: 'Hover to see drag handle', type: 'Text' }]
  },
  {
    id: 'block2',
    type: 'Paragraph',
    content: [{ text: 'Drag using the handle', type: 'Text' }]
  }
]);
</script>
```

## Paste Cleanup

### PasteCleanupSettings

Configure how pasted content is cleaned:

```vue
<template>
  <div>
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :pasteCleanupSettings="pasteCleanupSettings"
      :height="500"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);

const pasteCleanupSettings = ref({
  keepFormat: true,
  deniedTags: ['script', 'style', 'iframe'],
  allowedStyles: ['color', 'font-weight', 'font-style', 'text-decoration'],
  deniedAttrs: ['class', 'id', 'onclick'],
  plainText: false
});

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [
      {
        text: 'Paste formatted content here to see cleanup in action',
        type: 'Text'
      }
    ]
  }
]);
</script>
```

### Allowed Styles

Specify which inline styles are allowed when pasting:

```vue
<template>
  <div>
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :pasteCleanupSettings="pasteCleanupSettings"
      :height="500"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);

const pasteCleanupSettings = ref({
  keepFormat: true,
  allowedStyles: [
    'color',
    'background-color',
    'font-weight',
    'font-style',
    'text-decoration',
    'font-size',
    'font-family'
  ]
});

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [
      {
        text: 'Paste content with allowed styles',
        type: 'Text'
      }
    ]
  }
]);
</script>
```

### Denied Tags

Specify which HTML tags should be removed when pasting:

```vue
<template>
  <div>
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :pasteCleanupSettings="pasteCleanupSettings"
      :height="500"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);

const pasteCleanupSettings = ref({
  keepFormat: true,
  deniedTags: [
    'script',
    'style',
    'iframe',
    'object',
    'embed',
    'applet',
    'meta',
    'link',
    'form',
    'input',
    'button'
  ],
  deniedAttrs: ['onclick', 'onload', 'onerror', 'class', 'id']
});

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [
      {
        text: 'Dangerous tags and attributes will be removed',
        type: 'Text'
      }
    ]
  }
]);
</script>
```

### Keep Format Options

Control whether formatting is preserved when pasting:

```vue
<template>
  <div>
    <button @click="toggleKeepFormat">
      {{ keepFormat ? 'Disable' : 'Enable' }} Keep Format
    </button>
    
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :pasteCleanupSettings="pasteCleanupSettings"
      :height="500"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);
const keepFormat = ref(true);

const pasteCleanupSettings = ref({
  keepFormat: true,
  allowedStyles: ['color', 'font-weight', 'font-style']
});

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [
      {
        text: 'Paste content to test keep format setting',
        type: 'Text'
      }
    ]
  }
]);

const toggleKeepFormat = () => {
  keepFormat.value = !keepFormat.value;
  pasteCleanupSettings.value.keepFormat = keepFormat.value;
};
</script>
```

### Plain Text Mode

Strip all formatting from pasted content:

```vue
<template>
  <div>
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :pasteCleanupSettings="pasteCleanupSettings"
      :height="500"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);

const pasteCleanupSettings = ref({
  plainText: true, // Strip all formatting
  keepFormat: false
});

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [
      {
        text: 'Pasted content will be plain text only',
        type: 'Text'
      }
    ]
  }
]);
</script>
```

## Undo Redo

### UndoRedoStack Configuration

Configure undo/redo functionality:

```vue
<template>
  <div>
    <button @click="handleUndo">Undo</button>
    <button @click="handleRedo">Redo</button>
    
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :undoRedoStack="undoRedoStack"
      :height="500"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);

const undoRedoStack = ref({
  enable: true,
  limit: 30
});

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [
      {
        text: 'Make changes and use undo/redo',
        type: 'Text'
      }
    ]
  }
]);

const handleUndo = () => {
  blockEditor.value.ej2Instances.executeToolbarAction('Undo');
};

const handleRedo = () => {
  blockEditor.value.ej2Instances.executeToolbarAction('Redo');
};
</script>
```

### Stack Limit

Configure the undo/redo stack limit:

```vue
<template>
  <div>
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :undoRedoStack="undoRedoStack"
      :height="500"
    />
    <p>Undo/Redo stack limit: {{ undoRedoStack.limit }} actions</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);

const undoRedoStack = ref({
  enable: true,
  limit: 50 // Store up to 50 undo states
});

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [
      {
        text: 'Extended undo/redo history',
        type: 'Text'
      }
    ]
  }
]);
</script>
```

## Keyboard Configuration

### KeyConfig Customization

Customize keyboard shortcuts:

```vue
<template>
  <div>
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :keyConfig="keyConfig"
      :height="500"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);

const keyConfig = ref({
  'bold': 'ctrl+b',
  'italic': 'ctrl+i',
  'underline': 'ctrl+u',
  'undo': 'ctrl+z',
  'redo': 'ctrl+y',
  'save': 'ctrl+s',
  'selectAll': 'ctrl+a',
  'copy': 'ctrl+c',
  'cut': 'ctrl+x',
  'paste': 'ctrl+v'
});

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [
      {
        text: 'Use keyboard shortcuts: Ctrl+B (Bold), Ctrl+I (Italic), Ctrl+U (Underline)',
        type: 'Text'
      }
    ]
  }
]);
</script>
```

### Custom Shortcuts

Add custom keyboard shortcuts:

```vue
<template>
  <div>
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :keyConfig="keyConfig"
      :height="500"
    />
    <p>Custom shortcuts: Ctrl+Shift+D (Duplicate), Ctrl+Shift+Delete (Clear formatting)</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);

const keyConfig = ref({
  'bold': 'ctrl+b',
  'italic': 'ctrl+i',
  'underline': 'ctrl+u',
  'strikethrough': 'ctrl+shift+s',
  'duplicate': 'ctrl+shift+d',
  'clearFormat': 'ctrl+shift+delete',
  'heading1': 'ctrl+alt+1',
  'heading2': 'ctrl+alt+2',
  'heading3': 'ctrl+alt+3',
  'bulletList': 'ctrl+shift+l',
  'numberedList': 'ctrl+shift+n'
});

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [
      {
        text: 'Try custom shortcuts like Ctrl+Alt+1 for Heading 1',
        type: 'Text'
      }
    ]
  }
]);
</script>
```

## Read-Only Mode

Enable read-only mode to prevent editing:

```vue
<template>
  <div>
    <button @click="toggleReadOnly">
      {{ isReadOnly ? 'Enable' : 'Disable' }} Editing
    </button>
    
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :readOnly="isReadOnly"
      :height="500"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);
const isReadOnly = ref(false);

const editorValue = ref([
  {
    id: 'block1',
    type: 'Heading1',
    content: [{ text: 'Read-Only Mode Demo', type: 'Text' }]
  },
  {
    id: 'block2',
    type: 'Paragraph',
    content: [
      {
        text: 'Toggle the button to enable/disable editing',
        type: 'Text'
      }
    ]
  }
]);

const toggleReadOnly = () => {
  isReadOnly.value = !isReadOnly.value;
};
</script>
```

## Persistence

### EnablePersistence

Persist editor state across page reloads:

```vue
<template>
  <div>
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :enablePersistence="true"
      id="persistentEditor"
      :height="500"
    />
    <p>Your changes will be saved in localStorage</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [
      {
        text: 'This content persists across page reloads',
        type: 'Text'
      }
    ]
  }
]);
</script>
```

## Styling Configuration

### CssClass

Add custom CSS classes to the editor:

```vue
<template>
  <div>
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      cssClass="custom-editor dark-theme"
      :height="500"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [
      {
        text: 'Custom styled editor',
        type: 'Text'
      }
    ]
  }
]);
</script>

<style>
.custom-editor.dark-theme {
  background-color: #1e1e1e;
  color: #d4d4d4;
}

.custom-editor.dark-theme .e-block-editor-content {
  background-color: #2d2d2d;
  color: #d4d4d4;
}
</style>
```

### Height and Width

Configure editor dimensions:

```vue
<template>
  <div>
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :height="600"
      :width="800"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);

const editorValue = ref([
  {
    id: 'block1',
    type: 'Paragraph',
    content: [
      {
        text: 'Editor with custom dimensions: 800px wide, 600px tall',
        type: 'Text'
      }
    ]
  }
]);
</script>
```

## Complete Examples

### Comprehensive Configuration Example

A complete example with all major features configured:

```vue
<template>
  <div class="editor-container">
    <h2>Fully Configured BlockEditor</h2>
    
    <div class="controls">
      <button @click="toggleReadOnly">
        {{ isReadOnly ? 'Enable' : 'Disable' }} Editing
      </button>
      <button @click="toggleDragDrop">
        {{ dragEnabled ? 'Disable' : 'Enable' }} Drag & Drop
      </button>
      <button @click="handleUndo">Undo</button>
      <button @click="handleRedo">Redo</button>
      <button @click="exportData">Export JSON</button>
    </div>
    
    <ejs-blockeditor
      ref="blockEditor"
      :value="editorValue"
      :height="600"
      :width="'100%'"
      :enableDragAndDrop="dragEnabled"
      :enablePersistence="true"
      :readOnly="isReadOnly"
      cssClass="custom-blockeditor"
      id="configuredEditor"
      :pasteCleanupSettings="pasteCleanupSettings"
      :undoRedoStack="undoRedoStack"
      :keyConfig="keyConfig"
      :blockActionMenuSettings="blockActionMenuSettings"
      :inlineToolbarSettings="inlineToolbarSettings"
      :commandMenuSettings="commandMenuSettings"
      :imageBlockSettings="imageBlockSettings"
      :codeBlockSettings="codeBlockSettings"
    />
    
    <div class="info">
      <h3>Configuration Summary:</h3>
      <ul>
        <li>Drag & Drop: {{ dragEnabled ? 'Enabled' : 'Disabled' }}</li>
        <li>Read-Only: {{ isReadOnly ? 'Yes' : 'No' }}</li>
        <li>Persistence: Enabled</li>
        <li>Undo/Redo Stack: {{ undoRedoStack.limit }} levels</li>
        <li>Paste Cleanup: Configured</li>
        <li>Custom Keyboard Shortcuts: Configured</li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { BlockEditorComponent as EjsBlockeditor } from '@syncfusion/ej2-vue-blockeditor';

const blockEditor = ref(null);
const isReadOnly = ref(false);
const dragEnabled = ref(true);

const pasteCleanupSettings = ref({
  keepFormat: true,
  deniedTags: ['script', 'style', 'iframe', 'object'],
  allowedStyles: ['color', 'font-weight', 'font-style', 'text-decoration', 'background-color'],
  deniedAttrs: ['onclick', 'onload', 'onerror'],
  plainText: false
});

const undoRedoStack = ref({
  enable: true,
  limit: 30
});

const keyConfig = ref({
  'bold': 'ctrl+b',
  'italic': 'ctrl+i',
  'underline': 'ctrl+u',
  'strikethrough': 'ctrl+shift+s',
  'undo': 'ctrl+z',
  'redo': 'ctrl+y',
  'save': 'ctrl+s',
  'heading1': 'ctrl+alt+1',
  'heading2': 'ctrl+alt+2',
  'heading3': 'ctrl+alt+3'
});

const blockActionMenuSettings = ref({
  enable: true,
  items: ['DragHandle', 'Delete', 'Duplicate', 'MoveUp', 'MoveDown', 'TurnInto'],
  position: 'left',
  showTooltip: true
});

const inlineToolbarSettings = ref({
  enable: true,
  items: [
    'Bold',
    'Italic',
    'Underline',
    'Strikethrough',
    'FontColor',
    'BackgroundColor',
    'Link',
    'InlineCode',
    'ClearFormat'
  ]
});

const commandMenuSettings = ref({
  enable: true,
  trigger: '/',
  items: [
    'Paragraph',
    'Heading1',
    'Heading2',
    'Heading3',
    'BulletList',
    'NumberedList',
    'Checklist',
    'Code',
    'Quote',
    'Divider',
    'Table',
    'Image'
  ]
});

const imageBlockSettings = ref({
  saveUrl: 'https://api.example.com/upload',
  path: '/images/',
  maxFileSize: 5000000,
  allowedTypes: ['.jpg', '.jpeg', '.png', '.gif'],
  resize: true
});

const codeBlockSettings = ref({
  languages: [
    { name: 'JavaScript', value: 'javascript' },
    { name: 'TypeScript', value: 'typescript' },
    { name: 'Python', value: 'python' },
    { name: 'HTML', value: 'html' },
    { name: 'CSS', value: 'css' }
  ],
  defaultLanguage: 'javascript'
});

const editorValue = ref([
  {
    id: 'block1',
    type: 'Heading1',
    content: [{ text: 'Fully Configured Editor', type: 'Text' }]
  },
  {
    id: 'block2',
    type: 'Paragraph',
    content: [
      {
        text: 'This editor demonstrates all major configuration options including:',
        type: 'Text'
      }
    ]
  },
  {
    id: 'block3',
    type: 'BulletList',
    content: [{ text: 'Drag and drop functionality', type: 'Text' }]
  },
  {
    id: 'block4',
    type: 'BulletList',
    content: [{ text: 'Paste cleanup with custom rules', type: 'Text' }]
  },
  {
    id: 'block5',
    type: 'BulletList',
    content: [{ text: 'Undo/redo with 30-level history', type: 'Text' }]
  },
  {
    id: 'block6',
    type: 'BulletList',
    content: [{ text: 'Custom keyboard shortcuts', type: 'Text' }]
  },
  {
    id: 'block7',
    type: 'BulletList',
    content: [{ text: 'State persistence', type: 'Text' }]
  },
  {
    id: 'block8',
    type: 'BulletList',
    content: [{ text: 'Read-only mode toggle', type: 'Text' }]
  }
]);

const toggleReadOnly = () => {
  isReadOnly.value = !isReadOnly.value;
};

const toggleDragDrop = () => {
  dragEnabled.value = !dragEnabled.value;
};

const handleUndo = () => {
  blockEditor.value.ej2Instances.executeToolbarAction('Undo');
};

const handleRedo = () => {
  blockEditor.value.ej2Instances.executeToolbarAction('Redo');
};

const exportData = () => {
  const json = blockEditor.value.ej2Instances.getDataAsJson();
  console.log('Exported JSON:', json);
  alert('Check console for exported data');
};
</script>

<style scoped>
.editor-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.controls {
  margin-bottom: 20px;
}

.controls button {
  margin-right: 10px;
  padding: 8px 16px;
  cursor: pointer;
}

.custom-blockeditor {
  border: 2px solid #ddd;
  border-radius: 8px;
}

.info {
  margin-top: 20px;
  padding: 15px;
  background-color: #f5f5f5;
  border-radius: 4px;
}

.info h3 {
  margin-top: 0;
}

.info ul {
  margin: 0;
  padding-left: 20px;
}
</style>
```

This comprehensive guide covers all major features and configuration options in the Vue BlockEditor using the Composition API.
