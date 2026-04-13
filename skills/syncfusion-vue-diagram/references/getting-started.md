# Getting Started with Syncfusion Vue Diagram

## Table of Contents
- [Installation](#installation)
- [Project Setup](#project-setup)
- [CSS Imports](#css-imports)
- [Basic Usage](#basic-usage)
- [Module Injection](#module-injection)
- [Framework Integration](#framework-integration)

## Installation

The Syncfusion Vue Diagram component requires the `@syncfusion/ej2-vue-diagrams` package along with its dependencies.

### Required Dependencies

```javascript
|-- @syncfusion/ej2-vue-diagrams
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-navigations
    |-- @syncfusion/ej2-inputs
    |-- @syncfusion/ej2-popups
    |-- @syncfusion/ej2-buttons
    |-- @syncfusion/ej2-lists
    |-- @syncfusion/ej2-splitbuttons
    |-- @syncfusion/ej2-diagrams
    |-- @syncfusion/ej2-vue-base
```

### Install via npm

```bash
npm install @syncfusion/ej2-vue-diagrams --save
```

Or with Yarn:

```bash
yarn add @syncfusion/ej2-vue-diagrams
```

## Project Setup

```bash
npm create vite@latest my-diagram-app -- --template vue
cd my-diagram-app
npm install @syncfusion/ej2-vue-diagrams
npm run dev
```

## CSS Imports

Import Syncfusion diagram styles in your component or App.vue file. The necessity CSS styles need to be imported in the following order:

```vue
<style>
    @import "../node_modules/@syncfusion/ej2-base/styles/material.css";
    @import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";
    @import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
    @import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
    @import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
    @import "../node_modules/@syncfusion/ej2-vue-diagrams/styles/material.css";
</style>
```

> The order of importing CSS styles should be in line with its dependency graph.

Available themes:
- `material.css` (Default)
- `bootstrap.css` (Bootstrap theme)
- `bootstrap4.css` (Bootstrap 4 theme)
- `fabric.css` (Fabric UI)
- `highcontrast.css` (High contrast)

## Basic Usage

### Vue 2 with Options API

```vue
<template>
  <div>
    <ejs-diagram 
      id="diagram"
      :width="width"
      :height="height"
      :nodes="nodes"
    ></ejs-diagram>
  </div>
</template>

<script>
import { DiagramComponent as EjsDiagram } from '@syncfusion/ej2-vue-diagrams';

export default {
  components: {
    'ejs-diagram': EjsDiagram
  },
  data() {
    return {
      width: '100%',
      height: '590px',
      nodes: [
        {
          id: 'node1',
          width: 100,
          height: 100,
          offsetX: 250,
          offsetY: 250,
          style: { fill: '#6BA3D5' }
        }
      ]
    };
  }
};
</script>

<style>
@import '@syncfusion/ej2-vue-diagrams/styles/material.css';
</style>
```

### Vue 3 with <script setup>

```vue
<template>
  <div>
    <ejs-diagram 
      id="diagram"
      :width="width"
      :height="height"
      :nodes="nodes"
    ></ejs-diagram>
  </div>
</template>

<script setup>
import { DiagramComponent as EjsDiagram } from '@syncfusion/ej2-vue-diagrams';

const width = '100%';
const height = '590px';
const nodes = [
  {
    id: 'node1',
    width: 100,
    height: 100,
    offsetX: 250,
    offsetY: 250,
    style: { fill: '#6BA3D5' }
  }
];
</script>

<style>
@import '@syncfusion/ej2-vue-diagrams/styles/material.css';
</style>
```

## Module Injection

For advanced features like BPMN, UML, automatic layouts, and symbol palettes, inject the required modules into the diagram:

```javascript
// Vue 2 Options API
import { DiagramComponent, BpmnDiagrams, Inject } from '@syncfusion/ej2-vue-diagrams';

export default {
  components: {
    'ejs-diagram': DiagramComponent,
    'ejs-inject': Inject
  }
};
```

```vue
<!-- Vue 3 <script setup> -->
<template>
  <ejs-diagram id="diagram" :width="width" :height="height">
    <ejs-inject :services="[BpmnDiagrams, SymbolPalette, DataBinding]"></ejs-inject>
  </ejs-diagram>
</template>

<script setup>
import { DiagramComponent as EjsDiagram, BpmnDiagrams, SymbolPalette, DataBinding, Inject } from '@syncfusion/ej2-vue-diagrams';

const width = '100%';
const height = '590px';
</script>
```

Available services to inject:
- `BpmnDiagrams` - BPMN shape support
- `UmlDiagrams` - UML diagram support
- `SymbolPalette` - Symbol palette component
- `DataBinding` - Data binding support
- `HierarchicalTree` - Hierarchical layout
- `OrganizationalChart` - Org chart layout
- `ComplexHierarchicalTree` - Complex hierarchical layout
- `RadialTree` - Radial tree layout
- `MindMap` - Mind map layout
- `FlowchartLayout` - Flowchart layout

## Framework Integration Notes

- **Vue 2**: Use `$refs` for accessing diagram instance methods
- **Vue 3**: Use template refs with `<script setup>`
- **Next.js**: Use dynamic imports and disable SSR
- **Preact**: Components work similarly to Vue but use preact-specific imports

For framework-specific issues, refer to the main SKILL.md navigation guide.
