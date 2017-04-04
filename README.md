# Frontend Coding Challenge
We would like you to build a small web application for a weather dashboard using AngularJS. Your webapp should hook into the public APIs provided below. These APIs are built over services like Forecast.io, WeatherBug, WeatherUnderground, etc. for weather related data and allow you to display the current and 7-day weather forecast from different sources. Please feel free to pick other technologies as you see fit. You have complete creative control over how the dashboard looks and functions.

# API
Domain is [http://http://178.79.140.126/](http://http://178.79.140.126/)
## Cities API
API was built on top of Google API. Documentation and the examples of response can be found [here](https://developers.google.com/places/web-service/autocomplete?hl=en). 

`GET api/cities/search`<br/>
Method to search for the cities by name.

Parameters:<br/>
`byName` -  String. Name of city.

Example of request:<br/>
`/api/cities/search?byName=Kra`

Response:<br/>
```
{
   "predictions" : [
      {
         "description" : "Kraków, Poland",
         "id" : "22ee34a1db0c617129e62cb84d1eb7162afceb98",
         "matched_substrings" : [
            {
               "length" : 6,
               "offset" : 0
            }
         ],
         "place_id" : "ChIJ0RhONcBEFkcRv4pHdrW2a7Q",
         "reference" : "CjQnAAAAEef91cNPSIta_UfZj1knIjXIRiRssg_pnrI8roSdiuCZwaiRG5qXG6CCJs7GwEBhEhCFDsJo9EKQ2rZXgVLmn9uyGhRE5No6a5HxbIpGJt6HBz81v-YbHA",
         "terms" : [
            {
               "offset" : 0,
               "value" : "Kraków"
            },
            {
               "offset" : 8,
               "value" : "Poland"
            }
         ],
         "types" : [ "locality", "political", "geocode" ]
      },
      ...,
      ...
}
```
<hr/>
`GET api/cities/{:cityId}`<br/>
Method to get data about city by id. Response contains formatted name of the city, coordinates and other information.  

Parameters:<br/>
`cityId` - `place_id` of location from Google API.

Example of request:<br/>
`/api/cities/ChIJ0RhONcBEFkcRv4pHdrW2a7Q`

## Forecast API
`GET api/forecast`<br/>
Method to search for a forecast by coordinates.

Parameters:
* `latitude` -  Float. Latitude of the location.
* `longitude` -  Float. Longitude of the location.
* `source` -  String. Code name of the forecast provider. Supported codes are: 
  * `FORECAST_IO` for [forecast.io](forecast.io). [API reference.](https://developer.forecast.io)
  * `WORLD_WEATHER` for [World Weather Online](http://www.worldweatheronline.com). [API reference.](http://developer.worldweatheronline.com/api/)

Example of request:<br/>
`/api/forecast?latitude=50.06465009999999&longitude=19.9449799&source=WORLD_WEATHER`

Response:<br/>
```
{
  "currently":
    {
      "temperature":68.0,
      "apparentTemperature":68.0,
      "date":"2016-08-23",
      "humidity":0.68,
      "pressure":1027.0,
      "cloudCover":0.5
    },
  "futureForecasts": [
    {
      "temperatureMin":52.0,
      "temperatureMax":72.0,
      "apparentTemperatureMin":72.0,
      "apparentTemperatureMax":72.0,
      "date":"2016-08-24",
      "humidity":0.58,
      "pressure":1024.0,
      "cloudCover":0.46
    },
    {
      "temperatureMin":54.0,
      "temperatureMax":72.0,
      "apparentTemperatureMin":72.0,
      "apparentTemperatureMax":72.0,
      "date":"2016-08-25",
      "humidity":0.47,
      "pressure":1024.0,
      "cloudCover":0.0
    },
    ...,
    ...,
  ]
}
```
