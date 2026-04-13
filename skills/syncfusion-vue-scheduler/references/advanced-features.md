# Advanced Features

## Table of Contents
- [Virtual Scrolling](#virtual-scrolling)
- [Lazy Loading](#lazy-loading)
- [Exporting](#exporting)
- [Printing](#printing)
- [State Persistence](#state-persistence)
- [Row Auto Height](#row-auto-height)
- [Event Template](#event-template)
- [Quick Info Template](#quick-info-template)
- [Block Time Slots](#block-time-slots)
- [Tooltip](#tooltip)
- [Inline Editing](#inline-editing)
- [Responsive Design](#responsive-design)
- [Recurrence Editor](#recurrence-editor)
- [Calendar Mode](#calendar-mode)
- [Working Days Configuration](#working-days-configuration)
- [Scheduler Styling and Theming](#scheduler-styling-and-theming)
- [Performance Tips](#performance-tips)
- [Best Practices](#best-practices)

## Virtual Scrolling

Enable for large datasets in Agenda and Timeline views:

```vue
<template>
  <ejs-schedule :eventSettings="eventSettings">
    <e-views>
      <e-view 
        option="Agenda" 
        :allowVirtualScrolling="true">
      </e-view>
      <e-view 
        option="TimelineMonth" 
        :allowVirtualScrolling="true">
      </e-view>
    </e-views>
  </ejs-schedule>
</template>
```

**Benefits**:
- Improved performance with thousands of events
- Smooth scrolling experience
- Reduced initial load time

## Lazy Loading

Enable lazy loading to fetch events on-demand from the server as users scroll. This is ideal for very large datasets with resource grouping enabled:

```vue
<template>
  <ejs-schedule 
    :eventSettings="eventSettings"
    :group="group">
    <e-views>
      <e-view 
        option="TimelineMonth" 
        :enableLazyLoad="true"
        :allowVirtualScrolling="true">
      </e-view>
    </e-views>
    <e-resources>
      <e-resource 
        field="ResourceId" 
        title="Resource" 
        name="Resources" 
        :dataSource="resourceDataSource"
        textField="text" 
        idField="id">
      </e-resource>
    </e-resources>
  </ejs-schedule>
</template>

<script setup>
import { provide, ref } from "vue";
import { DataManager, WebApiAdaptor } from '@syncfusion/ej2-data';
import { ScheduleComponent as EjsSchedule, ViewDirective as EView, ViewsDirective as EViews, 
         TimelineMonth, ResourcesDirective as EResources, ResourceDirective as EResource } from '@syncfusion/ej2-vue-schedule';

const eventSettings = {
  dataSource: new DataManager({
    url: 'url',
    adaptor: new WebApiAdaptor(),
    crossDomain: true
  }),
  fields: {
    id: 'Id',
    subject: { name: 'Subject', title: 'Summary' },
    startTime: { name: 'StartTime', title: 'From' },
    endTime: { name: 'EndTime', title: 'To' },
    resourceIdField: 'ResourceId'
  }
};

const group = {
  resources: ['Resources']
};

const resourceDataSource = [
  { id: 1, text: 'Resource 1' },
  { id: 2, text: 'Resource 2' },
  { id: 3, text: 'Resource 3' }
];

provide('schedule', [TimelineMonth]);
</script>
```

### Vue 2 Options API Example:

```vue
<script>
export default {
  data() {
    return {
      eventSettings: {
        dataSource: new DataManager({
          url: 'url',
          adaptor: new WebApiAdaptor(),
          crossDomain: true
        }),
        fields: {
          id: 'Id',
          subject: { name: 'Subject', title: 'Summary' },
          startTime: { name: 'StartTime', title: 'From' },
          endTime: { name: 'EndTime', title: 'To' },
          resourceIdField: 'ResourceId'
        }
      },
      group: {
        resources: ['Resources']
      }
    }
  }
}
</script>
```

### Server-Side Implementation (C# ASP.NET Core):

```csharp
[HttpGet]
[EnableQuery]
[Route("api/VirtualEventData")]
public IActionResult GetData([FromQuery] VirtualEventParams param)
{
    IQueryable<EventData> query = dbContext.Events;
    
    // Filter by ResourceId if provided
    if (!string.IsNullOrEmpty(param.ResourceId))
    {
        string[] resourceIds = param.ResourceId.Split(',');
        query = query.Where(data => resourceIds.Contains(data.ResourceId.ToString()));
    }
    
    // Filter by date range if needed
    if (param.StartDate.HasValue)
    {
        query = query.Where(data => data.StartTime >= param.StartDate);
    }
    if (param.EndDate.HasValue)
    {
        query = query.Where(data => data.EndTime <= param.EndDate);
    }
    
    return Ok(query.ToList());
}

public class VirtualEventParams
{
    public DateTime? StartDate { get; set; }
    public DateTime? EndDate { get; set; }
    public string ResourceId { get; set; }
}

public class EventData
{
    public int Id { get; set; }
    public string Subject { get; set; }
    public DateTime StartTime { get; set; }
    public DateTime EndTime { get; set; }
    public int ResourceId { get; set; }
    public string Location { get; set; }
    public string Description { get; set; }
}
```

**Lazy Loading Characteristics**:
- Fetches events on-demand as users scroll through resources
- Works only with resource grouping enabled
- Not supported in MonthAgenda, Year, and TimelineYear (Horizontal) views
- Significantly improves performance with thousands of events
- Reduces initial load time and memory usage

## Exporting

Export scheduler events to Excel (`.xlsx`, `.csv`) and ICS calendar files:

### Excel Export with Custom Fields:

```vue
<template>
  <button @click="exportToExcel">Export to Excel</button>
  
  <ejs-schedule ref="scheduleObj" :eventSettings="eventSettings">
  </ejs-schedule>
</template>

<script setup>
import { ref, provide } from "vue";
import { ExcelExport } from '@syncfusion/ej2-vue-schedule';

const scheduleObj = ref(null);

provide('schedule', [ExcelExport]);

const exportToExcel = () => {
  const exportOptions = {
    fileName: 'SchedulerEvents',
    fields: ['Id', 'Subject', 'StartTime', 'EndTime', 'Location'],
    fieldsInfo: [
      { name: 'Subject', text: 'Event Title' },
      { name: 'StartTime', text: 'Start Date' },
      { name: 'EndTime', text: 'End Date' },
      { name: 'Location', text: 'Venue' }
    ]
  };
  scheduleObj.value.exportToExcel(exportOptions);
};
</script>
```

### Export with Custom Data:

```vue
<script setup>
const exportCustomEvents = () => {
  const customData = [
    {
      Id: 1,
      Subject: 'Conference',
      StartTime: new Date(2024, 0, 15, 9, 0),
      EndTime: new Date(2024, 0, 15, 11, 0),
      Location: 'Hall A'
    },
    {
      Id: 2,
      Subject: 'Training',
      StartTime: new Date(2024, 0, 15, 14, 0),
      EndTime: new Date(2024, 0, 15, 16, 0),
      Location: 'Hall B'
    }
  ];
  
  const exportOptions = {
    customData: customData,
    fileName: 'CustomEvents'
  };
  
  scheduleObj.value.exportToExcel(exportOptions);
};
</script>
```

### CSV Export with Custom Separator:

```vue
<script setup>
const exportToCSV = () => {
  const exportOptions = {
    exportType: 'csv',
    fileName: 'events',
    separator: ';'  // Use semicolon instead of comma
  };
  
  scheduleObj.value.exportToExcel(exportOptions);
};
</script>
```

### ICS Calendar Export:

```vue
<template>
  <button @click="exportToICS">Export to ICS</button>
  
  <ejs-schedule ref="scheduleObj" :eventSettings="eventSettings">
  </ejs-schedule>
</template>

<script setup>
import { ref, provide } from "vue";
import { ICalendarExport } from '@syncfusion/ej2-vue-schedule';

const scheduleObj = ref(null);

provide('schedule', [ICalendarExport]);

const exportToICS = () => {
  // Export with default name 'Calendar.ics'
  scheduleObj.value.exportToICalendar();
  
  // OR export with custom name
  // scheduleObj.value.exportToICalendar('MySchedule');
};
</script>
```

### ICS Import:

```vue
<template>
  <input 
    type="file" 
    accept=".ics" 
    @change="handleFileSelect">
  
  <ejs-schedule ref="scheduleObj">
  </ejs-schedule>
</template>

<script setup>
import { ref, provide } from "vue";
import { ICalendarImport } from '@syncfusion/ej2-vue-schedule';

const scheduleObj = ref(null);

provide('schedule', [ICalendarImport]);

const handleFileSelect = (event) => {
  const file = event.target.files[0];
  if (file) {
    scheduleObj.value.importICalendar(file);
  }
};
</script>
```

### Customize Export Before Download:

```vue
<script setup>
const onExcelExport = (args) => {
  const worksheet = args.worksheets[0];
  
  // Add custom header
  worksheet.rows.unshift({
    index: 1,
    cells: [{
      index: 1,
      value: 'Event Schedule Report',
      colSpan: worksheet.columns.length,
      style: {
        bold: true,
        fontSize: 18,
        hAlign: 'Center',
        fill: { color: '#1E90FF' },
        color: '#FFFFFF'
      }
    }]
  });
  
  // Update row indices
  worksheet.rows.forEach((row, idx) => {
    row.index = idx + 1;
  });
};
</script>
```

**Export Options**:
- `.xlsx` format (default)
- `.csv` format with custom separator
- `.ics` calendar format (for compatibility with Google Calendar, Outlook)
- Custom fields selection
- Field name customization
- Include/exclude recurring event occurrences

## Printing

Print scheduler:

```vue
<script setup>
import { Print } from '@syncfusion/ej2-vue-schedule';

provide('schedule', [Print]);

const printScheduler = () => {
  scheduleObj.value.print();
};
</script>
```

## State Persistence

Save and restore scheduler state:

```vue
<template>
  <ejs-schedule 
    :enablePersistence="true"
    id="schedule">
  </ejs-schedule>
</template>
```

**Persisted State**:
- Current view
- Selected date
- Scroll position
- Resource selection

## Row Auto Height

Auto-adjust row height based on overlapping events. Works on Timeline views, Month view, and with resource grouping:

```vue
<template>
  <ejs-schedule 
    :rowAutoHeight="true"
    :eventSettings="eventSettings">
    <e-views>
      <e-view option="TimelineMonth"></e-view>
      <e-view option="TimelineWeek"></e-view>
      <e-view option="Month"></e-view>
    </e-views>
  </ejs-schedule>
</template>

<script setup>
import { provide } from "vue";
import { ScheduleComponent as EjsSchedule, ViewDirective as EView, 
         ViewsDirective as EViews, TimelineMonth, TimelineViews, Month } from '@syncfusion/ej2-vue-schedule';
import { scheduleData } from './datasource.js';

const eventSettings = { dataSource: scheduleData };

provide('schedule', [TimelineMonth, TimelineViews, Month]);
</script>
```

### With Multiple Resources:

```vue
<template>
  <ejs-schedule 
    :rowAutoHeight="true"
    :group="group"
    :eventSettings="eventSettings">
    <e-views>
      <e-view option="TimelineWeek"></e-view>
    </e-views>
    <e-resources>
      <e-resource 
        field="ResourceId" 
        title="Room" 
        name="Rooms" 
        :dataSource="roomDataSource"
        textField="text" 
        idField="id">
      </e-resource>
    </e-resources>
  </ejs-schedule>
</template>

<script setup>
const group = {
  resources: ['Rooms']
};

const roomDataSource = [
  { id: 1, text: 'Room A' },
  { id: 2, text: 'Room B' },
  { id: 3, text: 'Room C' }
];
</script>
```

### Remove Whitespace in Auto-Height Rows:

```vue
<template>
  <ejs-schedule 
    :rowAutoHeight="true"
    :eventSettings="eventSettings">
  </ejs-schedule>
</template>

<script setup>
const eventSettings = {
  dataSource: scheduleData,
  ignoreWhitespace: true  // Appointments fill entire cell
};
</script>
```

**Features**:
- Dynamically expands row height for overlapping events
- Applicable to Timeline and Month views
- Works with resource grouping (each resource row expands independently)
- `ignoreWhitespace` property removes bottom padding when enabled
- Eliminates need for "+n more" indicators

## Event Template

Customize event appearance:

```vue
<template>
  <ejs-schedule :eventSettings="eventSettings">
    <template v-slot:eventTemplate="{ data }">
      <div class="custom-event">
        <div class="subject">{{ data.Subject }}</div>
        <div class="time">
          {{ formatTime(data.StartTime) }} - {{ formatTime(data.EndTime) }}
        </div>
        <div class="location" v-if="data.Location">
          <i class="e-icons e-location"></i> {{ data.Location }}
        </div>
      </div>
    </template>
  </ejs-schedule>
</template>

<script setup>
const formatTime = (date) => {
  return new Intl.DateTimeFormat('en-US', {
    hour: '2-digit',
    minute: '2-digit'
  }).format(date);
};
</script>

<style>
.custom-event {
  padding: 5px;
}
.subject {
  font-weight: bold;
  margin-bottom: 3px;
}
.time {
  font-size: 12px;
  color: #666;
}
.location {
  font-size: 11px;
  margin-top: 3px;
}
</style>
```

## Quick Info Template

Customize quick info popup:

```vue
<template>
  <ejs-schedule :quickInfoTemplates="quickInfoTemplates">
  </ejs-schedule>
</template>

<script setup>
const quickInfoTemplates = {
  header: (props) => {
    return `<div>${props.Subject || 'New Event'}</div>`;
  },
  content: (props) => {
    return `<div>
      <div>Time: ${formatDateTime(props.StartTime)}</div>
      <div>Location: ${props.Location || 'N/A'}</div>
      <div>Description: ${props.Description || 'N/A'}</div>
    </div>`;
  },
  footer: (props) => {
    return `<button class="e-btn">More Details</button>`;
  }
};
</script>
```

## Block Time Slots

Mark time slots as unavailable:

```vue
<script setup>
const eventSettings = {
  dataSource: [
    {
      Id: 1,
      Subject: 'Lunch Break',
      StartTime: new Date(2024, 0, 15, 12, 0),
      EndTime: new Date(2024, 0, 15, 13, 0),
      IsBlock: true // Blocks this time slot
    }
  ]
};
</script>
```

**Blocked slots**:
- Display with different styling
- Prevent event creation
- Show as unavailable time

## Tooltip

Show tooltip on hover:

```vue
<template>
  <ejs-schedule 
    :eventRendered="onEventRendered">
  </ejs-schedule>
</template>

<script setup>
import { Tooltip } from '@syncfusion/ej2-popups';

const onEventRendered = (args) => {
  const tooltip = new Tooltip({
    content: `${args.data.Subject}<br>
              ${formatDateTime(args.data.StartTime)} - ${formatDateTime(args.data.EndTime)}<br>
              ${args.data.Location || ''}`,
    target: args.element
  });
  tooltip.appendTo(args.element);
};
</script>
```

## Inline Editing

Enable quick inline editing:

```vue
<template>
  <ejs-schedule 
    :allowInline="true"
    :eventClick="onEventClick">
  </ejs-schedule>
</template>

<script setup>
const onEventClick = (args) => {
  // Enable inline editing by selecting event
  args.element.focus();
};
</script>
```

## Responsive Design

Scheduler adapts automatically to screen size. For custom responsive behavior:

```vue
<template>
  <ejs-schedule 
    :enableAdaptiveUI="true">
  </ejs-schedule>
</template>
```

**Mobile Features**:
- Touch-friendly interface
- Swipe navigation
- Optimized popups
- Compact view toggle

## Recurrence Editor

The Recurrence Editor is a standalone component for managing recurring event rules. It generates iCalendar-compliant recurrence rule strings:

### Basic Standalone Usage:

```vue
<template>
  <div>
    <label>Rule Output:</label>
    <div class="rule-output">{{ recurrenceRule }}</div>
    
    <ejs-recurrenceeditor 
      :selectedType="selectedType"
      @change="onRuleChange">
    </ejs-recurrenceeditor>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { RecurrenceEditorComponent as EjsRecurrenceeditor } from '@syncfusion/ej2-vue-schedule';

const selectedType = 1; // Weekly
const recurrenceRule = ref('Select Rule');

const onRuleChange = (args) => {
  recurrenceRule.value = args.value || 'Select Rule';
};
</script>
```

### Customize Repeat Options:

```vue
<script setup>
import { RecurrenceEditorComponent as EjsRecurrenceeditor } from '@syncfusion/ej2-vue-schedule';
import { onMounted, ref } from "vue";

const editorObj = ref(null);

onMounted(() => {
  // Show only specific repeat options
  editorObj.value.frequencies = ['none', 'daily', 'weekly', 'monthly'];
});
</script>
```

### Customize End Type Options:

```vue
<script setup>
const onMounted = () => {
  editorObj.value.endTypes = ['until', 'count']; // Remove 'never' option
};
</script>
```

### Set Predefined Recurrence Rule:

```vue
<script setup>
const onMounted = () => {
  // Set rule for "Every 2 days for 8 occurrences"
  editorObj.value.setRecurrenceRule('FREQ=DAILY;INTERVAL=2;COUNT=8');
};
</script>
```

### Generate Dates from Recurrence Rule:

```vue
<script setup>
const generateRecurrenceDates = () => {
  const dates = editorObj.value.getRecurrenceDates(
    new Date(2024, 0, 1, 10, 0),              // Start date
    'FREQ=DAILY;INTERVAL=1',                  // Rule
    '20240108T114224Z,20240110T114224Z',      // Exclude dates
    10,                                        // Max count
    new Date(2024, 0, 1)                      // View date
  );
  
  return dates.map(date => new Date(date).toString());
};
</script>
```

**Recurrence Editor Properties**:
- `frequencies` - Available repeat options
- `endTypes` - Available end options (never, until, count)
- `firstDayOfWeek` - Week start day
- `startDate` - Recurrence start date
- `dateFormat` - Custom date format
- `enableRtl` - RTL mode

## Calendar Mode

Switch between Gregorian and Islamic calendar systems:

### Gregorian Calendar (Default):

```vue
<template>
  <ejs-schedule 
    calendarMode="Gregorian"
    :eventSettings="eventSettings">
  </ejs-schedule>
</template>
```

### Islamic Calendar:

```vue
<template>
  <ejs-schedule 
    calendarMode="Islamic"
    :enableRtl="true"
    :eventSettings="eventSettings">
  </ejs-schedule>
</template>

<script setup>
import { provide } from "vue";
import { loadCldr, setCulture, L10n } from '@syncfusion/ej2-base';
import { Calendar, Islamic } from '@syncfusion/ej2-calendars';
import { ScheduleComponent as EjsSchedule, Day, Week, Month, Agenda } from '@syncfusion/ej2-vue-schedule';

// Load Islamic calendar CLDR data
import arNumberData from '@syncfusion/ej2-cldr-data/main/ar/numbers.json';
import arTimeZoneData from '@syncfusion/ej2-cldr-data/main/ar/timeZoneNames.json';
import arGregorian from '@syncfusion/ej2-cldr-data/main/ar/ca-gregorian.json';
import arIslamic from '@syncfusion/ej2-cldr-data/main/ar/ca-islamic.json';
import arNumberingSystem from '@syncfusion/ej2-cldr-data/supplemental/numberingSystems.json';
import localeText from './locale.json';

// Setup Islamic calendar
Calendar.Inject(Islamic);
loadCldr(arNumberData, arTimeZoneData, arGregorian, arIslamic, arNumberingSystem);
L10n.load(localeText);
setCulture('ar');

provide('schedule', [Day, Week, Month, Agenda]);
</script>
```

**Calendar Modes**:
- **Gregorian**: Solar calendar (default), 365-366 days per year
- **Islamic**: Lunar calendar, 354-355 days per year, months begin with new moon

## Working Days Configuration

Configure working days, working hours, and custom time ranges:

### Set Custom Working Days:

```vue
<template>
  <ejs-schedule 
    :workDays="[1, 3, 5]"
    :eventSettings="eventSettings">
    <e-views>
      <e-view option="Week"></e-view>
      <e-view option="WorkWeek"></e-view>
    </e-views>
  </ejs-schedule>
</template>

<script setup>
import { provide } from "vue";
import { ScheduleComponent as EjsSchedule, ViewDirective as EView, 
         ViewsDirective as EViews, Week, WorkWeek } from '@syncfusion/ej2-vue-schedule';

// Day mapping: 0=Sunday, 1=Monday, 2=Tuesday, 3=Wednesday, 4=Thursday, 5=Friday, 6=Saturday
// This example sets Monday, Wednesday, Friday as working days
const workDays = [1, 3, 5];

provide('schedule', [Week, WorkWeek]);
</script>
```

### Hide Weekend Days:

```vue
<template>
  <ejs-schedule 
    :workDays="[1, 3, 4, 5]"
    :showWeekend="false"
    :eventSettings="eventSettings">
    <e-views>
      <e-view option="Day"></e-view>
      <e-view option="Week"></e-view>
    </e-views>
  </ejs-schedule>
</template>

<script setup>
const showWeekend = false;  // Hide Sunday, Tuesday, Saturday
</script>
```

### Set Working Hours:

```vue
<template>
  <ejs-schedule 
    :workHours="workHours"
    :eventSettings="eventSettings">
    <e-views>
      <e-view option="Day"></e-view>
      <e-view option="Week"></e-view>
    </e-views>
  </ejs-schedule>
</template>

<script setup>
const workHours = {
  highlight: true,
  start: '11:00',
  end: '20:00'
};
</script>
```

### Display Custom Time Range:

```vue
<template>
  <ejs-schedule 
    startHour="07:00"
    endHour="18:00"
    :eventSettings="eventSettings">
  </ejs-schedule>
</template>
```

### Show Week Numbers:

```vue
<template>
  <ejs-schedule 
    :showWeekNumber="true"
    weekRule="FirstFourDayWeek"
    :eventSettings="eventSettings">
  </ejs-schedule>
</template>

<script setup>
// weekRule options: 'FirstDay', 'FirstFourDayWeek', 'FirstFullWeek'
const showWeekNumber = true;
const weekRule = 'FirstFourDayWeek';
</script>
```

### Set First Day of Week:

```vue
<template>
  <ejs-schedule 
    :firstDayOfWeek="3"
    :eventSettings="eventSettings">
  </ejs-schedule>
</template>

<script setup>
// 0=Sunday, 1=Monday, 2=Tuesday, 3=Wednesday, etc.
const firstDayOfWeek = 3;  // Start week on Wednesday
</script>
```

**Working Days Properties**:
- `workDays` - Array of working day numbers
- `workHours` - Start/end times and highlight flag
- `showWeekend` - Show/hide non-working days
- `showWeekNumber` - Display week numbers
- `weekRule` - Rule for week number calculation
- `firstDayOfWeek` - First day of the week
- `startHour`/`endHour` - Custom visible time range

## Scheduler Styling and Theming

Customize Scheduler appearance using CSS or Syncfusion Theme Studio:

### Built-in Themes:

```vue
<style>
/* Material3 (default) */
@import "@syncfusion/ej2-schedule/styles/material3.css";

/* Alternative themes */
@import "@syncfusion/ej2-schedule/styles/bootstrap5.css";
@import "@syncfusion/ej2-schedule/styles/fluent.css";
@import "@syncfusion/ej2-schedule/styles/tailwind.css";
</style>
```

### Styling Work Cells:

```vue
<style>
/* Vertical view work cells */
.e-schedule .e-vertical-view .e-work-cells {
  background-color: #f5f5f5;
}

/* Timeline view work cells */
.e-schedule .e-timeline-view .e-work-cells {
  border: 1px solid #ddd;
}

/* Month view work cells */
.e-schedule .e-month-view .e-work-cells {
  padding: 5px;
}
</style>
```

### Styling Appointments:

```vue
<style>
/* All appointments */
.e-schedule .e-appointment {
  border-radius: 4px;
  font-size: 13px;
}

/* Block appointments */
.e-schedule .e-block-appointment {
  opacity: 0.5;
  background-color: #d3d3d3 !important;
}

/* Selected appointment */
.e-schedule .e-appointment.e-appointment-border {
  border: 2px solid #1E90FF;
  box-shadow: 0 0 4px rgba(30, 144, 255, 0.5);
}
</style>
```

### Styling Working Days and Hours:

```vue
<style>
/* Working hour cells in vertical views */
.e-schedule .e-vertical-view .e-work-hours {
  background-color: #fffacd;
}

/* All-day cells */
.e-schedule .e-vertical-view .e-all-day-cells {
  background-color: #f0f0f0;
}

/* Working day cells in month view */
.e-schedule .e-month-view .e-work-days {
  background-color: #ffffff;
}
</style>
```

### Styling Resource Cells:

```vue
<style>
/* Resource cells in timeline views */
.e-schedule .e-timeline-view .e-resource-cells {
  background-color: #f9f9f9;
  padding: 8px;
}

/* Parent resource nodes */
.e-schedule .e-timeline-view .e-parent-node {
  font-weight: bold;
}

/* Child resource nodes */
.e-schedule .e-timeline-view .e-child-node {
  padding-left: 20px;
}
</style>
```

### Custom Theme Variables:

```vue
<style>
/* Override theme colors */
:root {
  --e-schedule-background: #ffffff;
  --e-schedule-border-color: #e0e0e0;
  --e-appointment-bg: #3f51b5;
  --e-appointment-text: #ffffff;
  --e-work-hours-bg: #fffacd;
}
</style>
```

**CSS Selectors Guide**:
- `.e-schedule .e-vertical-view .e-work-cells` - Vertical view work cells
- `.e-schedule .e-month-view .e-work-cells` - Month view cells
- `.e-schedule .e-timeline-view .e-work-cells` - Timeline view cells
- `.e-schedule .e-appointment` - Event appointments
- `.e-schedule .e-work-hours` - Working hour cells
- `.e-schedule .e-resource-cells` - Resource cells
- Use Theme Studio for visual customization: https://ej2.syncfusion.com/themestudio/

## Performance Tips

1. **Virtual Scrolling** - Enable for >1000 events
2. **includeFiltersInQuery** - Reduce data transfer from server
3. **Lazy Loading** - Load events on demand
4. **Debounce Actions** - Avoid rapid API calls
5. **Minimize Templates** - Complex templates impact rendering
6. **Use indexes** - On event ID field for faster queries
7. **Batch Operations** - Group multiple CRUD operations
8. **Cache Resources** - Store resource data locally when possible

## Best Practices

1. **Test with real data** - Verify performance with production-like datasets
2. **Optimize queries** - Use server-side filtering and pagination
3. **Implement caching** - Cache frequently accessed data
4. **Monitor performance** - Track rendering and API response times
5. **Use appropriate views** - Choose views based on data density
6. **Enable features selectively** - Only enable needed advanced features
7. **Handle errors gracefully** - Implement proper error handling
8. **Document customizations** - Maintain documentation for custom features
