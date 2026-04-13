# Filtering

## Table of Contents
- [Overview](#overview)
- [Member Filtering](#member-filtering)
- [Label Filtering](#label-filtering)
- [Value Filtering](#value-filtering)
- [Programmatic Filtering](#programmatic-filtering)
- [Filter Performance Tips](#filter-performance-tips)

## Overview

Filtering helps you focus on specific data by showing only the records you need in the Pivot Table. Three types of filtering options are available: **member filtering**, **label filtering**, and **value filtering**. Property: [`allowMemberFilter`](https://ej2.syncfusion.com/vue/documentation/api/pivotview/dataSourceSettingsModel#allowmemberfilter)

## Member Filtering

### Enable Member Filtering (Default)

Member filtering displays the Pivot Table with selective records based on the members you choose to include or exclude. By default, `allowMemberFilter` is **true**.

```vue
<template>
  <ejs-pivotview 
    :dataSourceSettings="dataSourceSettings"
    :height="height">
  </ejs-pivotview>
</template>

<script setup>
import { PivotViewComponent as EjsPivotview, FieldList } from "@syncfusion/ej2-vue-pivotview";
import { provide } from "vue";
import { pivotData } from './pivotData.js';

const dataSourceSettings = {
  dataSource: pivotData,
  rows: [{ name: 'Country' }, { name: 'Products' }],
  columns: [{ name: 'Year' }, { name: 'Quarter' }],
  values: [{ name: 'Amount', caption: 'Sales Amount' }],
  filters: [],
  allowMemberFilter: true  // Enable member filtering (default)
};

const height = 350;

provide('pivotview', [FieldList]);
</script>
```

### Filter Dialog Features

**Search Members:**
```vue
<!-- Type in search box to find specific members -->
<!-- Matches partial names -->
<!-- Filter updates in real-time -->
```

**Select/Deselect All:**
- **Check "All":** Select all members
- **Uncheck "All":** Deselect all members
- **Mixed state:** Some members selected, some not

**Sort Members:**
- Ascending (A-Z)
- Descending (Z-A)
- By count
- Original order

### Programmatic Member Filtering

```vue
<script setup>
const dataSourceSettings = {
  dataSource: pivotData,
  rows: [{ name: 'Country' }],
  columns: [{ name: 'Year' }],
  values: [{ name: 'Amount' }],
  
  // Apply member filter programmatically
  filterSettings: [
    {
      name: 'Country',
      type: 'Include',  // Include: true, Exclude: false
      items: ['USA', 'Canada', 'UK']  // Selected members
    },
    {
      name: 'Year',
      type: 'Exclude',
      items: ['2018', '2019']  // Excluded members
    }
  ]
};
</script>
```

**Filter Properties:**
- **`name`**: Field name to filter
- **`type`**: `Include` or `Exclude`
- **`items`**: Array of member names
- **`levelCount`**: (OLAP only) Level in hierarchy

## Label Filtering

### Enable Label Filtering

Label filtering displays data based on field member names matching specific criteria (contains, starts with, ends with, etc.). Property: [`allowLabelFilter`](https://ej2.syncfusion.com/vue/documentation/api/pivotview/dataSourceSettingsModel#allowlabelfilter)

```vue
<script setup>
const dataSourceSettings = {
  dataSource: pivotData,
  rows: [{ name: 'Country' }],
  columns: [{ name: 'Products' }],
  values: [{ name: 'Amount' }],
  allowLabelFilter: true
};
</script>
```

### Operator Types

| Operator | Match | Example |
|----------|-------|---------|
| Equals | Exact match | "USA" |
| NotEquals | Not exact | Excludes "USA" |
| BeginsWith | Starts with | "U*" matches USA, UK |
| EndsWith | Ends with | "*A" matches USA, Canada |
| Contains | Substring | "*ld" matches England |
| NotContains | Excludes substring | Excludes "*ld" |
| GreaterThan | Alphabetically after | > "N" |
| LessThan | Alphabetically before | < "N" |
| GreaterThanOrEqualTo | >= | >= "L" |
| LessThanOrEqualTo | <= | <= "S" |

## Value Filtering

### Enable Value Filtering

Value filtering displays data based on aggregated value ranges. Property: [`allowValueFilter`](https://ej2.syncfusion.com/vue/documentation/api/pivotview/dataSourceSettingsModel#allowvaluefilter)

```vue
<script setup>
const dataSourceSettings = {
  dataSource: pivotData,
  rows: [{ name: 'Country' }],
  columns: [{ name: 'Products' }],
  values: [{ name: 'Amount' }],
  allowValueFilter: true
};
</script>
```

### Value Filter Operators

| Operator | Means |
|----------|-------|
| Equals | Value equals specified number |
| NotEquals | Value not equal to number |
| GreaterThan | Value > specified number |
| GreaterThanOrEqualTo | Value >= specified number |
| LessThan | Value < specified number |
| LessThanOrEqualTo | Value <= specified number |
| Between | Value between two numbers |
| NotBetween | Value outside range |

## Programmatic Filtering

### Apply Multiple Filters

```vue
<script setup>
const dataSourceSettings = {
  dataSource: largeDataset,
  rows: [{ name: 'Country' }, { name: 'Region' }],
  columns: [{ name: 'Year' }],
  values: [{ name: 'Amount' }],
  
  // Combine multiple filter types
  filterSettings: [
    {
      name: 'Country',
      type: 'Include',
      items: ['USA', 'Canada']
    },
    {
      name: 'Region',
      type: 'Exclude',
      items: ['South', 'West']
    }
  ],
  
  // Member filter + value filter in UI
  allowMemberFilter: true,
  allowValueFilter: true
};
</script>
```

### Dynamic Filter Updates

```vue
<script setup>
// Update filters at runtime
const updateFilters = (newCountry) => {
  dataSourceSettings.filterSettings[0].items = [newCountry];
  // Pivot table updates automatically
};
</script>
```

## Filter Performance Tips

### Large Dataset Optimization

```vue
<script setup>
// Limit members shown in filter dialog
:maxNodeLimitInMemberEditor="500"
</script>
```

**Default:** 1000 members shown initially
**Performance impact:** When filtered list > limit, pagination is used

### Disable Unused Filters

```vue
<script setup>
const dataSourceSettings = {
  allowMemberFilter: true,    // Only enable needed filters
  allowLabelFilter: false,
  allowValueFilter: false
};
</script>
```

Disabling filters reduces UI complexity and improves performance.

### Best Practices

1. **Pre-filter large datasets** - Apply filters at data load time
2. **Limit filter items** - Use Include type instead of Exclude for large lists
3. **Use member filter** - Most performant option
4. **Defer layout update** - Set `allowDeferLayoutUpdate: true` for complex filters
5. **Test with realistic data** - Ensure filters work with actual dataset size

### Performance Checklist

- [ ] Filter type matches use case (Member/Label/Value)
- [ ] Large datasets use Include filters
- [ ] Programmatic filters applied at initialization
- [ ] Unused filter options disabled
- [ ] `maxNodeLimitInMemberEditor` set if dataset >1000 items
- [ ] Defer layout enabled for complex filtering
