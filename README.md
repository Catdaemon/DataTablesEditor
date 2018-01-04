# DataTablesEditor
A simple editor plugin for DataTables

# Usage
Create a table with the following specifications:
- tr elements have a `data-identity` attribute for the database row they refer to.
- td elements have a `data-field` attribute for the database column they refer to.
- td elements also have a `data-type` attribute to determine the input type to create for them when editing.

```html
<table id="schedule" class="dataTable">
    <thead>
        <tr>
            <th>Name</th>
            <th>Location</th>
            <th>Weekday</th>
            <th>Start Time</th>
            <th>End Time</th>
            <th>Date From</th>
            <th>Date To</th>
        </tr>
    </thead>
    <tbody>
        @foreach (var row in Model)
        {
            <tr data-identity="@row.ScheduleID">
                <td data-field="Name" data-type="text">@row.Name</td>
                <td data-field="Location" data-type="text">@row.Location</td>
                <td data-field="Weekday" data-type="number">@row.Weekday</td>
                <td data-field="StartTime" data-type="time">@row.StartTime</td>
                <td data-field="EndTime" data-type="time">@row.EndTime</td>
                <td data-field="DateFrom" data-type="date">@row.DateFrom.ToString("yyyy-MM-dd")</td>
                <td data-field="DateTo" data-type="date">@row.DateTo.ToString("yyyy-MM-dd")</td>
            </tr>
        }
    </tbody>
</table>
````

Then simply invoke with options:
```javascript
$("#schedule").dataTableEditor({ postURL: "/Enrichment/Timetable" });
```

## Options
- `postURL`: where to POST data.
- `success`: function to call on success.
- `error`: function to call on error.
- `complete`: function to call after success or error.

Functions will receive the relevant td element as the first parameter, then whatever content jQuery returns for the ajax callbacks.

## Server-side
You'll need to implement something to receive the requests and do something with the data. Your application will receive:
- `id`
- `field`
- `value`

By default the plugin will replace the content with whatever is returned by the server, so output the same `value` that was passed or do something more interesting.

# Demo
![gif](https://i.imgur.com/jxYtMjn.gif)
