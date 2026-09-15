# Chart API Reference

## Table of Contents
- [Property Index](#property-index)
- [Properties](#properties)
  - [Layout & Dimensions](#layout--dimensions)
  - [Data](#data)
  - [Styling & Appearance](#styling--appearance)
  - [Title & Subtitle](#title--subtitle)
  - [Axes](#axes)
  - [Legend](#legend)
  - [Interaction](#interaction)
  - [Tooltips & Crosshair](#tooltips--crosshair)
  - [Zoom & Pan](#zoom--pan)
  - [Animations](#animations)
  - [Advanced Features](#advanced-features)
  - [Export & Accessibility](#export--accessibility)
  - [Localization & Others](#localization--others)
- [Data Models](#data-models)
  - [SeriesModel](#seriesmodel)
  - [AxisModel](#axismodel)
  - [TooltipSettingsModel](#tooltipsettingsmodel)
  - [LegendSettingsModel](#legendsettingsmodel)
  - [CrosshairSettingsModel](#crosshairsettingsmodel)
  - [ZoomSettingsModel](#zoomsettingsmodel)
  - [MarginModel](#marginmodel)
  - [BorderModel](#bordermodel)
  - [ChartAreaModel](#chartareamodel)
- [Events](#events)
  - [load](#load)
  - [loaded](#loaded)
  - [pointClick](#pointclick)
  - [pointMove](#pointmove)
  - [legendClick](#legendclick)
  - [tooltipRender](#tooltiprender)
  - [beforeExport](#beforeexport)
  - [afterExport](#afterexport)
  - [selectionComplete](#selectioncomplete)
  - [resized](#resized)
  - [animationComplete](#animationcomplete)
- [Methods](#methods)
  - [export()](#export)
  - [print()](#print)
  - [addSeries()](#addseries)
  - [removeSeries()](#removeseries)
  - [clearSeries()](#clearseries)
  - [hideTooltip()](#hidetooltip)
  - [showTooltip()](#showtooltip)
  - [destroy()](#destroy)
- [Enums](#enums)
  - [ChartSeriesType](#chartseriestype)
  - [SelectionMode](#selectionmode)
  - [HighlightMode](#highlightmode)
  - [LegendPosition](#legendposition)
  - [ChartTheme](#charttheme)
- [Child Directives](#child-directives)
  - [SeriesCollectionDirective / e-series-collection](#seriescollectiondirective--e-series-collection)
  - [SeriesDirective / e-series](#seriesdirective--e-series)
- [Modules](#modules)
  - [LineSeries](#lineseries)
  - [ColumnSeries](#columnseries)
  - [AreaSeries](#areaseries)
  - [BarSeries](#barseries)
  - [Legend](#legend)
  - [Tooltip](#tooltip)
  - [Category](#category)
  - [DateTime](#datetime)
  - [Export](#export)
  - [Crosshair](#crosshair)
  - [Zoom](#zoom)
- [Common Usage Patterns](#common-usage-patterns)
  - [Pattern 1: Access Chart Instance](#pattern-1-access-chart-instance)
  - [Pattern 2: Dynamic Series Update](#pattern-2-dynamic-series-update)
  - [Pattern 3: Handle Events](#pattern-3-handle-events)
- [Additional Resources](#additional-resources)

---

## Property Index

**Quick Links to All Properties:**
- [Layout & Dimensions](#layout--dimensions): width, height, margin, rows, columns, isTransposed
- [Data](#data): dataSource, series, selectedDataIndexes
- [Styling & Appearance](#styling--appearance): background, backgroundImage, border, theme, chartArea, palettes, highlightColor
- [Title & Subtitle](#title--subtitle): title, titleStyle, subTitle, subTitleStyle
- [Axes](#axes): primaryXAxis, primaryYAxis, axes
- [Legend](#legend): legendSettings
- [Interaction](#interaction): selectionMode, selectionPattern, highlightMode, highlightPattern, isMultiSelect, allowMultiSelection
- [Tooltips & Crosshair](#tooltips--crosshair): tooltip, crosshair
- [Zoom & Pan](#zoom--pan): zoomSettings
- [Animations](#animations): enableAnimation
- [Advanced Features](#advanced-features): annotations, indicators, rangeColorSettings, stackLabels, noDataTemplate
- [Export & Accessibility](#export--accessibility): enableExport, allowExport, accessibility, description
- [Localization & Others](#localization--others): locale, enableRtl, enablePersistence, useGroupingSeparator, enableCanvas, enableHtmlSanitizer, enableAutoIntervalOnBothAxis, enableSideBySidePlacement, tabIndex

---

## Properties

### Layout & Dimensions

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| width | string | null | The width of the chart as a string, accepting input such as '100px' or '100%'. | [width](https://ej2.syncfusion.com/vue/documentation/api/chart/#width) |
| height | string | null | The height of the chart as a string, accepting input such as '100px' or '100%'. | [height](https://ej2.syncfusion.com/vue/documentation/api/chart/#height) |
| margin | [MarginModel](https://ej2.syncfusion.com/vue/documentation/api/chart/marginmodel/) | — | Options to customize the margins around the chart (left, right, top, bottom). See [MarginModel](#marginmodel). | [margin](https://ej2.syncfusion.com/vue/documentation/api/chart/#margin) |
| rows | [RowModel[]](https://ej2.syncfusion.com/vue/documentation/api/chart/rowmodel/) | [] | Options to split the chart into multiple plotting areas horizontally. | [rows](https://ej2.syncfusion.com/vue/documentation/api/chart/#rows) |
| columns | [ColumnModel[]](https://ej2.syncfusion.com/vue/documentation/api/chart/columnmodel/) | [] | Options to split the chart into multiple plotting areas vertically. | [columns](https://ej2.syncfusion.com/vue/documentation/api/chart/#columns) |
| isTransposed | boolean | false | When set to true, the chart will render in a transposed manner with X and Y axes interchanged. | [isTransposed](https://ej2.syncfusion.com/vue/documentation/api/chart/#istransposed) |

### Data

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| dataSource | Object \| DataManager | '' | Specifies the data source for the chart (array of JSON objects or DataManager instance). | [dataSource](https://ej2.syncfusion.com/vue/documentation/api/chart/#datasource) |
| series | [SeriesModel[]](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/) | — | Configuration options for the chart's series. See [SeriesModel](#seriesmodel). | [series](https://ej2.syncfusion.com/vue/documentation/api/chart/#series) |
| selectedDataIndexes | [IndexesModel[]](https://ej2.syncfusion.com/vue/documentation/api/chart/indexesmodel/) | [] | Specifies the point indexes to be selected when a chart is initially loaded. | [selectedDataIndexes](https://ej2.syncfusion.com/vue/documentation/api/chart/#selecteddataindexes) |

### Styling & Appearance

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| background | string | null | The background color of the chart accepts values in hex and rgba formats as valid CSS color strings. | [background](https://ej2.syncfusion.com/vue/documentation/api/chart/#background) |
| backgroundImage | string | null | The background image of the chart accepts a string value as a URL link or the location of an image. | [backgroundImage](https://ej2.syncfusion.com/vue/documentation/api/chart/#backgroundimage) |
| border | [BorderModel](https://ej2.syncfusion.com/vue/documentation/api/chart/bordermodel/) | — | Options for customizing the appearance of the border in the chart. See [BorderModel](https://ej2.syncfusion.com/vue/documentation/api/chart/bordermodel/). | [border](https://ej2.syncfusion.com/vue/documentation/api/chart/#border) |
| theme | [ChartTheme](https://ej2.syncfusion.com/vue/documentation/api/chart/charttheme) | 'Material' | The theme applied to the chart for visual styling. See [ChartTheme](#charttheme) enum. | [theme](https://ej2.syncfusion.com/vue/documentation/api/chart/#theme) |
| chartArea | [ChartAreaModel](https://ej2.syncfusion.com/vue/documentation/api/chart/chartareamodel/) | — | Configuration options for the chart area's border and background. | [chartArea](https://ej2.syncfusion.com/vue/documentation/api/chart/#chartarea) |
| palettes | string[] | [] | The palettes array defines a set of colors used for rendering the chart's series. | [palettes](https://ej2.syncfusion.com/vue/documentation/api/chart/#palettes) |
| highlightColor | string | '' | Defines the color used to highlight a data point on mouse hover. | [highlightColor](https://ej2.syncfusion.com/vue/documentation/api/chart/#highlightcolor) |

### Title & Subtitle

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| title | string | '' | The title is displayed at the top of the chart to provide information about the plotted data. | [title](https://ej2.syncfusion.com/vue/documentation/api/chart/#title) |
| titleStyle | [TitleSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/titlesettingsmodel/) | — | Options for customizing the appearance of the title. See [TitleSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/titlesettingsmodel/). | [titleStyle](https://ej2.syncfusion.com/vue/documentation/api/chart/#titlestyle) |
| subTitle | string | '' | The subtitle is positioned below the main title and provides additional details about the data. | [subTitle](https://ej2.syncfusion.com/vue/documentation/api/chart/#subtitle) |
| subTitleStyle | [TitleSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/titlesettingsmodel/) | — | Options for customizing the appearance of the subtitle. See [TitleSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/titlesettingsmodel/). | [subTitleStyle](https://ej2.syncfusion.com/vue/documentation/api/chart/#subtitlestyle) |

### Axes

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| primaryXAxis | [AxisModel](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/) | — | The primaryXAxis property configures the horizontal axis of the chart. See [AxisModel](#axismodel). | [primaryXAxis](https://ej2.syncfusion.com/vue/documentation/api/chart/#primaryxaxis) |
| primaryYAxis | [AxisModel](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/) | — | The primaryYAxis property configures the vertical axis of the chart. See [AxisModel](#axismodel). | [primaryYAxis](https://ej2.syncfusion.com/vue/documentation/api/chart/#primaryyaxis) |
| axes | [AxisModel[]](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/) | — | Configuration options for secondary axes in the chart. See [AxisModel](#axismodel). | [axes](https://ej2.syncfusion.com/vue/documentation/api/chart/#axes) |

### Legend

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| legendSettings | [LegendSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/legendsettingsmodel/) | — | The legend provides descriptive information about the data series displayed in the chart. See [LegendSettingsModel](#legendsettingsmodel). | [legendSettings](https://ej2.syncfusion.com/vue/documentation/api/chart/#legendsettings) |

### Interaction

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| selectionMode | [SelectionMode](https://ej2.syncfusion.com/vue/documentation/api/chart/selectionmode) | 'None' | The selectionMode property determines how data points or series can be highlighted or selected. | [selectionMode](https://ej2.syncfusion.com/vue/documentation/api/chart/#selectionmode) |
| selectionPattern | [SelectionPattern](https://ej2.syncfusion.com/vue/documentation/api/chart/selectionpattern) | 'None' | The selectionPattern property determines how selected data points or series are visually represented. | [selectionPattern](https://ej2.syncfusion.com/vue/documentation/api/chart/#selectionpattern) |
| highlightMode | [HighlightMode](https://ej2.syncfusion.com/vue/documentation/api/chart/highlightmode) | 'None' | The highlightMode property determines how a series or individual data points are highlighted in the chart. | [highlightMode](https://ej2.syncfusion.com/vue/documentation/api/chart/#highlightmode) |
| highlightPattern | [SelectionPattern](https://ej2.syncfusion.com/vue/documentation/api/chart/selectionpattern) | 'None' | The highlightPattern property determines how data points or series are visually highlighted. | [highlightPattern](https://ej2.syncfusion.com/vue/documentation/api/chart/#highlightpattern) |
| isMultiSelect | boolean | false | When set to true, it allows selecting multiple data points, series, or clusters. | [isMultiSelect](https://ej2.syncfusion.com/vue/documentation/api/chart/#ismultiselect) |
| allowMultiSelection | boolean | false | If set to true, enables multi-drag selection in the chart by dragging a selection box. | [allowMultiSelection](https://ej2.syncfusion.com/vue/documentation/api/chart/#allowmultiselection) |

### Tooltips & Crosshair

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| tooltip | [TooltipSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/tooltipsettingsmodel/) | — | Configuration options for the chart's tooltip, which displays details about points when hovering. | [tooltip](https://ej2.syncfusion.com/vue/documentation/api/chart/#tooltip) |
| crosshair | [CrosshairSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/crosshairsettingsmodel/) | — | The crosshair displays lines on the chart that follow the mouse cursor and show axis values. | [crosshair](https://ej2.syncfusion.com/vue/documentation/api/chart/#crosshair) |

### Zoom & Pan

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| zoomSettings | [ZoomSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/zoomsettingsmodel/) | — | Options to enable and configure the zooming feature in the chart. | [zoomSettings](https://ej2.syncfusion.com/vue/documentation/api/chart/#zoomsettings) |

### Animations

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| enableAnimation | boolean | true | If set to true, animation effects will be enabled for chart elements when the legend is clicked, or the data source is updated. | [enableAnimation](https://ej2.syncfusion.com/vue/documentation/api/chart/#enableanimation) |

### Advanced Features

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| annotations | [ChartAnnotationSettingsModel[]](https://ej2.syncfusion.com/vue/documentation/api/chart/chartannotationsettingsmodel) | — | Annotations are used to highlight specific data points or areas in the chart. | [annotations](https://ej2.syncfusion.com/vue/documentation/api/chart/#annotations) |
| indicators | [TechnicalIndicatorModel[]](https://ej2.syncfusion.com/vue/documentation/api/chart/technicalindicatormodel) | — | Technical indicators assist in evaluating market conditions and identifying trends. | [indicators](https://ej2.syncfusion.com/vue/documentation/api/chart/#indicators) |
| rangeColorSettings | [RangeColorSettingModel[]](https://ej2.syncfusion.com/vue/documentation/api/chart/rangecolorsettingmodel) | — | The rangeColorSettings property specifies a set of rules for applying different colors based on value ranges. | [rangeColorSettings](https://ej2.syncfusion.com/vue/documentation/api/chart/#rangecolorsettings) |
| stackLabels | [StackLabelSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/stacklabelsettingsmodel) | — | Configuration options for stack labels in stacked charts. | [stackLabels](https://ej2.syncfusion.com/vue/documentation/api/chart/#stacklabels) |
| noDataTemplate | string \| Function | null | Specifies the template to be displayed when the chart has no data. | [noDataTemplate](https://ej2.syncfusion.com/vue/documentation/api/chart/#nodatatemplate) |

### Export & Accessibility

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| enableExport | boolean | true | When set to true, it enables exporting the chart to JPEG, PNG, SVG, PDF, XLSX, or CSV formats. | [enableExport](https://ej2.syncfusion.com/vue/documentation/api/chart/#enableexport) |
| allowExport | boolean | false | To enable export feature in Blazor chart. | [allowExport](https://ej2.syncfusion.com/vue/documentation/api/chart/#allowexport) |
| accessibility | [AccessibilityModel](https://ej2.syncfusion.com/vue/documentation/api/chart/accessibilitymodel) | — | Options to improve accessibility for chart elements. | [accessibility](https://ej2.syncfusion.com/vue/documentation/api/chart/#accessibility) |
| description | string | null | A description for the chart that provides additional information about its content for screen readers. | [description](https://ej2.syncfusion.com/vue/documentation/api/chart/#description) |

### Localization & Others

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| locale | string | '' | Overrides the global culture and localization value for this component. | [locale](https://ej2.syncfusion.com/vue/documentation/api/chart/#locale) |
| enableRtl | boolean | false | Enable or disable rendering component in right to left direction. | [enableRtl](https://ej2.syncfusion.com/vue/documentation/api/chart/#enablertl) |
| enablePersistence | boolean | false | Enable or disable persisting component's state between page reloads. | [enablePersistence](https://ej2.syncfusion.com/vue/documentation/api/chart/#enablepersistence) |
| useGroupingSeparator | boolean | false | When set to true, a grouping separator will be used for numbers to separate thousands. | [useGroupingSeparator](https://ej2.syncfusion.com/vue/documentation/api/chart/#usegroupingseparator) |
| enableCanvas | boolean | false | When set to true, the chart will render using a canvas instead of SVG. | [enableCanvas](https://ej2.syncfusion.com/vue/documentation/api/chart/#enablecanvas) |
| enableHtmlSanitizer | boolean | false | Specifies whether to display or remove untrusted HTML values in the Chart component. | [enableHtmlSanitizer](https://ej2.syncfusion.com/vue/documentation/api/chart/#enablehtmlsanitizer) |
| enableAutoIntervalOnBothAxis | boolean | false | If set to true, the intervals for all axes will be calculated automatically based on zoom range. | [enableAutoIntervalOnBothAxis](https://ej2.syncfusion.com/vue/documentation/api/chart/#enableautointervalonbothaxis) |
| enableSideBySidePlacement | boolean | true | This property controls whether columns for different series appear next to each other. | [enableSideBySidePlacement](https://ej2.syncfusion.com/vue/documentation/api/chart/#enablesidebysideplacement) |
| tabIndex | number | 1 | The tabIndex value determines the order in which the chart container receives focus during keyboard navigation. | [tabIndex](https://ej2.syncfusion.com/vue/documentation/api/chart/#tabindex) |

---

## Data Models

### SeriesModel
**Purpose:** Configuration options for each data series displayed in the chart.

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| dataSource | Object \| DataManager | — | Specifies the data source for the series (array of JSON objects or DataManager instance). | [dataSource](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/#datasource) |
| type | [ChartSeriesType](https://ej2.syncfusion.com/vue/documentation/api/chart/chartseriestype) | 'Column' | Defines the type of series (Line, Column, Area, Scatter, Bubble, etc.). | [type](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/#type) |
| name | string | — | A name for the series that appears in the legend. | [name](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/#name) |
| xName | string | — | The property name in the data source that contains x-axis values. | [xName](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/#xname) |
| yName | string | — | The property name in the data source that contains y-axis values. | [yName](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/#yname) |
| marker | [MarkerSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/markersettingsmodel/) | — | Marker options for the data points in the series. | [marker](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/#marker) |
| fill | string | — | The fill color of the series. | [fill](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/#fill) |
| width | number | — | The width of the series line or border. | [width](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/#width) |
| opacity | number | — | The opacity of the series. | [opacity](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/#opacity) |
| cornerRadius | [CornerRadiusModel](https://ej2.syncfusion.com/vue/documentation/api/chart/cornerradiusmodel) | — | The corner radius for column/bar series. | [cornerRadius](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/#cornerradius) |
| border | [BorderModel](https://ej2.syncfusion.com/vue/documentation/api/chart/bordermodel/) | — | Border options for the series elements. | [border](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/#border) |
| animation | [AnimationModel](https://ej2.syncfusion.com/vue/documentation/api/chart/animationmodel/) | — | Animation settings for the series. | [animation](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/#animation) |

**Full Reference:** [SeriesModel](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/)

### AxisModel
**Purpose:** Configuration options for chart axes (horizontal X-axis or vertical Y-axis).

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| valueType | [ValueType](https://ej2.syncfusion.com/vue/documentation/api/chart/valuetype) | - | Defines the type of axis (Double, DateTime, Category, Logarithmic, DateTimeCategory). | [valueType](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/#valuetype) |
| title | string | — | The title of the axis displayed at the center of the axis. | [title](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/#title) |
| labelFormat | string | — | Format for axis labels (e.g., 'n2' for two decimal places). | [labelFormat](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/#labelformat) |
| minimum | Object | — | The minimum value of the axis range. | [minimum](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/#minimum) |
| maximum | Object | — | The maximum value of the axis range. | [maximum](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/#maximum) |
| interval | number | — | The interval between axis labels and grid lines. | [interval](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/#interval) |
| visible | boolean | true | Determines whether the axis is visible. | [visible](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/#visible) |
| opposedPosition | boolean | false | Places the axis on the opposite side of the chart. | [opposedPosition](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/#opposedposition) |
| majorGridLines | [MajorGridLinesModel](https://ej2.syncfusion.com/vue/documentation/api/chart/majorgridlinesmodel/) | — | Configuration for major grid lines. | [majorGridLines](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/#majorgridlines) |
| majorTickLines | [MajorTickLinesModel](https://ej2.syncfusion.com/vue/documentation/api/chart/majorticklines/) | — | Configuration for major tick marks. | [majorTickLines](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/#majorticklines) |
| labelStyle | [FontModel](https://ej2.syncfusion.com/vue/documentation/api/chart/fontmodel/) | — | Font and style options for axis labels. | [labelStyle](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/#labelstyle) |
| border | [LabelBorderModel](https://ej2.syncfusion.com/vue/documentation/api/chart/labelbordermodel) | — | Border configuration for the axis. | [border](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/#border) |

**Full Reference:** [AxisModel](https://ej2.syncfusion.com/vue/documentation/api/chart/axismodel/)

### TooltipSettingsModel
**Purpose:** Configuration options for the chart tooltip that displays point details on hover.

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| enable | boolean | false | Enables or disables the tooltip feature. | [enable](https://ej2.syncfusion.com/vue/documentation/api/chart/tooltipsettingsmodel/#enable) |
| template | string \| Function | — | A template string or function to customize the tooltip content. | [template](https://ej2.syncfusion.com/vue/documentation/api/chart/tooltipsettingsmodel/#template) |
| format | string | — | Format for the tooltip text (e.g., '<b>${series.name}</b> : ${point.x} : ${point.y}'). | [format](https://ej2.syncfusion.com/vue/documentation/api/chart/tooltipsettingsmodel/#format) |
| shared | boolean | false | Displays multiple tooltips for multi-series charts. | [shared](https://ej2.syncfusion.com/vue/documentation/api/chart/tooltipsettingsmodel/#shared) |
| textStyle | [FontModel](https://ej2.syncfusion.com/vue/documentation/api/chart/fontmodel/) | — | Font and style for tooltip text. | [textStyle](https://ej2.syncfusion.com/vue/documentation/api/chart/tooltipsettingsmodel/#textstyle) |
| border | [BorderModel](https://ej2.syncfusion.com/vue/documentation/api/chart/bordermodel/) | — | Border configuration for the tooltip. | [border](https://ej2.syncfusion.com/vue/documentation/api/chart/tooltipsettingsmodel/#border) |
| opacity | number | — | Opacity of the tooltip. | [opacity](https://ej2.syncfusion.com/vue/documentation/api/chart/tooltipsettingsmodel/#opacity) |

**Full Reference:** [TooltipSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/tooltipsettingsmodel/)

### LegendSettingsModel
**Purpose:** Configuration options for the chart legend that identifies series and data.

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| visible | boolean | —  | Enables or disables the legend. | [visible](https://ej2.syncfusion.com/vue/documentation/api/chart/legendsettingsmodel/#visible) |
| position | [LegendPosition](https://ej2.syncfusion.com/vue/documentation/api/chart/legendposition) | —  | Specifies the legend position (Right, Left, Top, Bottom, Auto, Custom). | [position](https://ej2.syncfusion.com/vue/documentation/api/chart/legendsettingsmodel/#position) |
| background | string | — | The background color of the legend. | [background](https://ej2.syncfusion.com/vue/documentation/api/chart/legendsettingsmodel/#background) |
| border | [BorderModel](https://ej2.syncfusion.com/vue/documentation/api/chart/bordermodel/) | — | Border configuration for the legend. | [border](https://ej2.syncfusion.com/vue/documentation/api/chart/legendsettingsmodel/#border) |
| textStyle | [FontModel](https://ej2.syncfusion.com/vue/documentation/api/chart/fontmodel/) | — | Font and style for legend text. | [textStyle](https://ej2.syncfusion.com/vue/documentation/api/chart/legendsettingsmodel/#textstyle) |
| margin | [MarginModel](https://ej2.syncfusion.com/vue/documentation/api/chart/marginmodel/) | — | Margin around the legend. | [margin](https://ej2.syncfusion.com/vue/documentation/api/chart/legendsettingsmodel/#margin) |
| alignment | [Alignment](https://ej2.syncfusion.com/vue/documentation/api/chart/alignment) | 'Center' | Legend alignment (Near, Far, Center). | [alignment](https://ej2.syncfusion.com/vue/documentation/api/chart/legendsettingsmodel/#alignment) |
| mode | [LegendMode](https://ej2.syncfusion.com/vue/documentation/api/chart/legendmode) | 'Series' | Legend display mode (Series, Range, Gradient, Point). | [mode](https://ej2.syncfusion.com/vue/documentation/api/chart/legendsettingsmodel/#mode) |

**Full Reference:** [LegendSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/legendsettingsmodel/)

### CrosshairSettingsModel
**Purpose:** Configuration options for the crosshair feature that tracks data point values.

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| enable | boolean | false | Enables or disables the crosshair feature. | [enable](https://ej2.syncfusion.com/vue/documentation/api/chart/crosshairsettingsmodel/#enable) |
| horizontalLineColor | string | — | Specifies the color of the horizontal crosshair line. | [horizontalLineColor](https://ej2.syncfusion.com/vue/documentation/api/chart/crosshairsettingsmodel#horizontallinecolor) |
| verticalLineColor | string | —  | The color of the vertical crosshair line accepts values in hex and rgba as valid CSS color strings. | [verticalLineColor](https://ej2.syncfusion.com/vue/documentation/api/chart/crosshairsettingsmodel#verticallinecolor) |
| dashArray | string | — | Dash array for crosshair line styling. | [dashArray](https://ej2.syncfusion.com/vue/documentation/api/chart/crosshairsettingsmodel#dasharray) |
| lineType | [LineType](https://ej2.syncfusion.com/vue/documentation/api/chart/linetype) | — | Type of crosshair lines (Horizontal, Vertical, Both, None). | [lineType](https://ej2.syncfusion.com/vue/documentation/api/chart/crosshairsettingsmodel/#linetype) |

**Full Reference:** [CrosshairSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/crosshairsettingsmodel/)

### ZoomSettingsModel
**Purpose:** Configuration options for the zoom feature to enable data exploration.

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| enablePinchZooming | boolean | false | Enables zoom by pinch gesture on touch devices. | [enablePinchZooming](https://ej2.syncfusion.com/vue/documentation/api/chart/zoomsettingsmodel#enablepinchzooming) |
| enableMouseWheelZooming | boolean | false | Enables zoom by mouse wheel scroll. | [enableMouseWheelZooming](https://ej2.syncfusion.com/vue/documentation/api/chart/zoomsettingsmodel/#enablemousewheelzooming) |
| enableDeferredZooming | boolean | false | Defers zoom update until the selection is complete. | [enableDeferredZooming](https://ej2.syncfusion.com/vue/documentation/api/chart/zoomsettingsmodel/#enabledeferredzooming) |
| mode | [ZoomMode](https://ej2.syncfusion.com/vue/documentation/api/chart/zoommode) | — | Zoom mode (X, Y, or XY). | [mode](https://ej2.syncfusion.com/vue/documentation/api/chart/zoomsettingsmodel/#mode) |
| toolbarItems | [ToolbarItems[]](https://ej2.syncfusion.com/vue/documentation/api/chart/toolbaritems) | — | Toolbar items for zoom controls. | [toolbarItems](https://ej2.syncfusion.com/vue/documentation/api/chart/zoomsettingsmodel/#toolbaritems) |

**Full Reference:** [ZoomSettingsModel](https://ej2.syncfusion.com/vue/documentation/api/chart/zoomsettingsmodel/)

### MarginModel
**Purpose:** Configuration options for chart margins (space around the chart area).

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| left | number | — | Left margin in pixels. | [left](https://ej2.syncfusion.com/vue/documentation/api/chart/marginmodel/#left) |
| right | number | — | Right margin in pixels. | [right](https://ej2.syncfusion.com/vue/documentation/api/chart/marginmodel/#right) |
| top | number | — | Top margin in pixels. | [top](https://ej2.syncfusion.com/vue/documentation/api/chart/marginmodel/#top) |
| bottom | number | — | Bottom margin in pixels. | [bottom](https://ej2.syncfusion.com/vue/documentation/api/chart/marginmodel/#bottom) |

**Full Reference:** [MarginModel](https://ej2.syncfusion.com/vue/documentation/api/chart/marginmodel/)

### BorderModel
**Purpose:** Configuration options for borders on chart elements.

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| color | string | — | The color of the border. | [color](https://ej2.syncfusion.com/vue/documentation/api/chart/bordermodel/#color) |
| width | number | — | The width of the border line in pixels. | [width](https://ej2.syncfusion.com/vue/documentation/api/chart/bordermodel/#width) |

**Full Reference:** [BorderModel](https://ej2.syncfusion.com/vue/documentation/api/chart/bordermodel/)

### ChartAreaModel
**Purpose:** Configuration options for the chart plotting area.

| Property | Type | Default | Description | Link |
|----------|------|---------|-------------|------|
| background | string | — | Background color of the chart area. | [background](https://ej2.syncfusion.com/vue/documentation/api/chart/chartareamodel/#background) |
| border | [BorderModel](https://ej2.syncfusion.com/vue/documentation/api/chart/bordermodel/) | — | Border configuration for the chart area. | [border](https://ej2.syncfusion.com/vue/documentation/api/chart/chartareamodel/#border) |

**Full Reference:** [ChartAreaModel](https://ej2.syncfusion.com/vue/documentation/api/chart/chartareamodel/)

---

## Events

### load
**Parameters:** [ILoadedEventArgs](https://ej2.syncfusion.com/vue/documentation/api/chart/iloadedeventargs)

**Description:** Triggers before the chart loads, allowing customization and configuration before rendering.

**Example:**
```vue
<script setup>
const onLoad = (args) => {
  console.log('Chart is loading...', args);
};
</script>

<template>
  <ejs-chart @load="onLoad"></ejs-chart>
</template>
```

### loaded
**Parameters:** [ILoadedEventArgs](https://ej2.syncfusion.com/vue/documentation/api/chart/iloadedeventargs)

**Description:** Triggers after the chart has fully loaded and is ready for interaction.

**Example:**
```vue
<script setup>
const onLoaded = (args) => {
  console.log('Chart loaded successfully!', args);
};
</script>

<template>
  <ejs-chart @loaded="onLoaded"></ejs-chart>
</template>
```

### pointClick
**Parameters:** [IPointEventArgs](https://ej2.syncfusion.com/vue/documentation/api/chart/ipointeventargs)

**Description:** Triggers when a data point is clicked on the chart.

**Example:**
```vue
<script setup>
const onPointClick = (args) => {
  console.log('Point clicked:', args.point, 'Series:', args.series);
};
</script>

<template>
  <ejs-chart @pointClick="onPointClick" selectionMode="Point"></ejs-chart>
</template>
```

### pointMove
**Parameters:** [IPointEventArgs](https://ej2.syncfusion.com/vue/documentation/api/chart/ipointeventargs)

**Description:** Triggers when the mouse hovers over a data point.

**Example:**
```vue
<script setup>
const onPointMove = (args) => {
  console.log('Hovering over point:', args.point);
};
</script>

<template>
  <ejs-chart @pointMove="onPointMove"></ejs-chart>
</template>
```

### legendClick
**Parameters:** [ILegendClickEventArgs](https://ej2.syncfusion.com/vue/documentation/api/chart/ilegendclickeventargs)

**Description:** Triggers after clicking on a legend item.

**Example:**
```vue
<script setup>
const onLegendClick = (args) => {
  console.log('Legend item clicked:', args.legendText);
};
</script>

<template>
  <ejs-chart @legendClick="onLegendClick" :legendSettings="{ visible: true }"></ejs-chart>
</template>
```

### tooltipRender
**Parameters:** [ITooltipRenderEventArgs](https://ej2.syncfusion.com/vue/documentation/api/chart/itooltiprendereventargs)

**Description:** Triggers before the tooltip for a series is rendered, allowing customization of tooltip content.

**Example:**
```vue
<script setup>
const onTooltipRender = (args) => {
  args.tooltip.template = '<div>${point.x} : ${point.y}</div>';
};
</script>

<template>
  <ejs-chart @tooltipRender="onTooltipRender" :tooltip="{ enable: true }"></ejs-chart>
</template>
```

### beforeExport
**Parameters:** [IExportEventArgs](https://ej2.syncfusion.com/vue/documentation/api/chart/iexporteventargs)

**Description:** Triggers before the export process begins, allowing customization of export settings.

**Example:**
```vue
<script setup>
const onBeforeExport = (args) => {
  args.height = 200;
  console.log('Exporting Height:', args.height);
};
</script>

<template>
  <ejs-chart @beforeExport="onBeforeExport" :enableExport="true"></ejs-chart>
</template>
```

### afterExport
**Parameters:** IAfterExportEventArgs

**Description:** Triggers after the export is completed.

**Example:**
```vue
<script setup>
const onAfterExport = (args) => {
  console.log('Export completed successfully!');
};
</script>

<template>
  <ejs-chart @afterExport="onAfterExport"></ejs-chart>
</template>
```

### selectionComplete
**Parameters:** [ISelectionCompleteEventArgs](https://ej2.syncfusion.com/vue/documentation/api/chart/iselectioncompleteeventargs)

**Description:** Triggers after the selection is completed.

**Example:**
```vue
<script setup>
const onSelectionComplete = (args) => {
  console.log('Selection completed:', args.selectedDataValues);
};
</script>

<template>
  <ejs-chart @selectionComplete="onSelectionComplete" selectionMode="DragXY"></ejs-chart>
</template>
```

### resized
**Parameters:** [IResizeEventArgs](https://ej2.syncfusion.com/vue/documentation/api/chart/iresizeeventargs)

**Description:** Triggers after the chart is resized.

**Example:**
```vue
<script setup>
const onResized = (args) => {
  console.log('Chart resized to:', args.currentSize);
};
</script>

<template>
  <ejs-chart @resized="onResized"></ejs-chart>
</template>
```

### animationComplete
**Parameters:** [IAnimationCompleteEventArgs](https://ej2.syncfusion.com/vue/documentation/api/chart/ianimationcompleteeventargs)

**Description:** Triggers after the animation for the series is completed.

**Example:**
```vue
<script setup>
const onAnimationComplete = (args) => {
  console.log('Animation completed for series:', args.series);
};
</script>

<template>
  <ejs-chart @animationComplete="onAnimationComplete" :enableAnimation="true"></ejs-chart>
</template>
```

---

## Methods

### export()
**Signature:** `export(type: [ExportType](https://ej2.syncfusion.com/vue/documentation/api/chart/exporttype), fileName: string): void`

**Return:** void

**Description:** Exports the chart in the specified format (PNG, JPEG, PDF, SVG, XLSX, CSV). See [enableExport](#export--accessibility) property.

**Example:**
```vue
<script setup>
import { Export } from "@syncfusion/ej2-vue-charts";

const exportChart = () => {
  let chart1 = document.getElementById("container").ej2_instances[0];
  chart1.exportModule.export('PDF', 'chart');
};

provide('chart',  [Export]);
</script>

<template>
  <ejs-chart ref="chartRef"></ejs-chart>
  <button @click="exportChart">Export to PDF</button>
</template>
```

### print()
**Signature:** `print(id?: string[] | string | Element): void`

**Return:** void

**Description:** Prints the chart or specified element.

**Example:**
```vue
<script setup>
import { ref } from 'vue';

const chartRef = ref(null);

const printChart = () => {
  chartRef.value.print();
};
</script>

<template>
  <ejs-chart ref="chartRef"></ejs-chart>
  <button @click="printChart">Print Chart</button>
</template>
```

### addSeries()
**Signature:** `addSeries(seriesCollection: [SeriesModel[]](https://ej2.syncfusion.com/vue/documentation/api/chart/seriesmodel/)): void`

**Return:** void

**Description:** Adds a new series to the chart dynamically. See [series](#data) property and [SeriesModel](#seriesmodel) data model.

**Example:**
```vue
<script setup>
import { ref } from 'vue';

const chartRef = ref(null);

const addNewSeries = () => {
  const newSeries = {
    type: 'Line',
    dataSource: [{ x: 'Jan', y: 45 }, { x: 'Feb', y: 50 }],
    xName: 'x',
    yName: 'y',
    name: 'New Series'
  };
  chartRef.value.addSeries([newSeries]);
};
</script>

<template>
  <ejs-chart ref="chartRef"></ejs-chart>
  <button @click="addNewSeries">Add Series</button>
</template>
```

### removeSeries()
**Signature:** `removeSeries(index: number): void`

**Return:** void

**Description:** Removes a series from the chart by index.

**Example:**
```vue
<script setup>
import { ref } from 'vue';

const chartRef = ref(null);

const removeFirstSeries = () => {
  chartRef.value.removeSeries(0);
};
</script>

<template>
  <ejs-chart ref="chartRef"></ejs-chart>
  <button @click="removeFirstSeries">Remove First Series</button>
</template>
```

### clearSeries()
**Signature:** `clearSeries(): void`

**Return:** void

**Description:** Clears all series from the chart.

**Example:**
```vue
<script setup>
import { ref } from 'vue';

const chartRef = ref(null);

const clearAllSeries = () => {
  chartRef.value.clearSeries();
};
</script>

<template>
  <ejs-chart ref="chartRef"></ejs-chart>
  <button @click="clearAllSeries">Clear All Series</button>
</template>
```

### hideTooltip()
**Signature:** `hideTooltip(): void`

**Return:** void

**Description:** Hides the tooltip displayed on the chart.

**Example:**
```vue
<script setup>
import { ref } from 'vue';

const chartRef = ref(null);

const hideTooltip = () => {
  chartRef.value.hideTooltip();
};
</script>

<template>
  <ejs-chart ref="chartRef" :tooltip="{ enable: true }"></ejs-chart>
  <button @click="hideTooltip">Hide Tooltip</button>
</template>
```

### showTooltip()
**Signature:** `showTooltip(x: number | string | Date, y: number, isPoint?: boolean): void`

**Return:** void

**Description:** Displays a tooltip for the data points. See [tooltip](#tooltips--crosshair) property and [TooltipSettingsModel](#tooltipsettingsmodel) data model.

**Example:**
```vue
<script setup>
import { ref } from 'vue';

const chartRef = ref(null);

const showTooltip = () => {
  chartRef.value.showTooltip(10, 20, true);
};
</script>

<template>
  <ejs-chart ref="chartRef"></ejs-chart>
  <button @click="showTooltip">Show Tooltip</button>
</template>
```

### destroy()
**Signature:** `destroy(): void`

**Return:** void

**Description:** Destroys the chart widget and removes it from the DOM.

**Example:**
```vue
<script setup>
import { ref } from 'vue';

const chartRef = ref(null);

const destroyChart = () => {
  chartRef.value.destroy();
};
</script>

<template>
  <ejs-chart ref="chartRef"></ejs-chart>
  <button @click="destroyChart">Destroy Chart</button>
</template>
```

---

## Enums

### ChartSeriesType
Defines the available chart series types:

- **Line** — Renders a line series
- **Column** — Renders a column chart
- **Area** — Renders an area chart
- **Bar** — Renders a bar chart
- **Scatter** — Renders a scatter plot
- **Bubble** — Renders a bubble chart
- **Candle** — Renders a candle stick chart
- **Hilo** — Renders a hilo chart
- **HiloOpenClose** — Renders the HiloOpenClose series
- **Pie** — Renders a pie chart
- **StackingColumn100** — Renders a 100% stacked column series
- **StackingColumn** — Renders a stacked column series
- **StackingLine** — Renders a stacked line series
- **StackingArea** — Renders a stacked area series
- **StepLine** — Renders a step line series
- **SplineArea** — Renders a spline area chart
- **Spline** — Renders a spline chart
- **RangeArea** — Renders a range area chart
- **Waterfall** — Renders a waterfall chart
- **Pareto** — Renders a Pareto chart
- **BoxAndWhisker** — Renders a box and whisker chart
- **Histogram** — Renders a histogram

### SelectionMode
Defines how data points or series can be selected:

- **None** — Disables selection
- **Series** — Selects an entire series
- **Point** — Selects individual data points
- **Cluster** — Selects a group of points in a cluster
- **DragXY** — Allows selection by dragging along both axes
- **DragX** — Allows selection by dragging along the X-axis
- **DragY** — Allows selection by dragging along the Y-axis
- **Lasso** — Allows selection by dragging with free form

### HighlightMode
Defines how data points are highlighted on hover:

- **None** — No highlighting
- **Series** — Highlights the entire series
- **Point** — Highlights a single data point
- **Cluster** — Highlights a cluster of points

### LegendPosition
Defines the position of the legend:

- **Auto** — Places the legend based on the area type
- **Right** — Legend appears on the right side
- **Left** — Legend appears on the left side
- **Top** — Legend appears at the top
- **Bottom** — Legend appears at the bottom
- **Custom** — Displays the legend based on the given x and y value

### ChartTheme
Defines available chart themes:

- **Fabric** — Material design theme
- **FabricDark** — Dark material theme
- **Bootstrap4** — Bootstrap 4 theme
- **Bootstrap** — Bootstrap 3 theme
- **BootstrapDark** — Dark Bootstrap theme
- **HighContrastLight** — High contrast light theme
- **HighContrast** — High contrast theme
- **Tailwind** — Tailwind CSS theme
- **TailwindDark** — Dark Tailwind theme
- **Bootstrap5** — Bootstrap 5 theme
- **Bootstrap5Dark** — Dark Bootstrap 5 theme
- **Fluent** — Fluent design theme
- **FluentDark** — Dark Fluent theme
- **Material3** — Material Design 3 theme
- **Material3Dark** — Dark Material Design 3 theme
- **Material** — Material Design theme
- **MaterialDark** — Dark Material Design theme

---

## Child Directives

### SeriesCollectionDirective / e-series-collection
**Purpose:** Container directive for defining multiple series within a chart.

**Properties:**
- None (container for series definitions)

**Example:**
```vue
<template>
  <ejs-chart>
    <e-series-collection>
      <e-series :dataSource="data1" type="Column" xName="x" yName="y" name="Series 1"></e-series>
      <e-series :dataSource="data2" type="Column" xName="x" yName="y" name="Series 2"></e-series>
    </e-series-collection>
  </ejs-chart>
</template>
```

### SeriesDirective / e-series
**Purpose:** Defines a single data series within the chart.

**Properties:**
- `dataSource` — Data source for the series
- `type` — Type of series (Column, Line, Area, etc.)
- `xName` — Property name for X values
- `yName` — Property name for Y values
- `name` — Name of the series for legend

**Example:**
```vue
<template>
  <ejs-chart>
    <e-series-collection>
      <e-series :dataSource="chartData" type="Line" xName="x" yName="y" name="Sales"></e-series>
    </e-series-collection>
  </ejs-chart>
</template>
```

---

## Modules

### LineSeries
**Purpose:** Module for rendering line series in the chart.

**Registration:**
```vue
import { LineSeries } from '@syncfusion/ej2-vue-charts';
import { provide, ref } from "vue";

// In Composition API
const chart = ref(null);
provide('chart', [LineSeries]);
```

### ColumnSeries
**Purpose:** Module for rendering column series in the chart.

**Registration:**
```vue
import { ColumnSeries } from '@syncfusion/ej2-vue-charts';
provide('chart', [ColumnSeries]);
```

### AreaSeries
**Purpose:** Module for rendering area series in the chart.

**Registration:**
```vue
import { AreaSeries } from '@syncfusion/ej2-vue-charts';
provide('chart', [AreaSeries]);
```

### BarSeries
**Purpose:** Module for rendering bar series in the chart.

**Registration:**
```vue
import { BarSeries } from '@syncfusion/ej2-vue-charts';
provide('chart', [BarSeries]);
```

### Legend
**Purpose:** Module for adding legend functionality to the chart.

**Registration:**
```vue
import { Legend } from '@syncfusion/ej2-vue-charts';
provide('chart', [Legend]);
```

### Tooltip
**Purpose:** Module for displaying tooltips on data points.

**Registration:**
```vue
import { Tooltip } from '@syncfusion/ej2-vue-charts';
provide('chart', [Tooltip]);
```

### Category
**Purpose:** Module for category axis support in the chart.

**Registration:**
```vue
import { Category } from '@syncfusion/ej2-vue-charts';
provide('chart', [Category]);
```

### DateTime
**Purpose:** Module for date-time axis support in the chart.

**Registration:**
```vue
import { DateTime } from '@syncfusion/ej2-vue-charts';
provide('chart', [DateTime]);
```

### Export
**Purpose:** Module for exporting the chart to various formats.

**Registration:**
```vue
import { Export } from '@syncfusion/ej2-vue-charts';
provide('chart', [Export]);
```

### Crosshair
**Purpose:** Module for crosshair functionality in the chart.

**Registration:**
```vue
import { Crosshair } from '@syncfusion/ej2-vue-charts';
provide('chart', [Crosshair]);
```

### Zoom
**Purpose:** Module for zoom functionality in the chart.

**Registration:**
```vue
import { Zoom } from '@syncfusion/ej2-vue-charts';
provide('chart', [Zoom]);
```

---


## Common Usage Patterns

### Pattern 1: Access Chart Instance
```vue
<script setup>
import { ref } from 'vue';

const chartRef = ref(null);

const getChartInstance = () => {
  return chartRef.value.ej2_instances[0];
};

const exportChart = () => {
  const chart = getChartInstance();
  chart.exportModule.export('PNG', 'my-chart.png');
};
</script>

<template>
  <ejs-chart ref="chartRef">
    <!-- series and config -->
  </ejs-chart>
  <ejs-button @click="exportChart">Export</ejs-button>
</template>
```

### Pattern 2: Dynamic Series Update
```typescript
const addNewSeries = (newSeriesData) => {
  const chart = getChartInstance();
  chart.addSeries([{
    dataSource: newSeriesData,
    type: 'Line',
    xName: 'x',
    yName: 'y'
  }]);
};

const removeSeries = (index) => {
  const chart = getChartInstance();
  chart.removeSeries(index);
};
```

### Pattern 3: Handle Events
```vue
<ejs-chart
  :seriesRender="onSeriesRender"
  :pointRender="onPointRender"
  :tooltipRender="onTooltipRender"
  :legendClick="onLegendClick"
>
</ejs-chart>

<script setup>
const onSeriesRender = (args) => {
  console.log('Series rendering:', args.series.name);
};

const onPointRender = (args) => {
  if (args.point.y > 50) {
    args.fill = '#FF0000'; // Color high values
  }
};

const onTooltipRender = (args) => {
  args.text = `Value: ${args.data.pointY.toFixed(2)}`;
};

const onLegendClick = (args) => {
  console.log('Legend clicked:', args.series.name);
};
</script>
```

```

---

## Additional Resources

- [Official Syncfusion Chart Documentation](https://ej2.syncfusion.com/vue/documentation/chart/)
- [Official Chart API Reference](https://ej2.syncfusion.com/vue/documentation/api/chart/index-default)
- [Syncfusion Community Forum](https://www.syncfusion.com/forums)
- [Chart Live Demos](https://ej2.syncfusion.com/vue/demos/#/material/chart/local-data.html)
