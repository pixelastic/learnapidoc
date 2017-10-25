---
title: "Sample OpenAPI (Swagger) specification file"
permalink: /pubapis_swagger_sample_specification_file.html
course: "Documenting REST APIs"
sidebar: docapis
weight: 8.26
section: restapispecifications
path1: /restapispecifications.html
---

In the [Swagger tutorial](pubapis_swagger.html), I referenced an OpenAPI specification file that you simply plugged into a Swagger UI project. In this section, we'll dive more deeply into the Swagger specification file (but not too deep, because one could write an entire book on the subject).

The following is an [OpenAPI specification file](/learnapidoc/docs/rest_api_specifications/openapi_weather.yml)(following the [3.0 version of the OpenAPI (Swagger) spec](https://swaggerhub.com/blog/news/openapi-3-0-swaggerhub-support/)) that I created for the [sample Mashape Weather API](https://market.mashape.com/fyhao/weather-13). Note that this API builds off of a [Yahoo weather service API](https://developer.yahoo.com/weather/documentation.html), so the data returned in the `weather` and `weatherdata` endpoints is highly similar to the data returned by the Yahoo weather service API.

You can view the OpenAPI specification file [embedded in Swagger UI here](pubapis_swagger_embedded.html).

```yaml
openapi: "3.0.0"
info:
  title: Weather API from Mashape
  description: "This is a sample spec that describes a Mashape Weather API as an example to demonstrate features in the Swagger-2.0 specification. This output is part of the <a href=\"http://idratherbewriting.com/learnapidoc\">Documenting REST API course</a> on my site. The Weather API displays forecast data by latitude and longitude. It's a simple weather API, but the data comes from Yahoo Weather Service. The weatherdata endpoint delivers the most robust package of information of the endpoints here.\n\nTo explore the API, you'll need an API key. You can sign up for an API through Mashape, or you can just use this one\\: `EF3g83pKnzmshgoksF83V6JB6QyTp1cGrrdjsnczTkkYgYrp8p`. For the latitude and longitude parameters, you can get this information from the URL of a location on Google Maps. For example, for Santa Clara, California, use the following\\:\n* **lat**: `37.3708698`\n* **lng**: `-122.037593` \n"
  version: "2.1"
servers:
- url: https://simple-weather.p.mashape.com
- url: https://another.simple-weather.p.mashape.com
  variables: {}
paths:
  /aqi:
    get:
      tags:
      - Air Quality
      summary: getAqi
      description: Gets the air quality index
      operationId: GetAqi
      parameters:
      - name: lat
        in: query
        description: "Latitude coordinates. Sunnyvale: 37.3708698"
        required: true
        style: form
        explode: false
        schema:
          type: string
      - name: lng
        in: query
        description: "Longitude coordinates. Sunnyvale: -122.037593"
        required: true
        style: form
        explode: false
        schema:
          type: string
      responses:
        200:
          description: AQI response
          content:
            text/plain:
              schema:
                type: string
                description: AQI response
                example: 52
              example: 52
      deprecated: false
      security:
      - Mashape-Key: []
      x-operation-settings:
        CollectParameters: false
        AllowDynamicQueryParameters: false
        AllowDynamicFormParameters: false
        IsMultiContentStreaming: false
  /weather:
    get:
      servers:
      - url: https://simple-weather.p.mashape.com
      tags:
      - Weather Forecast
      summary: getWeather
      description: Gets the weather forecast in abbreviated form
      operationId: GetWeather
      parameters:
      - name: lat
        in: query
        description: "Latitude coordinates. Sunnyvale: 37.3708698"
        required: true
        style: form
        explode: false
        schema:
          type: string
      - name: lng
        in: query
        description: "Longitude coordinates. Sunnyvale: -122.037593"
        required: true
        style: form
        explode: false
        schema:
          type: string
      responses:
        200:
          description: weather response
          content:
            text/plain:
              schema:
                type: string
                description: weather response
                example: 26 c, Mostly Clear at Singapore, Singapore
              example: 26 c, Mostly Clear at Singapore, Singapore
      deprecated: false
      security:
      - Mashape-Key: []
      x-operation-settings:
        CollectParameters: false
        AllowDynamicQueryParameters: false
        AllowDynamicFormParameters: false
        IsMultiContentStreaming: false
  /weatherdata:
    get:
      tags:
        - Full Weather Data
      servers:
      - url: https://another.simple-weather.p.mashape.com
      summary: getWeatherData
      description: Get weather forecast with lots of details
      operationId: GetWeatherData
      parameters:
      - name: lat
        in: query
        description: "Latitude coordinates. Sunnyvale: 37.3708698"
        required: true
        style: form
        explode: false
        schema:
          type: string
      - name: lng
        in: query
        description: "Longitude coordinates. Sunnyvale: -122.037593"
        required: true
        style: form
        explode: false
        schema:
          type: string
      responses:
        200:
          description: Successful operation
          content:
            application/json:
              schema:
                description: Successful operation
                $ref: '#/components/schemas/WeatherdataResponse'
      deprecated: false
      security:
      - Mashape-Key: []
      x-operation-settings:
        CollectParameters: false
        AllowDynamicQueryParameters: false
        AllowDynamicFormParameters: false
        IsMultiContentStreaming: false
components:
  schemas:
    WeatherdataResponse:
      title: weatherdata response
      type: object
      properties:
        query:
          $ref: '#/components/schemas/Query'
    Query:
      title: query
      type: object
      properties:
        count:
          type: integer
          description: The number of items (rows) returned -- specifically, the number of sub-elements in the results property
          format: int32
          example: 1
        created:
          type: string
          description: The date and time the response was created
          example: 6/14/2017 2:30:14 PM
        lang:
          type: string
          description: The locale for the response
          example: en-US
        results:
          $ref: '#/components/schemas/Results'
    Results:
      title: results
      type: object
      properties:
        channel:
          $ref: '#/components/schemas/Channel'
    Channel:
      title: channel
      type: object
      properties:
        units:
          description: Units for various aspects of the forecast. Note that the default is to use metric formats for the units (Celsius, kilometers, millibars, kilometers per hour).
          $ref: '#/components/schemas/Units'
        title:
          type: string
          description: The title of the feed, which includes the location city
          example: Yahoo! Weather - Singapore, South West, SG
        link:
          type: string
          description: The URL for the Weather page of the forecast for this location
          example: http://us.rd.yahoo.com/dailynews/rss/weather/Country__Country/*https://weather.yahoo.com/country/state/city-91792352/
        description:
          type: string
          description: The overall description of the feed including the location
          example: Yahoo! Weather for Singapore, South West, SG
        language:
          type: string
          description: The language of the weather forecast
          example: en-us
        lastBuildDate:
          type: string
          description: The last time the feed was updated. The format is in the date format defined by [RFC822 Section 5](http://www.rfc-editor.org/rfc/rfc822.txt).
          example: Wed, 14 Jun 2017 10:30 PM SGT
        ttl:
          type: string
          description: Time to Live -- how long in minutes this feed should be cached.
          example: 60
        location:
          description: The location of this forecast
          $ref: '#/components/schemas/Location'
        wind:
          description: Forecast information about wind
          $ref: '#/components/schemas/Wind'
        atmosphere:
          description: Forecast information about current atmospheric pressure, humidity, and visibility
          $ref: '#/components/schemas/Atmosphere'
        astronomy:
          description: Forecast information about current astronomical conditions
          $ref: '#/components/schemas/Astronomy'
        image:
          description: The image used to identify this feed
          $ref: '#/components/schemas/Image'
        item:
          description: The item element contains current conditions and forecast for the given location. There are multiple weather forecast elements for today and tomorrow.
          $ref: '#/components/schemas/Item'
    Units:
      title: units
      type: object
      properties:
        distance:
          type: string
          description: Units for distance, mi for miles or km for kilometers
          example: km
        pressure:
          type: string
          description: Units of barometric pressure, "in" for pounds per square inch or "mb" for millibars.
          example: mb
        speed:
          type: string
          description: Units of speed, "mph" for miles per hour or "kph" for kilometers per hour.
          example: km/h
        temperature:
          type: string
          description: Degree units, "f" for Fahrenheit or "c" for Celsius.
          example: C
      description: Units for various aspects of the forecast. Note that the default is to use metric formats for the units (Celsius, kilometers, millibars, kilometers per hour).
    Location:
      title: location
      type: object
      properties:
        city:
          type: string
          description: City name
          example: Singapore
        country:
          type: string
          description: Two-character country code
          example: Singapore
        region:
          type: string
          description: State, territory, or region, if given
          example: South West
      description: The location of this forecast
    Wind:
      title: wind
      type: object
      properties:
        chill:
          type: integer
          description: Wind chill in degrees
          format: int32
          example: 81
        direction:
          type: integer
          description: Wind direction, in degrees
          format: int32
          example: 158
        speed:
          type: integer
          description: Wind speed, in the units specified in the speed attribute of the units element (mph or kph)
          format: int32
      description: Forecast information about wind
    Atmosphere:
      title: atmosphere
      type: object
      properties:
        humidity:
          type: integer
          description: humidity, in percent
          format: int32
          example: 87
        pressure:
          type: integer
          description: Barometric pressure, in the units specified by the pressure attribute of the yweather:units element ("in" or "mb").
          format: int32
        rising:
          type: integer
          description: 'State of the barometric pressure: steady (0), rising (1), or falling (2).'
          format: int32
          example: 0
        visibility:
          type: integer
          description: Visibility, in the units specified by the distance attribute of the units element ("mi" or "km"). Note that the visibility is specified as the actual value * 100. For example, a visibility of 16.5 miles will be specified as 1650. A visibility of 14 kilometers will appear as 1400.
          format: int32
      description: Forecast information about current atmospheric pressure, humidity, and visibility
    Astronomy:
      title: astronomy
      type: object
      properties:
        sunrise:
          type: string
          description: Today's sunrise time. The time is a string in a local time format of "h:mm am/pm"
          example: 6:59 am
        sunset:
          type: string
          description: Today's sunset time. The time is a string in a local time format of "h:mm am/pm"
          example: 7:11 pm
      description: Forecast information about current astronomical conditions
    Image:
      title: image
      type: object
      properties:
        title:
          type: string
          description: The title of the image.
          example: Yahoo! Weather
        width:
          type: string
          description: The width of the image, in pixels
          example: 142
        height:
          type: string
          description: The height of the image, in pixels
          example: 18
        link:
          type: string
          description: Description of link
          example: http://weather.yahoo.com
        url:
          type: string
          description: The URL of Yahoo! Weather
          example: http://l.yimg.com/a/i/brand/purplelogo//uh/us/news-wea.gif
      description: The image used to identify this feed
    Item:
      title: item
      type: object
      properties:
        title:
          type: string
          description: The forecast title and time.
          example: Conditions for Singapore, South West, SG at 09:00 PM SGT
        lat:
          type: string
          description: The latitude of the location.
          example: 1.33464
        long:
          type: string
          description: The longitude of the location.
          example: 103.726471
        link:
          type: string
          description: The Yahoo! Weather URL for this forecast.
          example: http://us.rd.yahoo.com/dailynews/rss/weather/Country__Country/*https://weather.yahoo.com/country/state/city-91792352/
        pubDate:
          type: string
          description: The date and time this forecast was posted, in the date format defined by [RFC822 Section 5](http://www.rfc-editor.org/rfc/rfc822.txt).
          example: Wed, 14 Jun 2017 09:00 PM SGT
        condition:
          description: The current weather conditions
          $ref: '#/components/schemas/Condition'
        forecast:
          type: array
          items:
            $ref: '#/components/schemas/ForecastArray'
          description: ''
        description:
          type: string
          description: A simple summary of the current conditions and tomorrow's forecast, in HTML format, including a link to Yahoo! Weather for the full forecast.
          example: "<![CDATA[<img src=\"http:\/\/l.yimg.com\/a\/i\/us\/we\/52\/4.gif\"\/>\n<BR \/>\n<b>Current Conditions:<\/b>\n<BR \/>Thunderstorms\n<BR \/>\n<BR \/>\n<b>Forecast:<\/b>\n<BR \/> Fri - Thunderstorms. High: 30Low: 25\n<BR \/> Sat - Thunderstorms. High: 28Low: 25\n<BR \/> Sun - Thunderstorms. High: 28Low: 25\n<BR \/> Mon - Thunderstorms. High: 28Low: 25\n<BR \/> Tue - Thunderstorms. High: 28Low: 25\n<BR \/>\n<BR \/>\n<a href=\"http:\/\/us.rd.yahoo.com\/dailynews\/rss\/weather\/Country__Country\/*https:\/\/weather.yahoo.com\/country\/state\/city-91792352\/\">Full Forecast at Yahoo! Weather<\/a>\n<BR \/>\n<BR \/>\n(provided by <a href=\"http:\/\/www.weather.com\" >The Weather Channel<\/a>)\n<BR \/>\n]]>"
        guid:
          type: string
          description: Unique identifier for the forecast, made up of the location ID, the date, and the time.
          format: uuid
      description: The item element contains current conditions and forecast for the given location. There are multiple weather forecast elements for today and tomorrow.
    Condition:
      title: condition
      type: object
      properties:
        code:
          type: integer
          description: The condition code for this forecast. You could use this code to choose a text description or image for the forecast. The possible values for this element are described in the [Condition Codes](https://developer.yahoo.com/weather/).documentation.html.
          format: int32
          example: 33
        date:
          type: string
          description: The current date and time for which this forecast applies. The date is in RFC822 Section 5 format.
          example: Wed, 14 Jun 2017 09:00 PM SGT
        temp:
          type: integer
          description: The current temperature, in the units specified by the units element.
          format: int32
          example: 26
        text:
          type: string
          description: A textual description of conditions
          example: Mostly Clear
      description: The current weather conditions
    ForecastArray:
      title: forecast array
      type: object
      properties:
        code:
          type: integer
          description: The condition code for this forecast. You could use this code to choose a text description or image for the forecast. The possible values for this element are described in the [Condition Codes](https://developer.yahoo.com/weather/documentation.html#codes).
          format: int32
          example: 4
        date:
          type: string
          description: The date to which this forecast applies. The date is in 'dd Mmm yyyy' format, for example '30 Nov 2005'
          example: 14 Jun 2017
        day:
          type: string
          description: Day of the week to which this forecast applies. Possible values are Mon Tue Wed Thu Fri Sat Sun.
          example: Wed
        high:
          type: integer
          description: The forecasted high temperature for this day, in the units specified by the units element.
          format: int32
          example: 28
        low:
          type: integer
          description: The forecasted low temperature for this day, in the units specified by the units element.
          format: int32
          example: 25
        text:
          type: string
          description: A textual description of conditions
          example: Thunderstorms
      description: The weather forecast for a specific day. The item element contains multiple forecast elements for today and tomorrow.
    Guid:
      title: guid
      type: object
      properties:
        isPermaLink:
          type: string
          description: The attribute isPermaLink is false.
          example: false
      description: Unique identifier for the forecast, made up of the location ID, the date, and the time.
  securitySchemes:
    Mashape-Key:
      type: apiKey
      description: "Your Mashape key. If you don't have one, you can use `EF3g83pKnzmshgoksF83V6JB6QyTp1cGrrdjsnczTkkYgYrp8p`."
      name: X-Mashape-Key
      in: header
security:
- Mashape-Key: []
```

{: .tip }
If you have a spec in 2.0 and want to convert it to 3.0, you can use [APIMATIC](https://apimatic.io/transformer) to convert it automatically. You can also use APIMATIC to transform your spec file into a number of other outputs, such as RAML, Postman, or API Blueprint. To see the difference between the 2.0 and the 3.0 code, you can copy these code samples to separate files and then use an application like Diffmerge to highlight the differences.

{% include random_ad.html %}