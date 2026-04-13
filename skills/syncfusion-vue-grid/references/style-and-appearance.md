# Style and Appearance

## Table of Contents
- [When to Use](#when-to-use)
- [Theme Selection](#theme-selection)
- [CSS Styling](#css-styling)
- [Cell Styling](#cell-styling)
- [Row Styling](#row-styling)
- [Header Styling](#header-styling)
- [Paging Styling](#paging-styling)
- [Sorting Styling](#sorting-styling)
- [Filtering Styling](#filtering-styling)
- [Grouping Styling](#grouping-styling)
- [Toolbar Styling](#toolbar-styling)
- [Editing Styling](#editing-styling)
- [Aggregate Styling](#aggregate-styling)
- [Selection Styling](#selection-styling)
- [Responsive Design](#responsive-design)
- [Dark Mode](#dark-mode)

## When to Use

Use this reference when you need to:
- Select and apply themes (Material, Bootstrap, Fluent, Tailwind)
- Customize cell and row styling
- Style headers, paging, filtering, and other grid elements
- Implement responsive design
- Configure dark mode
- Apply custom CSS classes and styling

## Theme Selection

### Built-in Themes

Available: Material3 | Bootstrap5 | Tailwind | HighContrast | Fluent | Material

Import theme CSS and apply via grid configuration:

```vue
<script setup>
import '@syncfusion/ej2-vue-grids/styles/material3.css'; // or bootstrap5, tailwind, etc.
</script>

<template>
  <ejs-grid :dataSource="data">
    <e-columns>
      <e-column field="OrderID" width="100"></e-column>
      <e-column field="CustomerID" width="120"></e-column>
    </e-columns>
  </ejs-grid>
</template>
```

## CSS Styling

### Override Default Styles

Inspect generated HTML using browser DevTools to identify CSS classes. Use `.e-grid` root class and specific element classes:

```css
/* Root grid styling */
.e-grid { font-family: cursive; }
.my-grid .e-gridcontent { background-color: #f5f5f5; }

/* Header customization */
.e-grid .e-headercell {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white; font-weight: 600; padding: 12px;
}

/* Row hover and selection */
.e-grid .e-row:hover .e-rowcell { background-color: rgb(204, 229, 255); }
.e-grid .e-rowcell.e-selectionbackground { background-color: rgb(230, 230, 250); }
.e-grid .e-row.e-altrow { background-color: rgb(150, 212, 212); }
```

## Cell Styling

### Conditional Cell Styling

Use `queryCellInfo` callback to apply classes based on cell data:

```vue
<template>
  <ejs-grid :dataSource="data" :queryCellInfo="handleQueryCellInfo">
    <e-columns>
      <e-column field="Status" width="100"></e-column>
      <e-column field="Freight" width="100"></e-column>
    </e-columns>
  </ejs-grid>
</template>

<script setup>
const handleQueryCellInfo = (args) => {
  if (args.column.field === 'Status' && args.data.Status === 'Completed')
    args.cell.classList.add('status-completed');
  if (args.column.field === 'Freight' && args.data.Freight > 100)
    args.cell.classList.add('high-value');
};
</script>

<style>
.status-completed { background-color: #d4edda; color: #155724; font-weight: bold; }
.status-pending { background-color: #fff3cd; color: #856404; font-weight: bold; }
.high-value { background-color: #ffe6e6; color: #c00; }
</style>
```

## Row Styling

### Alternating Rows & Conditional Styling

```css
/* Alternating row colors */
.e-grid tbody tr:nth-child(odd) { background-color: #f9f9f9; }
.e-grid tbody tr:nth-child(even) { background-color: #ffffff; }
.e-grid tbody tr:hover { background-color: #e8f4f8; cursor: pointer; }
```

For conditional row styling, use `queryRowInfo` callback:

```javascript
const handleQueryRowInfo = (args) => {
  if (args.data.Status === 'Completed') args.row.classList.add('row-completed');
  if (args.data.Priority === 'High') args.row.classList.add('row-high-priority');
};
```

```css
.row-completed { background-color: #d4edda; }
.row-high-priority { background-color: #ffe6e6; font-weight: bold; }
```

## Header Styling

```css
/* Grid header container */
.e-gridheader { border-bottom: 2px solid #d0d0d0; background-color: #f5f5f5; }

/* Header cells */
.e-gridheader .e-headercell {
  background-color: #f8f9fa; color: #333333; font-weight: 600; padding: 12px 8px;
}
.e-gridheader .e-headercell:hover { background-color: #f0f2f5; }
.e-gridheader .e-headercelldiv { font-weight: 600; font-size: 14px; color: #1a1a1a; padding: 8px; }
```

## Paging Styling

```css
.e-gridpager { background-color: #f8f9fa; border-top: 2px solid #e8e8e8; padding: 12px 16px; }

/* Navigation buttons */
.e-gridpager .e-prevpage, .e-gridpager .e-nextpage, .e-gridpager .e-firstpage, .e-gridpager .e-lastpage {
  background-color: #ffffff; color: #495057; border: 1px solid #dee2e6; padding: 6px 12px; margin: 0 2px; border-radius: 4px; cursor: pointer; transition: all 0.2s ease;
}

.e-gridpager .e-prevpagedisabled, .e-gridpager .e-nextpagedisabled, .e-gridpager .e-firstpagedisabled, .e-gridpager .e-lastpagedisabled {
  background-color: #f5f5f5; color: #ccc; border: 1px solid #e0e0e0; cursor: not-allowed; padding: 6px 12px; margin: 0 2px;
}

/* Numeric pagination */
.e-gridpager .e-numericitem { background-color: #ffffff; color: #495057; border: 1px solid #dee2e6; padding: 6px 12px; margin: 0 2px; cursor: pointer; border-radius: 4px; font-weight: 500; }
.e-gridpager .e-numericitem:hover { background-color: #e3f2fd; border-color: #3f51b5; color: #3f51b5; }
.e-gridpager .e-currentitem { background-color: #3f51b5; color: #ffffff; border: 1px solid #3f51b5; padding: 6px 12px; margin: 0 2px; border-radius: 4px; font-weight: 600; }
```

## Sorting Styling

```css
.e-icon-ascending::before { content: '\e7a3'; color: #00a4ef; font-size: 14px; font-weight: 600; }
.e-icon-descending::before { content: '\e7b6'; color: #ff6b6b; font-size: 14px; font-weight: 600; }
.e-sortnumber {
  background-color: #ff8a65; color: #ffffff; border-radius: 50%; font-weight: 700; font-size: 11px;
  min-width: 20px; height: 20px; display: flex; align-items: center; justify-content: center; margin-left: 4px;
}
```

## Filtering Styling

```css
/* Filter bar cell */
.e-filterbarcell { background-color: #f5f7fa; border-bottom: 2px solid #e0e0e0; }

/* Filter input */
.e-filterbarcell .e-input-group input.e-input { padding: 8px 12px; border: 1px solid #cbd5e0; border-radius: 4px; font-size: 14px; font-family: cursive; }
.e-filterbarcell .e-input-group.e-input-focus input.e-input { border-color: #3f51b5; box-shadow: 0 0 0 3px rgba(63, 81, 181, 0.1); }

/* Filter icons */
.e-filterbarcell .e-clear-icon::before { content: '\e71d'; color: #999999; }
.e-filterbarcell .e-clear-icon:hover::before { color: #ff6b6b; }
.e-icon-filter::before { content: '\e7c8'; color: #3f51b5; }

/* Filter popup dialog */
.e-filter-popup .e-dlg-content, .e-filter-popup .e-footer-content { background-color: #deecf9; }
.e-filter-popup .e-footer-content { padding: 12px; border-top: 1px solid #e0e0e0; }
.e-filter-popup .e-btn { font-family: cursive; }
```

## Grouping Styling

```css
.e-groupdroparea { background: linear-gradient(135deg, #f5f7fa, #e8ecf1); border: 2px dashed #cbd5e0; padding: 12px 16px; border-radius: 6px; min-height: 60px; }

/* Group icons */
.e-icon-gdownarrow::before { content: '\e7c9'; color: #3f51b5; font-size: 14px; font-weight: 600; }
.e-icon-grightarrow::before { content: '\e80f'; color: #666666; font-size: 14px; }

/* Group caption and rows */
.e-groupcaption { background-color: #e8eef7; font-weight: 600; color: #2c3e50; border-bottom: 2px solid #d8d8d8; }
.e-grid .e-recordplusexpand, .e-grid .e-recordpluscollapse { background-color: #e8eef7; }
.e-indentcell { background-color: transparent; border-right: 2px solid #e8ecf1; }
```

## Toolbar Styling

```css
.e-toolbar { background: linear-gradient(to right, #f8f9fa, #f0f2f5); border-bottom: 3px solid #d8d8d8; padding: 10px; }
.e-toolbar-items { background-color: transparent; }

/* Toolbar buttons */
.e-toolbar .e-btn { background-color: #ffffff; color: #2c3e50; border: 1px solid #cbd5e0; padding: 8px 14px; margin: 2px 4px; border-radius: 4px; cursor: pointer; font-weight: 500; transition: all 0.2s ease; }
.e-toolbar .e-btn:hover { background-color: #f0f7ff; border-color: #3f51b5; color: #3f51b5; box-shadow: 0 2px 4px rgba(0,0,0,0.1); }
.e-toolbar .e-btn.e-active { background-color: #3f51b5; color: #ffffff; border-color: #3f51b5; }
```

## Editing Styling

```css
/* Edit row highlighting */
.e-editedrow table { background-color: #fffacd; border: 2px solid #ffd700; }
.e-addedrow table { background-color: #e0f7ff; border: 2px solid #00bfff; }

/* Edit form inputs */
.e-gridform .e-rowcell .e-input-group input.e-input { padding: 10px 12px; border: 2px solid #cbd5e0; border-radius: 4px; font-size: 14px; }
.e-gridform .e-rowcell .e-input-group.e-input-focus input.e-input { border-color: #3f51b5; box-shadow: inset 0 0 0 1px #3f51b5; }
.e-gridform .e-rowcell .e-float-input .e-field { padding: 12px; border-bottom: 2px solid #cbd5e0; font-size: 14px; }
.e-gridform .e-rowcell .e-float-input .e-field:focus { border-bottom-color: #3f51b5; }

/* Edit dialog */
.e-edit-dialog .e-dlg-header-content { background: linear-gradient(to right, #f8f9fa, #f0f2f5); border-bottom: 2px solid #d8d8d8; padding: 16px 20px; }

/* Toolbar action buttons */
.e-toolbar .e-btn.e-edit::before { color: #00a4ef; }
.e-toolbar .e-btn.e-delete::before { color: #f44336; }
.e-toolbar .e-btn.e-update::before { color: #4caf50; }
.e-grid .e-delete::before, .e-grid .e-cancel-icon::before { color: #f51717; }
```

## Aggregate Styling

```css
.e-gridfooter { background: linear-gradient(to bottom, #fafbfc, #f5f7fa); border-top: 3px solid #e0e0e0; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; }

.e-summaryrow { background-color: #f5f7fa; font-weight: 600; }
.e-summaryrow .e-summarycell { background-color: #f5f7fa; color: #2c3e50; font-weight: 600; padding: 10px 12px; border-right: 1px solid #e0e0e0; }
.e-summaryrow .e-summarycell:nth-child(even) { background-color: #eef0f5; }
```

## Selection Styling

```css
/* Row selection */
.e-selectionbackground { background-color: #cfe9ff; border-left: 4px solid #0078d4; }
.e-row.e-selectionbackground .e-rowcell { background-color: #cfe9ff; color: #000000; }
.e-row.e-selectionbackground:hover .e-rowcell { background-color: #a8d8ff; }

/* Cell and column selection */
.e-cellselectionbackground { background-color: #c8e6c9; border: 2px solid #25a125; }
.e-columnselection { background-color: #fff3cd; }
```

## Responsive Design & Dark Mode

### Responsive Grid
```css
@media (max-width: 800px) {
  .e-grid { font-size: 12px; }
  .e-grid .e-gridcontent { max-height: 300px; }
}
```

### Dark Mode
Apply dark theme by toggling a class and styling accordingly:

```css
.dark-mode .e-grid { background-color: #1e1e1e; color: #ffffff; }
.dark-mode .e-headercell { background-color: #2d2d2d; color: #ffffff; border-color: #444; }
.dark-mode .e-grid .e-row { border-color: #444; }
.dark-mode .e-grid tbody tr:hover { background-color: #3d3d3d; }
```

## Practical Example

```vue
<template>
  <div class="grid-container">
    <div class="controls">
      <button @click="toggleDarkMode">{{ isDarkMode ? 'Light' : 'Dark' }}</button>
    </div>
    <ejs-grid :dataSource="data" :class="{ 'dark-mode': isDarkMode }" :queryCellInfo="handleQueryCellInfo">
      <e-columns>
        <e-column field="OrderID" width="100"></e-column>
        <e-column field="Status" width="120"></e-column>
        <e-column field="Freight" format="C2" width="100"></e-column>
      </e-columns>
    </ejs-grid>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import '@syncfusion/ej2-vue-grids/styles/material3.css';

const isDarkMode = ref(false);

const toggleDarkMode = () => { isDarkMode.value = !isDarkMode.value; };
const handleQueryCellInfo = (args) => {
  if (args.data.Freight > 100) args.cell.classList.add('high-value');
};
</script>

<style>
.grid-container { padding: 20px; }
.controls { margin-bottom: 20px; display: flex; gap: 10px; }
.dark-mode .e-grid { background-color: #1e1e1e; color: #ffffff; }
.high-value { font-weight: bold; color: #ff0000; }
</style>
```
