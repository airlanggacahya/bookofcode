
# Javascript

## Function Naming
TODO

## Method Scoping
TODO

## Variable Naming
TODO

## Indentation
TODO

## New Line Ending
TODO

# Knockout

## KendoDatePicker
### Parsing value result
Consider to remove timezone before submiting datetime value to server.

Example of code to discard timezone data using moment.js
```js
var newdate = moment(date)
newdate = newdate.format("YYYY-MM-DDT00:00:00") + "Z"
```

## KendoChart
When using Kendo Chart with Knockout binding, it's recommended to use observable binding instead of long style html tag.

### Do use
```js
var report = ko.observableArray({
    data: [1, 2, 3],
    series: [{
        type: 'column',
        name: 'Approved',
        field: 'approved'
    },
    {
        type: 'column',
        name: 'Rejected',
        field: 'rejected'
    }]
})

var reportChart = {
    data: report.Data,
    series: report.Series,
    title: {
        font: "bold 12px Arial,Helvetica,Sans-Serif"
    }
}
```

```
<div data-bind="kendoChart: awesomeChart">
</div>
```

### Avoid
TODO

# Jquery
## Defered / Promise
Deferred jquery technique can be used when we need to waiting for two action at once. This is powerfull method for handling asynchronous call.

For example, we need to do two ajax at the same time, and calculate the differences between two data.

```js
var firstPromise = $.Deferred();
var secondPromise = $.Deferred();

$.ajax("/someapi/id/1", {
    method: "POST",
    success: function(data) {
        firstPromise.resolve(data)
    }
})

$.ajax("/someapi/id/1", {
    method: "POST",
    success: function(data) {
        secondPromise.resolve(data)
    }
})

$.when(firstPromise, secondPromise).then(function (result1, result2) {
    // result1 and result2 will containst value passed using resolve() method
    // this function will be only called when both firstPromise and secondPromise resolved
})
```