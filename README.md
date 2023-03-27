  <!DOCTYPE html>
<html>
  <head>
    <title>Snow Forecast</title>
  </head>
  <body>
    <h1>Will it snow today?</h1>
    <p id="forecast"></p>
    <script>
        // get user's location
        navigator.geolocation.getCurrentPosition(function(position) {
            // make API call to weather service
            fetch('https://api.weather.com/v3/wx/forecast/daily/5day?geocode=' + position.coords.latitude + ',' + position.coords.longitude + '&format=json&units=e&apiKey=YOUR_API_KEY')
                .then(function(response) {
                    return response.json();
                })
                .then(function(data) {
                    // check if forecast calls for snow
                    if (data.forecasts[0].day.snow_qpf > 0) {
                        document.getElementById("forecast").innerHTML = "Yes, it will snow today!";
                    } else {
                        document.getElementById("forecast").innerHTML = "No, it will not snow today.";
                    }
                });
        });
    </script>
  </body>
</html>
