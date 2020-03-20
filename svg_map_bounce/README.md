# Animated Zoom in and Out with an SVG Map

## A video of the operation of this file can be seen [here](https://www.youtube.com/watch?v=XCYRUInpFhg)

In this example, entire map is assigned a single onclick function.

Whenever an individual state is clicked on, it is processed by the map as a whole and the bounding box of the state is determined.

A number of steps that that will be used to zoom in is set with the line:
```
var decimation = 100.0;
```
Then, this line determines how much to change the ViewBox so that the original viewBox may linearly transition to the single state view in `decimation` steps.

Finally, the viewBox is adjusted every 15ms until it reaches max zoom, waits a second and then zooms out with the following code:
```
var frame_count = 0;
var h = setInterval(function() {
  src = src.map((elem,indx)=> src[indx] + deltas[indx]);
  var viewBoxString = "";
  src.forEach((elem)=>{viewBoxString = viewBoxString.concat(elem," ")});
  s.setAttribute('viewBox', viewBoxString);
  frame_count += 1;
  if (frame_count > decimation) {
    clearInterval(h);
    setTimeout( function() {
      frame_count = 0;
      hout = setInterval(function() {
        src = src.map((elem,indx)=> src[indx] - deltas[indx]);
        var viewBoxString = "";
        src.forEach((elem)=>{viewBoxString = viewBoxString.concat(elem," ")});
        s.setAttribute('viewBox', viewBoxString);
        frame_count += 1;
        if (frame_count > decimation) {
          in_transition = false;  
          clearInterval(hout);
        }
      }, 15)
    }, 1000 );
  }
}, 15)
```
