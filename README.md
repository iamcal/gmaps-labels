# Labels for Google Maps

This code allows you to place textual labels on Google Maps, by implementing an overlay class.

--

Using it is pretty simple. You'll need to load the JS and CSS files, along with jQuery:

    <link rel="stylesheet" type="text/css" media="all" href="gmaps-labels.css" />
    <script type="text/javascript" src="http://maps.google.com/maps/api/js?v=3&sensor=false"></script>
    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js"></script>
    <script type="text/javascript" src="gmaps-labels.js"></script>

Then after you've created your map, add some labels:

    var l = new LabelOverlay({
        ll : new google.maps.LatLng(-34.397, 150.644),
        label : "My label!",
        map : map
    });

The parameters specify the LatLng of the label, the text to display and the map to display them on.


## Optional parameters

Those are the only required params, but there are a bunch of optional ones:

    minBoxW : int, // The height and width (in LatLng units) of a box centered around the
    minBoxH : int, // label's point. If the label would overflow this box, hide it.

    minBox : LatLngBounds, // As above, but manually specify the box.

    maxBoxW : int, // The height and width (in LatLng units) of a box centered around the
    maxBoxH : int, // label's point. If the label is smaller than this box, hide it.

    maxBox :  LatLngBounds, // As above, but manually specify the box.

    minZoom : int, // Minimum zoom level to show the label at.
    maxZoom : int, // Maximum zoom level to show the label at.

    className : string, // CSS class name to add to the labe.

    debugBoxes : boolean, // Show the min/max boxes visually, to aid in debugging.
    debugVisibility: boolean, // Show the label in red in situations where it would be hidden.


## Sizing boxes

The min/max boxes are best illustrated with an example. When the label size fits inside the blue 
rectangle (the minBox), but is larger than the red rectangle (the maxBox), the label is shown.

--

When the label is smaller than the red rectangle (the maxBox), the label is hidden.

--

And when the label is larger than the blue rectangle (the minBox), the label is also hidden.

--


## Styling

Every label is given the class `gmaps-label`. The CSS file also defines the extra classes
`small`, `big` and `huge`.

--

You can replace the supplied CSS file with your own - just make sure the class has `position: absolute` set.


## Future changes

A nice feature would be to rearrange the labels within an allowed zone so that things don't 
overlap. This would be especially useful for maps with a lot of labels.

For maps with more than about 50 labels, it would probably make sense to start destroying 
the divs when they scroll off-pane. It might make more sense to also re-cycle the `div` elements
to avoid constant element creation/destruction. In this case, the labels would need to be sized
at creation time and those sizes cached.

These labels were created for projects that don't use the Google base maps, or use the Satellite-only
tileset which has no existing labels. Labels look best when baked into the tiles themselves, or in
a transparent overlay tileset, but rendering that is pretty slow and doesn't lend itself to dynamic
data or experimentation.

This class could be easily converted to other map engines that use a similar API, such as
<a href="http://leaflet.cloudmade.com/">Leaflet</a>.
