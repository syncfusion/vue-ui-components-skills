# Selection

## Table of Contents
- [Selection Overview](#selection-overview)
- [Enable / Disable Selection](#enable--disable-selection)
- [Selection Mode](#selection-mode)
- [Selection Type](#selection-type)
- [Row Selection](#row-selection)
- [Select Row on Initial Load](#select-row-on-initial-load)
- [Select Row Dynamically](#select-row-dynamically)
- [Multiple Row Selection](#multiple-row-selection)
- [Select Rows Based on Condition](#select-rows-based-on-condition)
- [Cell Selection](#cell-selection)
- [Multiple Cell Selection](#multiple-cell-selection)
- [Select Cell Dynamically](#select-cell-dynamically)
- [Toggle Selection](#toggle-selection)
- [Hover Highlighting](#hover-highlighting)
- [selectionSettings Reference](#selectionsettings-reference)
- [Programmatic Selection APIs](#programmatic-selection-apis)
- [Selection Events](#selection-events)
- [Prevent Row Selection](#prevent-row-selection)
- [Prevent Cell Selection](#prevent-cell-selection)
- [Checkbox Selection](#checkbox-selection)
- [Touch Interaction](#touch-interaction)

## Selection Overview

Gantt supports row and cell selection. Selection is enabled by default. Inject the `Selection` module and configure via `selectionSettings`.

```js
import { GanttComponent as EjsGantt, Selection } from '@syncfusion/ej2-vue-gantt';
provide('gantt', [Selection]);
```

## Enable / Disable Selection

Selection is enabled by default. Disable it entirely with `allowSelection: false`:

```vue
<ejs-gantt :allowSelection="false" ...></ejs-gantt>
```

## Selection Mode

Set `selectionSettings.mode` to control what can be selected:

| Mode | Description |
|---|---|
| `'Row'` | Select entire rows only (default) |
| `'Cell'` | Select individual grid cells only |
| `'Both'` | Select rows and cells simultaneously |

```vue
<ejs-gantt :selectionSettings="{ mode: 'Both' }" ...></ejs-gantt>
```

## Selection Type

Set `selectionSettings.type` to control how many items can be selected:

| Type | Description |
|---|---|
| `'Single'` | Only one row or cell at a time (default) |
| `'Multiple'` | Multiple rows or cells — hold Ctrl to add to selection |

## Row Selection

```vue
<ejs-gantt
  :selectionSettings="selectionSettings"
  @rowSelected="onRowSelected"
  @rowDeselected="onRowDeselected"
  ...
></ejs-gantt>

<script setup>
const selectionSettings = {
  mode: 'Row',
  type: 'Single'
};

function onRowSelected(args) {
  console.log('Selected row data:', args.data);
  console.log('Selected row index:', args.rowIndex);
}

function onRowDeselected(args) {
  console.log('Deselected row data:', args.data);
}
</script>
```

## Select Row on Initial Load

Use `selectedRowIndex` to pre-select a row when the Gantt first renders (zero-based flat row index):

```vue
<ejs-gantt :selectedRowIndex="5" ...></ejs-gantt>
```

## Select Row Dynamically

```js
const gantt = this.$refs.ganttRef.ej2Instances;

gantt.selectionModule.selectRow(2);          // select single row by index
gantt.selectionModule.selectRows([1, 2, 3]); // select multiple rows by indexes
```

## Multiple Row Selection

```vue
<ejs-gantt :selectionSettings="{ mode: 'Row', type: 'Multiple' }" ...></ejs-gantt>
```

Hold **Ctrl+Click** to add rows to the selection. Hold **Shift+Click** to select a range.

## Select Rows Based on Condition

Select rows programmatically based on data values using the `dataBound` event:

```vue
<ejs-gantt
  :selectionSettings="{ mode: 'Row', type: 'Multiple' }"
  @dataBound="onDataBound"
  ...
></ejs-gantt>

<script setup>
const gantt = ref(null);

function onDataBound() {
  const ganttObj = gantt.value.ej2Instances;
  const rowIndexes = [];
  ganttObj.treeGrid.grid.dataSource.forEach((data, index) => {
    if (data.TaskID === 3 || data.TaskID === 4) {
      rowIndexes.push(index);
    }
  });
  ganttObj.selectionModule.selectRows(rowIndexes);
}
</script>
```

## Cell Selection

Set `mode: 'Cell'` to enable cell selection:

```vue
<ejs-gantt :selectionSettings="{ mode: 'Cell' }" @cellSelected="onCellSelected" ...></ejs-gantt>

<script setup>
function onCellSelected(args) {
  // args.selectedRowCellIndex contains cellIndexes and rowIndex
  console.log('Selected cell indexes:', args.selectedRowCellIndex[0].cellIndexes);
}
</script>
```

Get all selected cell info using `getSelectedRowCellIndexes()`:

```js
const selected = gantt.selectionModule.getSelectedRowCellIndexes();
// returns [{ rowIndex: 1, cellIndexes: [2] }, ...]
```

> **Note:** Cell selection is not supported when virtualization (`enableVirtualization`) is enabled.

## Multiple Cell Selection

```vue
<ejs-gantt :selectionSettings="{ mode: 'Cell', type: 'Multiple' }" ...></ejs-gantt>
```

Hold **Ctrl+Click** to select multiple cells.

## Select Cell Dynamically

```js
const gantt = this.$refs.ganttRef.ej2Instances;

gantt.selectionModule.selectCell({ rowIndex: 1, cellIndex: 1 });
```

## Toggle Selection

When `enableToggle: true`, clicking an already-selected row or cell deselects it. Default is `false`.

```vue
<ejs-gantt :selectionSettings="{ mode: 'Row', type: 'Multiple', enableToggle: true }" ...></ejs-gantt>
```

Disable toggle programmatically at runtime:

```js
gantt.selectionSettings.enableToggle = false;
```

## Hover Highlighting

Enable hover highlighting on grid rows, taskbars, header cells, and timeline cells:

```vue
<ejs-gantt :enableHover="true" ...></ejs-gantt>
```

## selectionSettings Reference

| Property | Type | Default | Description |
|---|---|---|---|
| `mode` | string | `'Row'` | `'Row'`, `'Cell'`, or `'Both'` |
| `type` | string | `'Single'` | `'Single'` or `'Multiple'` |
| `enableToggle` | boolean | `false` | Click selected row/cell again to deselect |
| `persistSelection` | boolean | `false` | Persist selection across data refresh |
| `checkboxOnly` | boolean | `false` | Allow selection only via checkbox column |
| `checkboxMode` | string | `'Default'` | `'Default'` or `'ResetOnRowClick'` |

## Programmatic Selection APIs

```js
const gantt = this.$refs.ganttRef.ej2Instances;

// Row selection
gantt.selectionModule.selectRow(2);           // by row index
gantt.selectionModule.selectRows([0, 2, 4]);  // multiple indexes

// Cell selection
gantt.selectionModule.selectCell({ rowIndex: 1, cellIndex: 2 });

// Clear all selection
gantt.clearSelection();

// Get selected data
const records = gantt.getSelectedRecords();                        // array of data objects
const indexes = gantt.getSelectedRowIndexes();                     // array of row indexes
const cells   = gantt.selectionModule.getSelectedRowCellIndexes(); // cell selection info
```

## Selection Events

| Event | Args | When fired |
|---|---|---|
| `rowSelecting` | `data`, `cancel` | Before row selection — set `args.cancel = true` to prevent |
| `rowSelected` | `data`, `rowIndex`, `row` | After row selection completes |
| `rowDeselecting` | `data`, `cancel` | Before row deselection — set `args.cancel = true` to prevent |
| `rowDeselected` | `data`, `rowIndex`, `row` | After row deselection completes |
| `cellSelecting` | `data`, `cellIndex`, `cancel` | Before cell selection — set `args.cancel = true` to prevent |
| `cellSelected` | `selectedRowCellIndex` | After cell selection completes |
| `cellDeselected` | `selectedRowCellIndex` | After cell deselection completes |

## Prevent Row Selection

Use the `rowSelecting` event to cancel selection based on row data:

```vue
<ejs-gantt @rowSelecting="onRowSelecting" ...></ejs-gantt>

<script setup>
function onRowSelecting(args) {
  if (args.data.TaskID === 4) {
    args.cancel = true;
  }
}
</script>
```

## Prevent Cell Selection

Use the `cellSelecting` event to cancel cell selection based on row/cell conditions:

```vue
<ejs-gantt :selectionSettings="{ mode: 'Cell' }" @cellSelecting="onCellSelecting" ...></ejs-gantt>

<script setup>
function onCellSelecting(args) {
  if (args.data.TaskID === 4 && args.cellIndex.cellIndex === 1) {
    args.cancel = true;
  }
}
</script>
```

## Checkbox Selection

Add a checkbox column and restrict selection to checkbox clicks only:

```js
const columns = [
  { type: 'checkboxselect', width: 50 },
  { field: 'TaskName', headerText: 'Task Name', width: 250 },
];

const selectionSettings = {
  type: 'Multiple',
  checkboxOnly: true
};
```

```vue
<ejs-gantt :columns="columns" :selectionSettings="selectionSettings" ...></ejs-gantt>
```

### checkboxMode options

| Value | Behavior |
|---|---|
| `'Default'` | Clicking a row also toggles its checkbox |
| `'ResetOnRowClick'` | Clicking a row clears all other checkboxes and selects only that row |

## Touch Interaction

On touch devices:
- **Single tap** on a row — selects that row
- **Multi-row selection** — tap a row to see the multi-select popup, then tap additional rows to add to the selection
