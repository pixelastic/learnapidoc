---
title: Dive into dot notation
permalink: /docapis_diving_into_dot_notation.html
keywords:
course: "Documenting REST APIs"
weight: 2.91
sidebar: docapis
section: likeadeveloper
path1: /likeadeveloper.html
---

In the previous topic, [Access and print a specific JSON value](docapis_access_json_values.html), you accessed and printed a specific JSON value to the page. Let's dive into dot notation a little more, since understanding how to access the right JSON value you want is key to making use of the response.

* TOC
{:toc}

## Dot notation

You use a dot after the object name to access its properties. For example, suppose you have an object called `data`:

```json
"data": {
"name": "Tom"
}
```

To access `Tom`, you would use `data.name`.

Note the different levels of nesting so you can trace back the appropriate objects and access the information you want. You access each level down through the object name followed by a dot.

## Use square brackets to access the values in an array

To access a value in an array, you use square brackets followed by the position number. For example, suppose you have the following array:

```json
"data" : {
  "items": ["ball", "bat", "glove"]
}
```

To access glove, you would use `data.items[2]`.

`glove` is the third item in the array. (You can't access an item directly in an array by the item's name &mdash; only by its position. Usually, programmers loop through an array and pull out values that match.)

{: .note}
With most programming languages, you usually start counting at `0`, not `1`.

## Exercise with dot notation {#exercise_dot_notation}

{% include activity.html %}

In this activity, you'll practice accessing different values through dot notation.

1. Create a new file in your text editor and insert the following into it:

   ```html
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://code.jquery.com/jquery-2.1.1.min.js"></script>
      <meta charset="utf-8">
      <title>JSON dot notation practice</title>

    <script>
    $( document ).ready(function() {

       var john = {
        "hair": "brown",
        "eyes": "green",
        "shoes": {
            "brand": "nike",
            "type": "basketball"
        },
        "favcolors": [
            "azure",
            "goldenrod"
        ],
        "children": [
            {
                "child1": "Sarah",
                "age": 2
            },
            {
                "child2": "Jimmy",
                "age": 5
            }
        ]
    }

    var sarahjson = john.children[0].child1;
    var greenjson = john.children[0].child1;
    var nikejson = john.children[0].child1;
    var goldenrodjson = john.children[0].child1;
    var jimmyjson = john.children[0].child1;

    $("#sarah").append(sarahjson);
    $("#green").append(greenjson);
    $("#nike").append(nikejson);
    $("#goldenrod").append(goldenrodjson);
    $("#jimmy").append(jimmyjson);
    });
    </script>
    </head>
    <body>

        <div id="sarah">Sarah: </div>
        <div id="green">green: </div>
        <div id="nike">nike: </div>
        <div id="goldenrod">goldenrod: </div>
        <div id="jimmy">Jimmy: </div>

    </body>
    </html>
   ```

    Here we have a JSON object defined as a variable named `john`. (Usually, APIs retrieve the response through a URL request, but for practice here, we're just defining the object locally.)

    If you view the page in your browser, you'll see the page says "Sarah" for each item because we're accessing this value: `john.children[0].child1` for each item.

2. Change `john.children[0].child1` to display the corresponding values for each item. For example, the word `green` should appear at the ID tag called `green`.

You can view the correct page here: [http://idratherbewriting.com/learnapidoc/assets/files/dot-notation-practice.html](/learnapidoc/assets/files/dot-notation-practice.html). This page also shows the answers printed.

## Showing wind conditions on the page

At the beginning of the section on [Using an API like a developer](docapis_scenario_for_using_weather_api.html#endgoal), I showed an example of [embedding the wind speed](docapis_scenario_for_using_weather_api.html#endgoal) and other details on a website. Now let's revisit this code example and see how it's put together.

Copy the following code into a basic HTML page, customize the `APIKEY` value, and view the page in the browser:

```html
<html>
<head>
<script src="http://code.jquery.com/jquery-2.1.1.min.js"></script>
<link rel="stylesheet"  href='https://maxcdn.bootstrapcdn.com/bootstrap/3.3.4/css/bootstrap.min.css' rel='stylesheet' type='text/css'>

  <title>Sample Query to get the wind</title>
<style>
   #wind_direction, #wind_chill, #wind_speed, #temperature, #speed {color: red; font-weight: bold;}
   body {margin:20px;}
</style>
  </head>
<body>


<script>

function checkWind() {

  var settings = {
    "async": true,
    "crossDomain": true,
    "dataType": "json",
    "url": "https://simple-weather.p.mashape.com/weatherdata?lat=37.354108&lng=-121.955236",
    "method": "GET",
    "headers": {
      "accept": "application/json",
      "x-mashape-key": "APIKEY"
    }
}

  $.ajax(settings)

  .done(function (response) {
    console.log(response);

    $("#wind_speed").append (response.query.results.channel.wind.speed);
    $("#wind_direction").append (response.query.results.channel.wind.direction);
    $("#wind_direction").append (" degrees");
    $("#wind_chill").append (response.query.results.channel.wind.chill);
    $("#temperature").append (response.query.results.channel.units.temperature);
    $("#speed").append (response.query.results.channel.units.speed);
  });
}
</script>


<button type="button" onclick="checkWind()" class="btn btn-danger weatherbutton">Check wind conditions</button>

<h2>Wind conditions for Santa Clara</h2>

<b>Wind chill: </b><span id="wind_chill"></span> <span id="temperature"></span></br>
<b>Wind speed: </b><span id="wind_speed"></span> <span id="speed"></span></br>
<b>Wind direction: </b><span id="wind_direction"></span>
</body>
</html>
```
A few things are different here, but it's essentially the same code:

* Rather than running the `ajax` method on page load, the `ajax` method is wrapped inside a function called `checkWind`. When the web page's button is clicked, the `onclick` method fires the `checkWind()` function.
* When `checkWind` runs, the wind chill, speed, and direction values are written to several ID tags on the page. Units for each of these values are also added to the page.
* Some minimal styling is added. Bootstrap is loaded to make the button styling.

When you load the page and click the button, the following should appear:

<a href="http://idratherbewriting.com/learnapidoc/assets/files/wind-mashape.html" class="noExtIcon"><img src="images/windconditionsfinaloutput.png" alt="Final REST API" /></a>

You can view the file <a href="http://idratherbewriting.com/learnapidoc/assets/files/wind-mashape.html">idratherbewriting.com/learnapidoc/assets/files/wind-mashape.html</a>.

## Next section

As you've gone through the exercise of using an API like a developer, you've gained a high-level understanding of how REST APIs work, what information developers need, how they might use an API, how they make requests, evaluate responses, and other details.

With this background, it's time to switch gears and put on your technical writing hat. In the next section, [Documenting endpoints](docendpoints.html), you'll assume the task of [documenting a new endpoint](docapis_new_endpoint_to_doc.html) that was added to the weather API. You'll learn the 8 essential sections in endpoint reference documentation, the terminology to use, and formatting conventions for the reference information.

{% include random_ad.html %}
