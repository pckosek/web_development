# Zooming into an SVG Map

## A video of the operation of this file can be seen [here](https://www.youtube.com/watch?v=eD2kHskVii0)

In this example, entire map is assigned a single onclick function.
```
all_states.onclick = function(ev) {
    
    // get the state
    var this_state = ev.target;
    
    // zoom in to the state
    fly_in(this_state);
}
```

The html element for the individual state that was clicked on is teased out of the event in the line:
```
	var this_state = ev.target;
```

f
