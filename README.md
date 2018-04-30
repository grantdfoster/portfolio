![logo](star-sheets-logo.png)

![screenshots](star-sheets-screenshots.png)

![demo](star-sheets-demo.gif)

## Stack
![stack](star-sheets-stack.png)

## Code Snippets - [View on Github](https://github.com/WeConnect/star-sheets)

#### Create Vector Plan from Points
```html
<svg :width="windowWidthExtents[1]" :height="windowHeightExtents[0]">
  <path
    v-for="room, index in rooms"
    :key="room.uuid"
    @mouseover="hoveredRoom = room.uuid"
    @mouseleave="hoveredRoom = null"
    @click="addRoomToSelection(room)"
    :d="computeLine(room.outline)"
    :style="{'cursor': 'pointer', 'fill': getProgramColor(room, index, true)}">
  </path>
</svg>
```
```javascript
computeLine: function (points) {
  var line = d3.line().x(pt => this.scaledLocationX()(pt.x)).y(pt => this.scaledLocationY()(pt.y)).curve(d3.curveLinearClosed);
  return line(points);
},
scaledLocationX () {
  return d3.scaleLinear().domain(this.planWidthExtents).range(this.windowWidthExtents)
},
scaledLocationY () {
  return d3.scaleLinear().domain(this.planHeightExtents).range(this.windowHeightExtents)
}
```

#### Create a formatted Google Sheet Tab with Data
```javascript
function createTabWithData(tabName, headers, doubleArray) {
  var tab = createTab(tabName);
  var rows = doubleArray.length;
  var columns = doubleArray[0].length;
  // row, column, rows, columns
  tab.getRange(1, 1, 1, columns).setValues([headers]).setFontWeight("bold").setBackground('#616161').setFontColor('#FFFFFF');
  tab.getRange(2, 1, rows, columns).setValues(doubleArray);
  return tabName;
}
```