# Data Labels and Annotations

## Table of Contents
- [Data Labels](#data-labels)
  - [Enable Data Labels](#enable-data-labels)
  - [Label Positioning](#label-positioning)
  - [Label Formatting](#label-formatting)
  - [Label Templates](#label-templates)
  - [Label Styling](#label-styling)
  - [Example: Currency Labels with Bold Font](#example-currency-labels-with-bold-font)
- [Annotations](#annotations)
  - [Text Annotation](#text-annotation)
  - [Shape Annotation](#shape-annotation)
  - [Image Annotation](#image-annotation)
  - [Positioning Annotations](#positioning-annotations)
  - [Example: Highlight Q1 Sales Peak](#example-highlight-q1-sales-peak)
- [Dynamic Updates](#dynamic-updates)
  - [Update Labels on Data Change](#update-labels-on-data-change)
  - [Update Annotations Programmatically](#update-annotations-programmatically)
- [Common Patterns](#common-patterns)
  - [Pattern 1: Percentage Labels in Pie Chart](#pattern-1-percentage-labels-in-pie-chart)
  - [Pattern 2: Currency Format with Commas](#pattern-2-currency-format-with-commas)
  - [Pattern 3: Highlight Top 3 Values](#pattern-3-highlight-top-3-values)
  - [Pattern 4: Comparison Annotation](#pattern-4-comparison-annotation)
- [Troubleshooting](#troubleshooting)
  - [Labels Overlapping](#labels-overlapping)
  - [Annotations Not Visible](#annotations-not-visible)
  - [Labels Appear Outside Chart](#labels-appear-outside-chart)
- [Next Steps](#next-steps)

Data labels display values directly on data points, while annotations add text, shapes, and images to highlight specific areas or insights.

## Data Labels

### Enable Data Labels

```vue
<template>
  <ejs-chart>
    <e-series-collection>
      <e-series :dataSource="data" type="Column" xName="month" yName="sales" 
                :marker="marker" name="Sales">
      </e-series>
    </e-series-collection>
  </ejs-chart>
</template>

<script setup>
const marker = {
  dataLabel: { visible: true }
};

const data = [
  { month: "Jan", sales: 35 },
  { month: "Feb", sales: 28 },
  { month: "Mar", sales: 34 },
];
</script>
```

### Label Positioning

```vue
const dataLabelSettings = {
  visible: true,
  position: 'Top',    // 'Top', 'Bottom', 'Left', 'Right', 'Middle', 'Auto'
};
```

**Position Options:**
- `Top` - Above the data point
- `Bottom` - Below the data point
- `Left` - Left of the data point
- `Right` - Right of the data point
- `Middle` - Center of the data point
- `Auto` - Best position (default)

### Label Formatting

```vue
const dataLabelSettings = {
  visible: true,
  format: '${point.y}K',     // Show as "35K"
};
```

**Format Placeholders:**
- `${point.x}` - X-axis value
- `${point.y}` - Y-axis value
- `${point.percentage}` - Percentage (pie charts)
- `${series.name}` - Series name

### Label Templates

```vue
<template>
  <ejs-chart>
    <e-series-collection>
      <e-series :dataSource="data" type="Column" xName="month" yName="sales" 
                :marker="marker">
      </e-series>
    </e-series-collection>
  </ejs-chart>
</template>

<script setup>
const marker = {
  dataLabel: {
    visible: true,
    template: '#label-template',
  }
};
</script>

<template id="label-template">
  <div style="background: rgba(255,255,255,0.8); padding: 2px 5px; border-radius: 3px;">
    <b>${point.y}</b>
  </div>
</template>
```

### Label Styling

```vue
const dataLabelSettings = {
  visible: true,
  textStyle: {
    color: '#fff',
    fontFamily: 'Arial',
    fontSize: 12,
    fontWeight: 'bold',
  },
  backgroundColor: '#666',
  border: {
    color: '#ccc',
    width: 1,
  },
  margin: { left: 5, right: 5, top: 5, bottom: 5 },
};
```

### Example: Currency Labels with Bold Font

```vue
const dataLabelSettings = {
  visible: true,
  format: '$${point.y}',
  textStyle: {
    color: '#333',
    fontSize: 14,
    fontWeight: 'bold',
  },
  position: 'Top',
};
```

## Annotations

**Annotations** add text, shapes, or images to highlight specific areas of the chart.

### Text Annotation

```vue
<template>
  <ejs-chart :annotations="annotations">
    <!-- series -->
  </ejs-chart>
</template>

<script setup>
const annotations = [
  {
    content: 'Peak Sales',
    x: '50%',
    y: '20%',
    coordinateUnits: 'Percent',
  }
];
</script>
```

### Shape Annotation

```vue
const annotations = [
  {
    type: 'Rectangle',
    x: 2,
    y: 30,
    width: 3,
    height: 40,
    fill: 'rgba(255, 0, 0, 0.2)',
    border: { color: 'red', width: 2 },
  }
];
```

**Shape Types:**
- `Rectangle` - Rectangular region
- `Circle` - Circular region
- `Line` - Line segment
- `Ellipse` - Oval region

### Image Annotation

```vue
const annotations = [
  {
    type: 'Image',
    x: '50%',
    y: '30%',
    height: 50,
    width: 50,
    url: '/images/icon.png',
  }
];
```

### Positioning Annotations

```vue
const annotation = {
  content: 'Peak Sales',
  x: 2,              // X position (data value or percentage)
  y: 50,             // Y position (data value or percentage)
  coordinateUnits: 'Point',    // 'Point' (data units) or 'Percent' (percentage)
  verticalAlignment: 'Top',    // 'Top', 'Middle', 'Bottom'
  horizontalAlignment: 'Center', // 'Center', 'Left', 'Right'
};
```

### Example: Highlight Q1 Sales Peak

```vue
<template>
  <ejs-chart :annotations="annotations">
    <e-series-collection>
      <e-series :dataSource="data" type="Column" xName="month" yName="sales">
      </e-series>
    </e-series-collection>
  </ejs-chart>
</template>

<script setup>
const annotations = [
  {
    type: 'Rectangle',
    x: 1,           // Start at month "Feb"
    y: 20,          // Start at sales value 20
    width: 1,       // Cover 1 month width
    height: 20,     // Height in data units
    fill: 'rgba(255, 255, 0, 0.2)',
    border: { color: 'orange', width: 2 },
  },
  {
    content: 'Peak Season',
    x: 1.5,
    y: 40,
    textStyle: {
      fontWeight: 'bold',
      color: 'orange',
      fontSize: 14,
    },
  }
];

const data = [
  { month: "Jan", sales: 35 },
  { month: "Feb", sales: 42 },  // Peak
  { month: "Mar", sales: 34 },
];
</script>
```

## Dynamic Updates

### Update Labels on Data Change

```vue
<template>
  <button @click="updateData">Update Data</button>
  <ejs-chart ref="chart">
    <e-series-collection>
      <e-series :dataSource="data" :marker="marker" type="Column" 
                xName="month" yName="sales">
      </e-series>
    </e-series-collection>
  </ejs-chart>
</template>

<script setup>
import { ref } from "vue";

const chart = ref(null);
const data = ref([
  { month: "Jan", sales: 35 },
  { month: "Feb", sales: 28 },
  { month: "Mar", sales: 34 },
]);

const marker = {
  dataLabel: {
    visible: true,
    format: '${point.y}K',
  }
};

const updateData = () => {
  data.value = [
    { month: "Jan", sales: 40 },
    { month: "Feb", sales: 45 },
    { month: "Mar", sales: 50 },
  ];
  // Labels automatically update with new data
};
</script>
```

### Update Annotations Programmatically

```vue
// Get chart instance
const chartInstance = chart.value.ej2_instances[0];

// Update annotation
chartInstance.annotations = [
  {
    content: 'New Peak',
    x: 3,
    y: 60,
  }
];

// Refresh chart
chartInstance.refresh();
```

## Common Patterns

### Pattern 1: Percentage Labels in Pie Chart
```vue
const dataLabelSettings = {
  visible: true,
  format: '${point.percentage}%',
  position: 'Outside',
};
```

### Pattern 2: Currency Format with Commas
```vue
const dataLabelSettings = {
  visible: true,
  format: '$${point.y:N0}',  // N0 = no decimal places with commas
};
```

### Pattern 3: Highlight Top 3 Values
```vue
<template>
  <ejs-chart :annotations="topAnnotations">
    <!-- series -->
  </ejs-chart>
</template>

<script setup>
const topAnnotations = [
  {
    x: 2,
    y: 50
  },
  // ... more rectangles for other top values
];
</script>
```

### Pattern 4: Comparison Annotation
```vue
const annotations = [
  {
    x: 0,
    y: 40
  },
  {
    content: 'Target: 40',
    x: 2,
    y: 42
  }
];
```

## Troubleshooting

### Labels Overlapping
**Solution:** Use `position: 'Top'` or `position: 'Bottom'` instead of `Auto`

### Annotations Not Visible
**Solution:** Check `coordinateUnits` matches your axis type. Use `'Point'` for data values, `'Percent'` for percentages.

### Labels Appear Outside Chart
**Solution:** Reduce `fontSize` or use shorter `format`

## Next Steps

- Configure interactivity: [Interactions and Events](../interactions-and-events.md)
- Customize colors: [Customization and Styling](../customization-and-styling.md)
- Export charts: [Export and Data Management](../export-and-data-management.md)
