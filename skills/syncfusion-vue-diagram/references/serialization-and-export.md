# Serialization and Export in Syncfusion Vue Diagram

## Table of Contents
- [Overview](#overview)
- [Diagram Serialization](#diagram-serialization)
- [Save and Load](#save-and-load)
- [Export to Image](#export-to-image)
- [Print Diagram](#print-diagram)
- [Visio Import](#visio-import)
- [EJ1 Migration](#ej1-migration)

## Overview

Serialization enables saving diagram state for later restoration. Export converts diagrams to image/document formats for sharing or documentation.

## Diagram Serialization

### Save Diagram

```javascript
var savedData = '';
const saveDiagramAsJSON = () => {
  savedData = diagram.saveDiagram();
  
  // Store in local storage or send to server
  localStorage.setItem('diagram-data', diagramData);
};
```

### Load Diagram

```javascript
const loadDiagramFromJSON = (savedData) => {
  if (savedData) {
    diagram.loadDiagram(savedData);
  }
};
```

### Save/Load diagram from local storage

```javascript
var saved = '';
// Save
const save = () => {
  saved = diagram.saveDiagram();
  // Store in local storage 
  localStorage.setItem('myDiagram', saved);
};

// Load
const load = () => {
  // Retrieve the saved string from local storage
  const savedData = localStorage.getItem('myDiagram');
  if (savedData) {
    diagram.loadDiagram(savedData);
  }
};
```

## Export

```vue
<template>
    <div id="app">
        <button v-on:click="export">Export</button>
        <ejs-diagram id="diagram" ref="diagramObj" :width="width" :height="height" :nodes="nodes"
            :snapSettings="snapSettings"></ejs-diagram>
    </div>
</template>

<script>
import { DiagramComponent, PrintAndExport } from '@syncfusion/ej2-vue-diagrams';

var diagramInstance;
var nodes = [
    {
        id: 'node1',
        width: 100,
        height: 50,
        offsetX: 100,
        offsetY: 100,
        style: { strokeColor: '#868686', fill: '#d5f5d5' },
        annotations: [{ content: 'Node 1' }],
    },
    {
        id: 'node2',
        width: 100,
        height: 75,
        offsetX: 100,
        offsetY: 225,
        shape: { type: 'Basic', shape: 'Diamond' },
        style: { strokeColor: '#8f908f', fill: '#e2f3fa' },
        annotations: [{ content: 'Node 2' }],
    },
];

export default {
    name: 'App',
    components: {
        'ejs-diagram': DiagramComponent,
    },
    data() {
        return {
            width: '1000px',
            height: '650px',
            nodes: nodes,
        };
    },
    methods: {
        export() {
          //By default exported in JPG format
          let exportOptions = {};
          diagramInstance.exportDiagram(exportOptions);
        }
    },
    mounted: function () {
        diagramInstance = this.$refs.diagramObj.ej2Instances;
    },
    provide: { diagram: [PrintAndExport] },
};
</script>
```

### Export as Image

```javascript
// Export as JPG
const exportJPG = () => {
  const exportOptions = { format: 'JPG', fileName: 'Export' };
  diagramInstance.exportDiagram(exportOptions);
};
// Export as PNG
const exportPNG = () => {
  const exportOptions = { format: 'PNG', fileName: 'Export' };
  diagramInstance.exportDiagram(exportOptions);
};
// Export as SVG
const exportSVG = () => {
  const exportOptions = { format: 'SVG', fileName: 'Export' };
  diagramInstance.exportDiagram(exportOptions);
};
```

### Export with Options

```javascript
const exportWithOptions = () => {
  let exportOptions = {
    format: 'PNG',
    fileName: 'my-diagram',
    region: 'Content',        // 'Content' | 'PageSettings'
    margin: { top: 20, left: 20, right: 20, bottom: 20 },
    multiplePage: true,
    pageOrientation: 'Portrait',   // 'Portrait' | 'Landscape'
  };
  diagramInstance.exportDiagram(exportOptions);
};
```

## Print Diagram

### Print Current Diagram

```vue
<template>
    <div id="app">
        <button v-on:click="print">Print</button>
        <ejs-diagram id="diagram" ref="diagramObj" :width="width" :height="height" :nodes="nodes"
            :snapSettings="snapSettings"></ejs-diagram>
    </div>
</template>

<script>
import { DiagramComponent, PrintAndExport } from '@syncfusion/ej2-vue-diagrams';

var diagramInstance;
var nodes = [
    {
        id: 'node1',
        width: 100,
        height: 50,
        offsetX: 100,
        offsetY: 100,
        style: { strokeColor: '#868686', fill: '#d5f5d5' },
        annotations: [{ content: 'Node 1' }],
    },
    {
        id: 'node2',
        width: 100,
        height: 75,
        offsetX: 100,
        offsetY: 225,
        shape: { type: 'Basic', shape: 'Diamond' },
        style: { strokeColor: '#8f908f', fill: '#e2f3fa' },
        annotations: [{ content: 'Node 2' }],
    },
];

export default {
    name: 'App',
    components: {
        'ejs-diagram': DiagramComponent,
    },
    data() {
        return {
            width: '1000px',
            height: '650px',
            nodes: nodes,
        };
    },
    methods: {
        print() {
          let printOptions = {};
          diagramInstance.print(printOptions);
        }
    },
    mounted: function () {
        diagramInstance = this.$refs.diagramObj.ej2Instances;
    },
    provide: { diagram: [PrintAndExport] },
};
</script>
```

### Print with Options

```javascript
const printWithOptions = () => {
  // Print with options
  let printOptions = {
    region: 'Content',
    margin: { top: 20, left: 20, right: 20, bottom: 20 },
    pageOrientation: 'Landscape',
    multiplePage: true        // Multi-page print
  };
  diagramInstance.print(printOptions);
};
```

## Visio Import

### Visio File Input and Export

```vue
<template>
    <div id="app">
        <input type="file" accept=".vsdx" @change="handleVisioImport" />
        <button v-on:click="exportVisio">Export</button>
        <ejs-diagram id="diagram" ref="diagramObj" :width="width" :height="height" :nodes="nodes" ></ejs-diagram>
    </div>
</template>

<script>
import { DiagramComponent, ImportAndExportVisio } from '@syncfusion/ej2-vue-diagrams';

var diagramInstance;
var nodes = [
    {
        id: 'node1',
        width: 100,
        height: 50,
        offsetX: 100,
        offsetY: 100,
        style: { strokeColor: '#868686', fill: '#d5f5d5' },
        annotations: [{ content: 'Node 1' }],
    },
    {
        id: 'node2',
        width: 100,
        height: 75,
        offsetX: 100,
        offsetY: 225,
        shape: { type: 'Basic', shape: 'Diamond' },
        style: { strokeColor: '#8f908f', fill: '#e2f3fa' },
        annotations: [{ content: 'Node 2' }],
    },
];

export default {
    name: 'App',
    components: {
        'ejs-diagram': DiagramComponent,
    },
    data() {
        return {
            width: '1000px',
            height: '650px',
            nodes: nodes,
        };
    },
    methods: {
      async handleVisioImport(event) {
        const file = event.target && event.target.files && event.target.files[0];
        if (!file) return;
          // Import the VSDX into the diagram
          await diagramInstance.importFromVisio(file);
          diagramInstance.width = '100%';
          diagramInstance.height = '700px';
          // Clear the input so the same file can be chosen again
          event.target.value = '';
      },
      exportVisio() {
        diagramInstance.exportToVisio();
      }
    },
    mounted: function () {
        diagramInstance = this.$refs.diagramObj.ej2Instances;
    },
    provide: { diagram: [ImportAndExportVisio] },
};
</script>
```

## EJ1 Migration

### Convert EJ1 Diagram to EJ2

When migrating from Syncfusion EJ1 diagrams to EJ2:
1. Import and inject the EJ1SerializationModule
2. Load the EJ1 JSON data using the diagram loadDiagram method and set the second parameter to true.

```vue
<template>
    <div id="app">
        <button v-on:click="loadEJ1">Load EJ1</button>
        <ejs-diagram id="diagram" ref="diagramObj" :width="width" :height="height" ></ejs-diagram>
    </div>
</template>

<script>
import { DiagramComponent, EJ1SerializationModule  } from '@syncfusion/ej2-vue-diagrams';

var diagramInstance;

export default {
    name: 'App',
    components: {
        'ejs-diagram': DiagramComponent,
    },
    data() {
        return {
            width: '1000px',
            height: '650px',
        };
    },
    methods: {
      loadEJ1() {
        let ej1Data = {"JSONData"};  //Replace JSONData with your EJ1 JSON data
        //Load the EJ1 JSON and pass a boolean value as true.
        diagramInstance.loadDiagram(ej1Data, true);
      }
    },
    mounted: function () {
        diagramInstance = this.$refs.diagramObj.ej2Instances;
    },
    provide: { diagram: [EJ1SerializationModule ] },
};
</script>

```

## Complete Export Example

```vue
<template>
  <div>
    <div style="margin-bottom: 10px;">
      <button v-on:click="save">Save Diagram</button>
      <button v-on:click="load">Load Diagram</button>
      <button v-on:click="exportPNG">Export as PNG</button>
      <button v-on:click="printDiagram">Print</button>
    </div>
    <ejs-diagram id="diagram" ref="diagramObj" :width="width" :height="height" :nodes="nodes" ></ejs-diagram>

  </div>
</template>


<script>
import { DiagramComponent, PrintAndExport  } from '@syncfusion/ej2-vue-diagrams';

var diagramInstance;
let saveData;
var nodes = [
  { id: 'node1', offsetX: 250, offsetY: 250, width: 100, height: 60 }
];
export default {
    name: 'App',
    components: {
        'ejs-diagram': DiagramComponent,
    },
    data() {
        return {
            width: '1000px',
            height: '650px',
            nodes: nodes,
        };
    },
    methods: {
      save() {
        saveData = diagramInstance.saveDiagram();
      },
      load() {
        if (saveData) {
          diagramInstance.loadDiagram(saveData);
        }
      },
      exportPNG() {
        const exportOptions = { format: 'PNG', fileName: 'Export' };
        diagramInstance.exportDiagram(exportOptions);
      },
      printDiagram() {
        let printOptions = { region: 'Content', pageOrientation: 'Landscape' };
        diagramInstance.print(printOptions);
      }
    },
    mounted: function () {
        diagramInstance = this.$refs.diagramObj.ej2Instances;
    },
    provide: { diagram: [PrintAndExport ] },
};
</script>
```

Serialization and export capabilities ensure diagrams are preserved, shared, and documented effectively across different formats and systems.
