---
title: Workshop activities
permalink: /workshop-activities.html
course: "Documenting REST APIs"
weight: 1.32
sidebar: docapis
section: introtoapis
path1: /docapis_introtoapis.html
---

The following are activities used in the [live workshops](http://idratherbewriting.com/2018/01/29/api-workshop-in-denver/).

* TOC
{:toc}

## Part I: Intro to API documentation

Slides: [Intro to API documentation](http://idratherbewriting.com/intro-to-api-documentation/index.html)

### Activity: Explore an API

Explore the basic sections in API reference documentation in these 2 weather APIs:

* [Mashape Weather API](https://market.mashape.com/fyhao/weather-13).
* [Aeris Weather API](https://www.aerisweather.com/support/docs/api/)

### Activity: Make a curl request

Mac:

```
curl --get --include 'https://simple-weather.p.mashape.com/weatherdata?lat=37.3710062&lng=-122.0375935' -H 'X-Mashape-Key: EF3g83pKnzmshgoksF83V6JB6QyTp1cGrrdjsnczTkkYgYrp8p' -H 'Accept: application/json'
```

Windows:

```
curl --get -k --include "https://simple-weather.p.mashape.com/weatherdata?lat=37.3710062&lng=-122.0375935" -H "X-Mashape-Key: EF3g83pKnzmshgoksF83V6JB6QyTp1cGrrdjsnczTkkYgYrp8p" -H "Accept: application/json"
```

### Activity: Postman client

1. Download [Postman](https://www.getpostman.com/).
2. Populate Postman from the Run in Postman button or from [this link](https://www.getpostman.com/collections/7975e93f7b4944f50fa7):

    <div class="postman-run-button"
    data-postman-action="collection/import"
    data-postman-var-1="7975e93f7b4944f50fa7"></div>
    <script type="text/javascript">
    (function (p,o,s,t,m,a,n) {
    !p[s] && (p[s] = function () { (p[t] || (p[t] = [])).push(arguments); });
    !o.getElementById(s+t) && o.getElementsByTagName("head")[0].appendChild((
    (n = o.createElement("script")),
    (n.id = s+t), (n.async = 1), (n.src = m), n
    ));
    }(window, document, "_pm", "PostmanRunObject", "https://run.pstmn.io/button.js"));
    </script>

3. Make requests in Postman.
4. Generate code snippets in JavaScript (AJAX) from Postman.
5. Create a Run in Postman button for your requests. In the Collections pane, click the **<** arrow to expand the pane and click **Share**.

## Part II: OpenAPI and Swagger

Slides: [OpenAPI and Swagger](http://idratherbewriting.com/openapi-and-swagger/#/)

### Activity: OpenAPI with Stoplight

1. Open [v3 next Stoplight app](https://next.stoplight.io/). (You can also use the [Desktop app](https://github.com/stoplightio/desktop/releases/latest))
2. From main.oas, open the Code tab and paste in content for this 2.0 JSON Open API definition: [http://idratherbewriting.com/learnapidoc/docs/rest_api_specifications/openapi_weather20.json](/learnapidoc/docs/rest_api_specifications/openapi_weather20.json)
3. Edit, explore Basics, Requests, Responses sections.
4. In the Responses area, click **Generate from JSON**, paste in complex JSON snippet into the Responses area, then click **Generate!**

   ```json
   {
    "query": {
      "count": 1,
      "created": "6/14/2017 2:30:14 PM",
      "lang": "en-US",
      "results": {
        "channel": {
          "units": {
            "distance": "km",
            "pressure": "mb",
            "speed": "km/h",
            "temperature": "C"
          },
          "title": "Yahoo! Weather - Singapore, South West, SG",
          "link": "http://us.rd.yahoo.com/dailynews/rss/weather/Country__Country/*https://weather.yahoo.com/country/state/city-91792352/",
          "description": "Yahoo! Weather for Singapore, South West, SG",
          "language": "en-us",
          "lastBuildDate": "Wed, 14 Jun 2017 10:30 PM SGT",
          "ttl": 60,
          "location": {
            "city": "Singapore",
            "country": "Singapore",
            "region": "South West"
          },
          "wind": {
            "chill": 81,
            "direction": 158,
            "speed": 0
          },
          "atmosphere": {
            "humidity": 87,
            "pressure": 0,
            "rising": 0,
            "visibility": 0
          },
          "astronomy": {
            "sunrise": "6:59 am",
            "sunset": "7:11 pm"
          },
          "image": {
            "title": "Yahoo! Weather",
            "width": 142,
            "height": 18,
            "link": "http://weather.yahoo.com",
            "url": "http://l.yimg.com/a/i/brand/purplelogo//uh/us/news-wea.gif"
          },
          "item": {
            "title": "Conditions for Singapore, South West, SG at 09:00 PM SGT",
            "lat": 1.33464,
            "long": 103.726471,
            "link": "http://us.rd.yahoo.com/dailynews/rss/weather/Country__Country/*https://weather.yahoo.com/country/state/city-91792352/",
            "pubDate": "Wed, 14 Jun 2017 09:00 PM SGT",
            "condition": {
              "code": 33,
              "date": "Wed, 14 Jun 2017 09:00 PM SGT",
              "temp": 26,
              "text": "Mostly Clear"
            },
            "forecast": [
              {
                "code": 4,
                "date": "14 Jun 2017",
                "day": "Wed",
                "high": 28,
                "low": 25,
                "text": "Thunderstorms"
              }
            ],
            "description": "<![CDATA[<img src=\"http://l.yimg.com/a/i/us/we/52/4.gif\"/>\n<BR />\n<b>Current Conditions:</b>\n<BR />Thunderstorms\n<BR />\n<BR />\n<b>Forecast:</b>\n<BR /> Fri - Thunderstorms. High: 30Low: 25\n<BR /> Sat - Thunderstorms. High: 28Low: 25\n<BR /> Sun - Thunderstorms. High: 28Low: 25\n<BR /> Mon - Thunderstorms. High: 28Low: 25\n<BR /> Tue - Thunderstorms. High: 28Low: 25\n<BR />\n<BR />\n<a href=\"http://us.rd.yahoo.com/dailynews/rss/weather/Country__Country/*https://weather.yahoo.com/country/state/city-91792352/\">Full Forecast at Yahoo! Weather</a>\n<BR />\n<BR />\n(provided by <a href=\"http://www.weather.com\" >The Weather Channel</a>)\n<BR />\n]]>",
            "guid": "string"
          }
        }
      }
    }
   }
  ```


### Activity: Swagger Editor

1. Paste [this YAML file](/learnapidoc/docs/rest_api_specifications/openapi_weather.yml) into [Swagger Editor](https://editor.swagger.io/) and make updates.
2. Go to [this SwaggerHub API](https://app.swaggerhub.com/apis/IdRatherBeWriting/MashapeWeatherAPI/2.3). Observe Generate Client SDK options.

### Activity: Swagger UI

1. Download [Swagger UI](https://github.com/swagger-api/swagger-ui/tree/v3.4.1).
2. Uncompress and pull out the **dist** folder.
3. Save this file locally:  [http://idratherbewriting.com/learnapidoc/docs/rest_api_specifications/openapi_weather.yml](/learnapidoc/docs/rest_api_specifications/openapi_weather.yml) into the **dist** folder.
4. Reference **openapi_weather.yml** in place of the default `url` value.
5. Open in Firefox.

## Part III: Non-reference content in API docs

Slides: [Non-reference content in API docs](http://idratherbewriting.com/nonref-content-api-docs/#/)

###  Activity: GitHub workflow

1.  Create new repo and initialize with readme. Clone repo locally using `git clone`.
2.  Make update to readme file and push back into repo:

```
git add .
git commit -m "made update to readme"
git pull
git push
```
