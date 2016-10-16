<div id="map" style="width: 100%; height: 400px;"> </div>

<script src="https://maps.googleapis.com/maps/api/js?v=3.exp&sensor=false"></script>



<script>
    var markers = [];

    function initialize() {
        var beaches = <?=$map ?>;
        var map = new google.maps.Map(document.getElementById('map'), {
            zoom: 9,
            center: new google.maps.LatLng(18.274430, 100.019334),
            mapTypeId: google.maps.MapTypeId.ROADMAP
        });

        var infowindow = new google.maps.InfoWindow();

        for (var i = 0; i < beaches.length; i++) {

            var newMarker = new google.maps.Marker({
                position: new google.maps.LatLng(beaches[i][1], beaches[i][2]),
                map: map,
                title: beaches[i][0]
            });

            google.maps.event.addListener(newMarker, 'click', (function(newMarker, i) {
                return function() {
                    infowindow.setContent(beaches[i][0]);
                    infowindow.open(map, newMarker);
                }
            })(newMarker, i));

            markers.push(newMarker);
        }
    }

    initialize();

</script>
