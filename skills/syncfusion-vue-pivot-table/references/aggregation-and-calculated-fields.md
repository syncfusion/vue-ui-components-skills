# Aggregation and Calculated Fields

## Table of Contents
- [Overview](#overview)
- [Aggregation Types](#aggregation-types)
- [Setting Aggregation Type](#setting-aggregation-type)
- [Changing Aggregation at Runtime](#changing-aggregation-at-runtime)
- [Customizing Aggregation Dropdown](#customizing-aggregation-dropdown)
- [Hiding Aggregation Label](#hiding-aggregation-label)
- [Advanced Aggregation](#advanced-aggregation)

## Overview

Aggregation combines multiple data values into a single summary value (Sum, Average, Count, etc.). By default, values are summed. Each value field must have an aggregation type. Property: [`type`](https://ej2.syncfusion.com/vue/documentation/api/pivotview/iFieldOptions#type)

## Aggregation Types

### Numeric Field Types (All Supported)

| Type | Description | Use Case |
|------|-------------|----------|
| **Sum** | Total of all values (Default) | Sales totals, revenue |
| **Avg** | Mean of values | Average price, avg quantity |
| **Count** | Total record count | Number of transactions |
| **Min** | Lowest value | Minimum sale amount |
| **Max** | Highest value | Peak sales, max price |
| **Product** | Multiplication of all values | Growth rates, compounded values |
| **Median** | Middle value (50th percentile) | Typical value, outlier detection |
| **DistinctCount** | Count of unique records | Unique customers, unique products |
| **SampleStDev** | Sample standard deviation (n-1) | Data variability within sample |
| **PopulationStDev** | Population std dev (all data) | Variability across entire dataset |
| **SampleVar** | Sample variance | Spread in sample |
| **PopulationVar** | Population variance | Spread across population |

### Percentage and Comparative Types

| Type | Description | Base Field? |
|------|-------------|-------------|
| **PercentageOfRowTotal** | Row sum % | No |
| **PercentageOfColumnTotal** | Column sum % | No |
| **PercentageOfGrandTotal** | Grand total % | No |
| **PercentageOfParentTotal** | Parent group % | Yes |
| **PercentageOfParentRowTotal** | Parent row % | Yes |
| **PercentageOfParentColumnTotal** | Parent column % | Yes |
| **DifferenceFrom** | Difference vs base item | Yes (baseField, baseItem) |
| **PercentageOfDifferenceFrom** | % difference vs base | Yes (baseField, baseItem) |
| **RunningTotals** | Cumulative sum | No |

### Non-Numeric Field Types (Limited)

**Only two aggregations supported:**
- **Count** - Number of non-null records
- **Distinct Count** - Unique record count

## Setting Aggregation Type

### Basic Aggregation Setup

```vue
<script setup>
import { PivotViewComponent as EjsPivotview } from "@syncfusion/ej2-vue-pivotview";
import { pivotData } from './pivotData.js';

const dataSourceSettings = {
  dataSource: pivotData,
  rows: [{ name: 'Country' }],
  columns: [{ name: 'Year' }],
  values: [
    {
      name: 'Amount',
      type: 'Sum'  // Sum (default for numeric)
    },
    {
      name: 'Quantity',
      type: 'Avg'  // Average quantity per item
    },
    {
      name: 'Orders',
      type: 'Count'  // Total order count
    }
  ]
};
</script>
```

### Percentage Aggregation

```vue
<script setup>
const dataSourceSettings = {
  rows: [{ name: 'Country' }],
  columns: [{ name: 'Year' }],
  values: [
    {
      name: 'Amount',
      type: 'PercentageOfGrandTotal'  // Show % of all sales
    },
    {
      name: 'Quantity',
      type: 'PercentageOfRowTotal'  // Show % per country
    }
  ]
};
</script>
```

### Comparative Aggregation (Requires Base Field)

```vue
<script setup>
const dataSourceSettings = {
  rows: [{ name: 'Country' }],
  columns: [{ name: 'Year' }],
  values: [
    {
      name: 'Sales',
      type: 'DifferenceFrom',
      baseField: 'Year',    // Compare against Year field
      baseItem: '2022',     // Compare to 2022 values
      // Result: 2023 sales - 2022 sales = difference
    },
    {
      name: 'Revenue',
      type: 'PercentageOfDifferenceFrom',
      baseField: 'Region',
      baseItem: 'North',    // Compare to North values
      // Result: (South Revenue - North Revenue) / North Revenue * 100
    }
  ]
};
</script>
```

## Changing Aggregation at Runtime

### UI Aggregation Dropdown

Users can change aggregation by:
1. Click dropdown icon on value field (in Field List/Grouping Bar)
2. Select new aggregation type
3. Table updates immediately

**Supported Edit Modes:**
- Inline editing
- Dialog editing
- Batch editing

## Customizing Aggregation Dropdown

### Show Only Specific Aggregation Types

```vue
<template>
  <ejs-pivotview 
    :dataSourceSettings="dataSourceSettings"
    :aggregateTypes="aggregateTypes">
  </ejs-pivotview>
</template>

<script setup>
const dataSourceSettings = {
  dataSource: pivotData,
  rows: [{ name: 'Country' }],
  values: [{ name: 'Amount' }]
};

const aggregateTypes = [
  'Sum',
  'Avg',
  'Count',
  'Min',
  'Max'
];
</script>
```

### Example: Financial Dashboard

```vue
<script setup>
// Only show aggregations relevant for financial analysis
const aggregateTypes = [
  'Sum',           // Total revenue
  'Avg',           // Average expense
  'Min',           // Lowest cost
  'Max',           // Highest cost
  'SampleStDev',   // Shows risk/volatility
  'PercentageOfGrandTotal'  // Budget allocation
];
</script>
```

## Hiding Aggregation Label

### Remove "Sum of", "Average of" Text

```vue
<script setup>
const dataSourceSettings = {
  dataSource: pivotData,
  rows: [{ name: 'Country' }],
  columns: [{ name: 'Year' }],
  values: [
    { name: 'Amount' },
    { name: 'Quantity' }
  ],
  // Hide aggregation type display
  showAggregationOnValueField: false
};
</script>
```

### Display Results

**With `showAggregationOnValueField: true` (default):**
```
Field List shows:
- Sum of Amount
- Sum of Quantity
```

**With `showAggregationOnValueField: false`:**
```
Field List shows:
- Amount
- Quantity
```

**Use Case:** Cleaner UI when field names already indicate what they represent

## Advanced Aggregation

### Multiple Values with Mixed Aggregation

```vue
<script setup>
const dataSourceSettings = {
  values: [
    { name: 'Revenue', type: 'Sum' },
    { name: 'Transactions', type: 'Count' },
    { name: 'Price', type: 'Avg' },
    { name: 'Items', type: 'Sum' },
    { name: 'Profit', type: 'Sum' }
  ]
};
</script>
```

Each value field shows its configured aggregation independently.

### Running Totals (Cumulative Sum)

```vue
<script setup>
const dataSourceSettings = {
  rows: [{ name: 'Country' }],
  columns: [{ name: 'Month' }],
  values: [
    {
      name: 'Sales',
      type: 'RunningTotals'
      // Each cell shows cumulative sum to that point
    }
  ]
};
</script>
```

**Result:** Jan=100, Feb=250, Mar=450, etc. (cumulative)

### Calculated Field (Custom Formula)

When creating calculated fields, use the `calculatedFieldSettings` property to define custom fields based on formulas.

```vue
<script setup>
const dataSourceSettings = {
  values: [
    {
      name: 'TotalRevenue',
      type: 'CalculatedField'
    }
  ],
  calculatedFieldSettings: [
    {
      name: 'TotalRevenue',
      formula: '"Sum(Amount)"*"Sum(Quantity)"'  // Custom formula
    }
  ]
};
</script>
```

## Events

### AggregateCellInfo

The `aggregateCellInfo` event triggers each time a value cell renders. It allows you to intercept and modify cell values or skip formatting on specific cells.

**When to use:**
- Override cell values dynamically
- Skip formatting for specific cells
- Apply conditional logic based on cell data

```vue
<template>
  <div id="app">
    <ejs-pivotview 
      :dataSourceSettings="dataSourceSettings" 
      :aggregateCellInfo="aggregateCellInfo"
      :height="height">
    </ejs-pivotview>
  </div>
</template>
<script setup>
import { provide } from "vue";
import { PivotViewComponent as EjsPivotview } from "@syncfusion/ej2-vue-pivotview";
import { pivotData } from './pivotData.js';

const dataSourceSettings = {
  dataSource: pivotData,
  expandAll: false,
  columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
  values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
  rows: [{ name: 'Country' }, { name: 'Products' }],
  formatSettings: [{ name: 'Amount', format: 'C0' }],
  filters: []
};
const height = 350;

const aggregateCellInfo = (args) => {
  // args.fieldName - field name of current cell
  // args.value - value of current cell
  // args.cellSets - raw data for the aggregated value cell
  
  // Example: Override cell value or skip formatting
  if (args.fieldName === 'Amount' && args.value > 50000) {
    args.value = 'High';  // Display custom label
  }
  // args.skipFormatting = true;  // Optionally skip formatting
};

provide('pivotview', []);
</script>
<style>
@import "../node_modules/@syncfusion/ej2-vue-pivotview/styles/tailwind3.css";
</style>
```

### ActionBegin

The `actionBegin` event triggers when a UI action starts (e.g., aggregation change, drag operation). Use it to prevent or log actions before they execute.

**When to use:**
- Prevent specific actions (set `args.cancel = true`)
- Log user interactions
- Validate before action proceeds

```vue
<template>
  <div id="app">
    <ejs-pivotview 
      :dataSourceSettings="dataSourceSettings" 
      :showGroupingBar="showGroupingBar"
      :actionBegin="actionBegin"
      :height="height">
    </ejs-pivotview>
  </div>
</template>
<script setup>
import { provide } from "vue";
import { PivotViewComponent as EjsPivotview, GroupingBar, FieldList } from "@syncfusion/ej2-vue-pivotview";
import { pivotData } from './pivotData.js';

const dataSourceSettings = {
  dataSource: pivotData,
  expandAll: false,
  columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
  values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
  rows: [{ name: 'Country' }, { name: 'Products' }],
  formatSettings: [{ name: 'Amount', format: 'C0' }],
  filters: []
};
const height = 350;
const showGroupingBar = true;

const actionBegin = (args) => {
  // args.actionName - name of action being performed
  // args.cancel - set to true to prevent action
  
  console.log('Action starting:', args.actionName);
  
  // Example: Prevent aggregation changes
  if (args.actionName === 'Aggregate field') {
    // args.cancel = true;  // Uncomment to prevent
  }
};

provide('pivotview', [GroupingBar, FieldList]);
</script>
<style>
@import "../node_modules/@syncfusion/ej2-vue-pivotview/styles/tailwind3.css";
</style>
```

### ActionComplete

The `actionComplete` event triggers after a UI action finishes successfully. Use it to respond after changes are applied.

**When to use:**
- Refresh related components after aggregation change
- Update display based on new data
- Sync with external data sources

```vue
<template>
  <div id="app">
    <ejs-pivotview 
      :dataSourceSettings="dataSourceSettings" 
      :actionComplete="actionComplete"
      :height="height">
    </ejs-pivotview>
  </div>
</template>
<script setup>
import { PivotViewComponent as EjsPivotview } from "@syncfusion/ej2-vue-pivotview";
import { pivotData } from './pivotData.js';

const dataSourceSettings = {
  dataSource: pivotData,
  expandAll: false,
  columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
  values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
  rows: [{ name: 'Country' }, { name: 'Products' }],
  formatSettings: [{ name: 'Amount', format: 'C0' }],
  filters: []
};
const height = 350;

const actionComplete = (args) => {
  // args.actionName - name of completed action
  // args.dataSourceSettings - updated pivot configuration
  
  if (args.actionName === 'Field aggregated') {
    console.log('Aggregation changed successfully');
    // Perform post-update tasks
  }
};
</script>
<style>
@import "../node_modules/@syncfusion/ej2-vue-pivotview/styles/tailwind3.css";
</style>
```

### ActionFailure

The `actionFailure` event triggers when a UI action fails. Use it to handle errors and inform users.

**When to use:**
- Display error messages
- Log failures for debugging
- Implement retry logic

```vue
<template>
  <div id="app">
    <div v-if="errorMessage" class="error-box">{{ errorMessage }}</div>
    <ejs-pivotview 
      :dataSourceSettings="dataSourceSettings" 
      :actionFailure="actionFailure"
      :height="height">
    </ejs-pivotview>
  </div>
</template>
<script setup>
import { ref } from "vue";
import { PivotViewComponent as EjsPivotview } from "@syncfusion/ej2-vue-pivotview";
import { pivotData } from './pivotData.js';

const dataSourceSettings = {
  dataSource: pivotData,
  expandAll: false,
  columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
  values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
  rows: [{ name: 'Country' }, { name: 'Products' }],
  formatSettings: [{ name: 'Amount', format: 'C0' }],
  filters: []
};
const height = 350;
const errorMessage = ref('');

const actionFailure = (args) => {
  // args.actionName - name of failed action
  // args.errorInfo - error details
  
  errorMessage.value = `Action "${args.actionName}" failed. Error: ${args.errorInfo}`;
  console.error('Action failed:', args.errorInfo);
};
</script>
<style>
@import "../node_modules/@syncfusion/ej2-vue-pivotview/styles/tailwind3.css";
.error-box {
  background-color: #ffebee;
  color: #c62828;
  padding: 10px;
  border-radius: 4px;
  margin-bottom: 10px;
}
</style>
```

### CalculatedFieldCreate

The `calculatedFieldCreate` event triggers when users create or edit calculated fields. Use it to validate field definitions before saving.

**When to use:**
- Validate formulas
- Prevent invalid calculated fields
- Auto-format field names

```vue
<template>
  <div id="app">
    <ejs-pivotview 
      :dataSourceSettings="dataSourceSettings" 
      :showFieldList="showFieldList"
      :allowCalculatedField="allowCalculatedField"
      :calculatedFieldCreate="calculatedFieldCreate"
      :height="height">
    </ejs-pivotview>
  </div>
</template>
<script setup>
import { provide } from "vue";
import { PivotViewComponent as EjsPivotview, CalculatedField, FieldList } from "@syncfusion/ej2-vue-pivotview";
import { pivotData } from './pivotData.js';

const dataSourceSettings = {
  dataSource: pivotData,
  expandAll: false,
  columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
  values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
  rows: [{ name: 'Country' }, { name: 'Products' }],
  formatSettings: [{ name: 'Amount', format: 'C0' }],
  filters: []
};
const height = 350;
const showFieldList = true;
const allowCalculatedField = true;

const calculatedFieldCreate = (args) => {
  // args.calculatedField - new/edited calculated field
  // args.fieldName - field name
  // args.cancel - set to true to cancel creation
  
  // Validate that formula field is set
  if (!args.calculatedField.formula || args.calculatedField.formula.length === 0) {
    args.cancel = true;
    alert('Formula cannot be empty');
  }
};

provide('pivotview', [CalculatedField, FieldList]);
</script>
<style>
@import "../node_modules/@syncfusion/ej2-vue-pivotview/styles/tailwind3.css";
</style>
```
      name: 'Profit Margin',
      type: 'CalculatedField'
      // Formula: (Revenue - Cost) / Revenue
    }
  ]
};
</script>
```

Creates new field derived from existing fields.

### Performance Optimization for Aggregation

```vue
<template>
  <ejs-pivotview 
    :dataSourceSettings="dataSourceSettings"
    :allowDeferLayoutUpdate="true"
    :enableVirtualization="true">
  </ejs-pivotview>
</template>

<script setup>
const dataSourceSettings = {
  values: [
    { name: 'Amount', type: 'Sum' }  // Sum is fastest aggregation
  ]
};
</script>
```

**Component Properties for Performance:**
- `allowDeferLayoutUpdate: true` — Calculate only when needed (deferred calculation)
- `enableVirtualization: true` — Lazy calculate visible cells (render only visible area)

**Aggregation Performance (Fastest → Slowest):**
1. Sum (simplest calculation)
2. Count, Min, Max
3. Average
4. Standard Deviation, Variance
5. Percentage operations (more complex)
6. Calculated fields (most expensive)

### Aggregation Best Practices

- [ ] Use simple types (Sum, Count) for best performance
- [ ] Set `showAggregationOnValueField: false` for cleaner UI
- [ ] Limit custom aggregations in dropdown for clarity
- [ ] Use `baseField` for meaningful comparative analysis
- [ ] Test percentage types with actual data
- [ ] Document custom aggregation formulas
- [ ] Cache calculations for large datasets
- [ ] Use `allowDeferLayoutUpdate: true` for complex aggregations
