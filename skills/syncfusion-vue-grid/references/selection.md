# Selection

## Table of Contents
- [When to Use](#when-to-use)
- [Row Selection](#row-selection)
- [Cell Selection](#cell-selection)
- [Column Selection](#column-selection)
- [Checkbox Selection](#checkbox-selection)
- [Multi Select](#multi-select)
- [Keyboard Shortcuts](#keyboard-shortcuts)
- [Selection Events](#selection-events)

## When to Use

Use this reference when you need to:
- Enable row, cell, or column selection in grid
- Implement multi-select with checkboxes
- Configure keyboard shortcuts for selection
- Handle selection events
- Get selected rows/cells programmatically
- Customize selection appearance

## Row Selection

### Enable Row Selection
```vue
<template>
  <ejs-grid 
    :dataSource="data"
    :allowSelection="true"
    :selectionSettings="selectionSettings">
    <e-columns>
      <e-column field="OrderID" headerText="Order ID" width="100"></e-column>
      <e-column field="CustomerID" headerText="Customer ID" width="120"></e-column>
    </e-columns>
  </ejs-grid>
</template>

<script setup>
import { GridComponent as EjsGrid, ColumnDirective as EColumn, ColumnsDirective as EColumns, Selection } from "@syncfusion/ej2-vue-grids";
import { provide } from 'vue';

const selectionSettings = {
  type: 'Row',      // 'Row', 'Cell', 'Column'
  mode: 'Single'    // 'Single', 'Multiple'
};

provide('grid', [Selection]);
</script>
```

### Single Row Selection
```vue
<script setup>
const selectionSettings = {
  type: 'Row',
  mode: 'Single'
};
</script>
```

### Multiple Row Selection
```vue
<script setup>
const selectionSettings = {
  type: 'Row',
  mode: 'Multiple'
};
</script>
```

### Cell Selection Modes

Cell selection display can be customized using `cellSelectionMode`:

```javascript
const selectionSettings = {
  type: 'Cell',
  mode: 'Multiple',
  cellSelectionMode: 'Flow'  // 'Flow', 'Box', 'BoxWithBorder'
};
```

**Cell Selection Modes:**
- **`Flow`** - Continuous selection flowing through cells (default)
- **`Box`** - Rectangular box selection
- **`BoxWithBorder`** - Rectangular selection with visible border

### External Cell Selection
```javascript
// Select single cell by row and column index
gridInstance.selectCell({ rowIndex: 1, cellIndex: 2 });

// Select multiple cells
gridInstance.selectCells([
  { rowIndex: 0, cellIndex: 0 },
  { rowIndex: 1, cellIndex: 1 },
  { rowIndex: 2, cellIndex: 2 }
]);

// Select cell range
gridInstance.selectCellsByRange({ startRowIndex: 0, endRowIndex: 5, startCellIndex: 0, endCellIndex: 3 });

// Clear cell selection
gridInstance.clearCellSelection();
```

### Cell Selection Events
```vue
<template>
  <ejs-grid 
    :dataSource="data"
    :cellSelecting="handleCellSelecting"
    :cellSelected="handleCellSelected"
    :cellDeselected="handleCellDeselected">
    <!-- columns -->
  </ejs-grid>
</template>

<script setup>
const handleCellSelecting = (args) => {
  console.log('Cell selecting:', args.cellIndex, args.rowIndex);
};

const handleCellSelected = (args) => {
  console.log('Cell selected:', args.data);
};

const handleCellDeselected = (args) => {
  console.log('Cell deselected:', args.data);
};
</script>
```

## Column Selection

### Enable Column Selection
```vue
<script setup>
const selectionSettings = {
  type: 'Column',
  mode: 'Single',
  allowColumnSelection: true
};
</script>
```

### Multiple Column Selection
```vue
<script setup>
const selectionSettings = {
  type: 'Column',
  mode: 'Multiple',
  allowColumnSelection: true
};
</script>
```

### External Column Selection
```javascript
// Select single column by index
gridInstance.selectColumn(2);

// Select multiple columns
gridInstance.selectColumns([0, 2, 4]);

// Select column range
gridInstance.selectColumnsByRange(0, 4);

// Clear column selection
gridInstance.clearColumnSelection();
```

### Column Selection Events
```vue
<template>
  <ejs-grid 
    :dataSource="data"
    :columnSelecting="handleColumnSelecting"
    :columnSelected="handleColumnSelected"
    :columnDeselected="handleColumnDeselected">
    <!-- columns -->
  </ejs-grid>
</template>

<script setup>
const handleColumnSelecting = (args) => {
  console.log('Column selecting:', args.column);
};

const handleColumnSelected = (args) => {
  console.log('Column selected:', args.column);
};

const handleColumnDeselected = (args) => {
  console.log('Column deselected:', args.column);
};
</script>
```

## Checkbox Selection

### Row Selector Column
```vue
<template>
  <ejs-grid :dataSource="data">
    <e-columns>
      <e-column type="checkbox" width="50"></e-column>
      <e-column field="OrderID" headerText="Order ID" width="100"></e-column>
      <e-column field="CustomerID" headerText="Customer ID" width="120"></e-column>
    </e-columns>
  </ejs-grid>
</template>
```

### Checkbox Selection Modes

Configure checkbox behavior with `checkboxMode`:

```javascript
const selectionSettings = {
  checkboxOnly: true,
  checkboxMode: 'Default',     // 'Default' or 'ResetOnRowClick'
  type: 'Row'
};
```

**Checkbox Modes:**
- **`Default`** - Checkbox selection independent of row click
- **`ResetOnRowClick`** - Reset other selections when clicking a row

### Allow Checkbox-Only Selection
```vue
<template>
  <ejs-grid 
    :dataSource="data"
    :selectionSettings="selectionSettings">
    <e-columns>
      <e-column type="checkbox" width="50"></e-column>
      <e-column field="OrderID" width="100"></e-column>
    </e-columns>
  </ejs-grid>
</template>

<script setup>
const selectionSettings = {
  checkboxOnly: true,  // Only allow checkbox selection, not row click
  type: 'Row'
};
</script>
```

### Prevent Selection on Specific Rows
```vue
<template>
  <ejs-grid 
    :dataSource="data"
    :rowDataBound="handleRowDataBound">
    <e-columns>
      <e-column type="checkbox" width="50"></e-column>
      <e-column field="OrderID" width="100"></e-column>
    </e-columns>
  </ejs-grid>
</template>

<script setup>
const handleRowDataBound = (args) => {
  // Disable checkbox for specific rows (e.g., cancelled orders)
  if (args.data.Status === 'Cancelled') {
    args.isSelectable = false;
  }
};
</script>
```

### Partial Checkbox Selection

Use `isRowSelectable` function with `rowDataBound` event:

```javascript
const selectionSettings = {
  type: 'Row'
};

const handleRowDataBound = (args) => {
  // Allow selection only for orders with Freight > 50
  if (args.data.Freight < 50) {
    args.isSelectable = false;
  }
};
```

## Selection Persistence

Persist selection when paging or re-binding data:

```javascript
const selectionSettings = {
  type: 'Row',
  mode: 'Multiple',
  persistSelection: true  // Maintain selection across page navigation
};
```

## Toggle Selection

Allow users to toggle selection on/off for the same row/cell:

```javascript
const selectionSettings = {
  type: 'Row',
  mode: 'Multiple',
  enableToggle: true  // Click again to deselect
};
```

## Programmatic Selection

### Select Rows
```javascript
// Select by row index
gridInstance.selectRow(0);

// Select multiple rows
gridInstance.selectRows([0, 2, 4]);

// Select all rows
gridInstance.selectAll();
```

### Deselect Rows
```javascript
// Deselect by row index
gridInstance.deselectRow(0);

// Clear all selection
gridInstance.clearSelection();
```

## Selection Events

### Row Selected Event
```vue
<template>
  <ejs-grid 
    :dataSource="data"
    :rowSelected="handleRowSelected">
    <!-- columns -->
  </ejs-grid>
</template>

<script setup>
const handleRowSelected = (args) => {
  console.log('Row selected:', args.data);
  console.log('Row index:', args.rowIndex);
};
</script>
```

### Row Deselected Event
```javascript
const handleRowDeselected = (args) => {
  console.log('Row deselected:', args.data);
};
```

## Get Selected Data

### Get Selected Rows
```javascript
// Get selected row data
const selectedRecords = gridInstance.getSelectedRecords();
console.log(selectedRecords);  // Array of selected records

// Get selected row indices
const selectedIndices = gridInstance.getSelectedRowIndexes();
console.log(selectedIndices);  // [0, 2, 4]
```

### Get Selected Cells indexes
```javascript
// Get selected cells indexes
const selectedCells = gridInstance.getSelectedRowCellIndexes();
```
