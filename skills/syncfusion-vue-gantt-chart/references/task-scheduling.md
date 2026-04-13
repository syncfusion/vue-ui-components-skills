# Task Scheduling

Configure how the Gantt Chart calculates and displays task dates, durations.

## Table of Contents
- [Scheduling Modes](#scheduling-modes)
  - [Custom Mode (per-task scheduling)](#custom-mode-per-task-scheduling)
  - [Validate predecessors in Manual mode](#validate-predecessors-in-manual-mode)
- [taskFields Mapping](#taskfields-mapping)
- [Duration Units](#duration-units)
  - [Global duration unit](#global-duration-unit)
  - [Map per-task duration unit from data source](#map-per-task-duration-unit-from-data-source)
  - [Inline duration unit in duration field](#inline-duration-unit-in-duration-field)
- [Unscheduled Tasks](#unscheduled-tasks)
- [Work Time and Weekends](#work-time-and-weekends)
  - [Working time range](#working-time-range)
  - [Per-day working hours (weekWorkingTime)](#per-day-working-hours-weekworkingtime)
  - [Non-working days / Weekend](#non-working-days--weekend)
  - [Include weekends as working days](#include-weekends-as-working-days)
- [Baselines](#baselines)

## Scheduling Modes

Control whether the Gantt auto-calculates dates or lets the user set them manually via `taskMode`.

| Mode | Behavior |
|---|---|
| `Auto` (default) | Dates validated based on working time, holidays, predecessors |
| `Manual` | User sets all dates freely; Gantt does not auto-adjust |
| `Custom` | Per-task mode — mix auto and manual tasks using a data field |

```vue
<ejs-gantt :dataSource="data" :taskFields="taskFields" taskMode="Auto" height="450px"></ejs-gantt>
```

### Custom Mode (per-task scheduling)

Map a boolean field in your data to `taskFields.manual` to control each task individually:

```js
const taskFields = {
  id: 'TaskID',
  name: 'TaskName',
  startDate: 'StartDate',
  duration: 'Duration',
  manual: 'isManual'   // true = manual task, false/undefined = auto task
};
```

> In `Manual` mode, dates are **not** validated against dependencies, holidays, weekends, or working time. All dates are taken as-is from the data source.

### Validate predecessors in Manual mode

Use `validateManualTasksOnLinking` to selectively enforce predecessor-based date validation even in `Manual` mode:

```vue
<ejs-gantt taskMode="Manual" :validateManualTasksOnLinking="true" ...></ejs-gantt>
```

When `true`, tasks in Manual mode will still auto-adjust their start dates based on predecessor relationships, while all other scheduling constraints (holidays, working time) remain ignored.

## taskFields Mapping

`taskFields` tells the Gantt which data source properties map to which Gantt concepts. All fields are optional except `id` and `name`.

```js
const taskFields = {
  id: 'TaskID',               // required — unique identifier
  name: 'TaskName',           // required — display name
  startDate: 'StartDate',     // task start
  endDate: 'EndDate',         // task end (alternative to duration)
  duration: 'Duration',       // number of working days/hours
  progress: 'Progress',       // 0–100 percent complete
  dependency: 'Predecessor',  // task dependency string (e.g. "2FS")
  parentID: 'ParentID',       // for self-referential flat data
  child: 'subtasks',          // for hierarchical nested data (mutually exclusive with parentID)
  resourceInfo: 'resources',  // resource assignment array
  manual: 'isManual',         // for Custom scheduling mode
  work: 'Work',               // work hours field
  type: 'TaskType',           // task type (FixedWork, FixedDuration, FixedUnit)
  baselineStartDate: 'BaselineStartDate',
  baselineEndDate: 'BaselineEndDate',
  baselineDuration: "BaselineDuration",
  hasChildMapping: 'isParent',  // for load-on-demand
  notes: 'Notes'
};
```

## Duration Units

The default duration unit is `day`. Change it globally or per-task.

### Global duration unit

```vue
<ejs-gantt durationUnit="hour" :taskFields="taskFields" ...></ejs-gantt>
```

Supported values: `day`, `hour`, `minute`.

### Map per-task duration unit from data source

Use `taskFields.durationUnit` to map a data field that holds each task's unit:

```js
const taskFields = {
  id: 'TaskID',
  name: 'TaskName',
  startDate: 'StartDate',
  duration: 'Duration',
  durationUnit: 'DurationUnit',   // maps field containing 'day' | 'hour' | 'minute'
  child: 'subtasks'
};
```

```js
// Data source example
{ TaskID: 2, TaskName: 'Design', Duration: 3, DurationUnit: 'day' }
{ TaskID: 3, TaskName: 'Review', Duration: 12, DurationUnit: 'hour' }
```

> Tasks without a `DurationUnit` value inherit the global `durationUnit` property (default: `day`).

### Inline duration unit in duration field

You can also embed the unit directly in the duration string value (no space between number and unit):

```js
{ TaskID: 2, Duration: '3days' }
{ TaskID: 3, Duration: '12hours' }
{ TaskID: 4, Duration: '1800minutes' }
```

> The edit type of the duration column in Gantt is `string` to support duration values with embedded units.

## Unscheduled Tasks

Tasks with missing start, end, or duration are rendered as unscheduled. Enable with:

```vue
<ejs-gantt :allowUnscheduledTasks="true" :editSettings="editSettings" ...></ejs-gantt>

<script setup>
import { provide } from 'vue';
import { Edit } from '@syncfusion/ej2-vue-gantt';
provide('gantt', [Edit]);
const editSettings = { allowEditing: true };
</script>
```

### Unscheduled task types

| Type | Data provided | Rendering |
|---|---|---|
| Start date only | `startDate` only | Bar from start, extends to project end |
| End date only | `endDate` only | Bar ending at end date |
| Duration only | `duration` only | Bar of that duration from project start |
| Milestone | `duration: 0` (no start/end) | Diamond shape at project start |

```js
// Start date only
{ TaskID: 2, TaskName: 'Site location', Duration: 3, Progress: 50 }

// End date only
{ TaskID: 4, TaskName: 'Soil approval', EndDate: new Date('04/08/2019'), Progress: 50 }

// Start date only
{ TaskID: 3, TaskName: 'Soil test', StartDate: new Date('04/02/2019'), Progress: 50 }

// Milestone (duration = 0)
{ TaskID: 8, TaskName: 'Estimation approval', Duration: 0, Progress: 50 }
```

> When `allowUnscheduledTasks` is `false` (default), Gantt auto-calculates missing dates using a default duration of `1` and the project start date.

## Work Time and Weekends

### Working time range

Configure working hours that apply to all days using `dayWorkingTime`. Inject `DayMarkers` module:

```vue
<ejs-gantt
  :dayWorkingTime="dayWorkingTime"
  :highlightWeekends="true"
  :timelineSettings="timelineSettings"
  :editSettings="editSettings"
  ...
></ejs-gantt>

<script setup>
import { provide } from 'vue';
import { Edit, DayMarkers } from '@syncfusion/ej2-vue-gantt';
provide('gantt', [DayMarkers, Edit]);

const dayWorkingTime = [{ from: 9, to: 18 }];   // 9 AM to 6 PM
const timelineSettings = { timelineViewMode: 'Day' };
const editSettings = { allowTaskbarEditing: true };
</script>
```

> Individual tasks can lie between any time within the defined working time range. Days not listed in `weekWorkingTime` fall back to `dayWorkingTime`.

### Per-day working hours (weekWorkingTime)

Use `weekWorkingTime` to define different working hours for specific days of the week. This overrides `dayWorkingTime` for the listed days and is useful for schedules where working hours vary by day (e.g. shorter Fridays).

```vue
<ejs-gantt
  :dayWorkingTime="dayWorkingTime"
  :weekWorkingTime="weekWorkingTime"
  :timelineSettings="timelineSettings"
  ...
></ejs-gantt>

<script setup>
import { provide } from 'vue';
import { DayMarkers } from '@syncfusion/ej2-vue-gantt';
provide('gantt', [DayMarkers]);

// Default working hours for all days
const dayWorkingTime = [{ from: 9, to: 17 }];

// Override specific days with different hours
const weekWorkingTime = [
        { dayOfWeek: 'Monday',  timeRange: [{ from: 10, to: 18 }] },
        { dayOfWeek: 'Tuesday', timeRange: [{ from: 10, to: 18 }] }
];

const timelineSettings = { timelineViewMode: 'Day' };
</script>
```

**`weekWorkingTime` item properties:**

| Property | Type | Description |
|---|---|---|
| `dayOfWeek` | string | Day name: `'Monday'`, `'Tuesday'`, … `'Sunday'` |
| `workingTime` | `{ from, to }[]` | Working hour ranges for those days |

> Days not listed in `weekWorkingTime` use `dayWorkingTime` as the fallback.

### Non-working days / Weekend

Define which days are working days using `workWeek`. Inject `DayMarkers` module:

```vue
<ejs-gantt :workWeek="workWeek" :highlightWeekends="true" ...></ejs-gantt>

<script setup>
import { provide } from 'vue';
import { DayMarkers } from '@syncfusion/ej2-vue-gantt';
provide('gantt', [DayMarkers]);

// Only Sunday–Thursday are working days
const workWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday'];
</script>
```

> By default, Saturdays and Sundays are non-working days.

### Include weekends as working days

Set `includeWeekend: true` to count Saturday and Sunday in task duration calculations:

```vue
<ejs-gantt :includeWeekend="true" ...></ejs-gantt>
```

> To show/hide weekends in the timeline header, use `timelineSettings.showWeekend`.

## Baselines

Render baseline bars to compare planned vs actual dates:

```vue
<ejs-gantt :renderBaseline="true" baselineColor="red" ...></ejs-gantt>
```

Map baseline fields in `taskFields`:
```js
const taskFields = {
  // ... standard fields
  baselineStartDate: 'BaselineStartDate',
  baselineEndDate: 'BaselineEndDate',
  baselineDuration: "BaselineDuration",
};
```

Data example:
```js
{ TaskID: 2, TaskName: 'Design', StartDate: new Date('04/05/2019'), Duration: 3,
  BaselineStartDate: new Date('04/04/2019'), BaselineEndDate: new Date('04/08/2019'), BaselineDuration: '5' }
```
