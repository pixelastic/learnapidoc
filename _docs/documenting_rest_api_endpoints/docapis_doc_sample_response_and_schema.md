---
title: "Step 5: Response example and schema (API reference tutorial)"
permalink: /docapis_doc_sample_responses_and_schema.html
keywords:
course: "Documenting REST APIs"
weight: 3.5
sidebar: docapis
section: docendpoints
path1: /docendpoints.html
redirect_from:
- http://idratherbewriting.com/learnapidoc/docapis_doc_sample_responses.html
---

{% include workflow_map.html step="5" map="content/reference_doc_map.html"  %}
{% if site.format == "pdf" or site.format == "kindle" %}
<img src="images/apiref6.png"/>
{% endif %}

> **{{site.data.apirefsections.response_example_and_schema.term}}**: {{site.data.apirefsections.response_example_and_schema.def}}

* TOC
{:toc}

## Example of a response example and response schema

The following is a sample response from the SendGrid API. Their documentation provides a tabbed display with an **Example** on one tab:

<a class="noExtIcon" href="https://sendgrid.com/docs/API_Reference/api_v3.html"><img src="images/sendgridresponseexample1.png" /></a>

And the response **Schema** on another tab:

<a class="noExtIcon" href="https://sendgrid.com/docs/API_Reference/api_v3.html"><img src="images/sendgridresponseexample2.png" /></a>

The definition of the response is called the schema or the model (the terms are used synonymously), and aligns with the [JSON schema language and descriptions](http://json-schema.org/). What works particularly well with the SendGrid example is the use of expand/collapse tags to mirror the same structure as the example, with objects at different levels.

Swagger UI also provides both an example value and a schema or model. For example, in the sample Sunset and sunrise times API doc that I created for the [SwaggerUI activity](/learnapidoc/assets/files/swagger-sunrise-sunset/index.html#/default/getSunriseSunset), you can see a distinction between the response example and the response schema. Here's the **Example Value**:

<a class="noExtIcon" href="/learnapidoc/assets/files/swagger-sunrise-sunset/index.html#/default/getSunriseSunset"><img src="images/sunriseexample.png" alt="Sunrise example value" /></a>

The example response should correspond with the example request. And just as the request example might only include a subset of all possible parameters, the response example might also be a subset of all possible returned information.

However, the *response schema* is comprehensive of all possible properties returned in the response. This is why you need both a response example and a response schema. Here's the response schema for the Sunrise and sunset API:

<a class="noExtIcon" href="/learnapidoc/assets/files/swagger-sunrise-sunset/index.html#/default/getSunriseSunset"><img src="images/sunrisemodelexample.png" alt="Sunrise model" /></a>

The schema or model provides the following:

* Description of each property
* Definition of the data type for each property
* Whether each property is required or optional

If the header information is important to include in the response example (because it provides unique information other than standard [status codes](docapis_doc_status_codes.html)), you can include it as well.

## Do you need to define the response?

Some API documentation omits the response schema because the responses might seem self-evident or intuitive. In Twitter's API, the responses aren't explained (you can see an [example here](https://developer.twitter.com/en/docs/accounts-and-users/manage-account-settings/api-reference/get-account-settings)).

However, most documentation would be better off with the response described, especially if the properties are abbreviated or cryptic. Developers sometimes abbreviate the responses to increase performance by reducing the amount of text sent. In one endpoint I documented, the response included about 20 different two-letter abbreviations. I spent days tracking down what each abbreviation meant, and found that many developers who worked on the API didn't know what many of the responses meant.

One of the problems with the [Mashape Weather API](https://market.mashape.com/fyhao/weather-13) we've been using [as an example](docapis_new_endpoint_to_doc.html) is that it doesn't describe the meaning of the responses. If the air quality index is `25`, is that a good or bad value when compared to `65`? What is the max or min value that the API might return? Further, what exactly does the "air quality index" mean? Also, what longitude and latitude values are supported?

## Use realistic values in the example response

In the example response, the values should be realistic without being real. If developers give you a sample response, make sure each of the possible values are reasonable and not so fake they're distracting (such as users consisting of comic book character names).

Also, the sample response should not contain real customer data. If you get a sample response from an engineer, and the data looks real, make sure it's not just from a cloned production database, which is commonly done. Developers may not realize that the data needs to be fictitious but representative, and scraping a production database may be the easiest approach for them.

## Format the JSON and use code syntax highlighting

Use proper JSON formatting for the response. A tool such as [JSON Formatter and Validator](http://jsonformatter.curiousconcept.com/) can make sure the spacing is correct.

If you can add syntax highlighting as well, definitely do it. If you're using a static site generator such as [Jekyll](pubapis_jekyll.html) or markdown syntax with [GitHub](pubapis_github_wikis.html), you can probably use the [Rouge](https://github.com/jneen/rouge) built-in syntax highlighter. Other static site generators use [Pygments](http://pygments.org/).

Rouge and Pygments rely on "lexers" to indicate how the code should be highlighted. For example, some common lexers are `java`, `json`, `html`, `xml`, `cpp`, `dotnet`, and `javascript`.

If you don't have any syntax highlighters to integrate directly into your tool, you could add syntax highlighting manually for each code sample by pasting it into the [syntaxhighlight.in](http://syntaxhighlight.in/) highlighter.

## Strategies for documenting nested objects

Many times the response contains nested objects (objects within objects), or has repeating elements. Formatting the documentation for the response schema is one of the more challenging aspects of API reference documentation.

Tables are most commonly used. In [Peter Gruenbaum's API tech writing course on Udemy](https://www.udemy.com/api-documentation-1-json-and-xml/), he represents the nested objects using tables with various columns:

<a href="http://idratherbewriting.com/2015/05/22/api-technical-writing-course-on-udemy/" class="noExtIcon"><img src="images/gruenbaumtable.png" alt="Peter Gruenbaum course" /></a>

Gruenbaum's use of tables is mostly to reduce the emphasis on tools and place it more on the content.

The Dropbox API represents the nesting with a slash. For example, `name_details/`, `team/`, and `quota_info` indicate the multiple object levels.

<a href="https://www.dropbox.com/developers/core/docs#disable-token" class="noExtIcon"><img src="images/returnvaluedefinitions.png" alt="Dropbox nested example" /></a>

Other APIs will nest the response definitions to imitate the JSON structure. Here's an example from bit.ly's API:

<a href="http://dev.bitly.com/user_info.html" class="noExtIcon"><img src="images/bitlyresponsedoc.png" alt="Bitly response" /></a>

Multiple levels of bullets is usually an eyesore, but here it serves a purpose that works well without requiring sophisticated styling.

{% include random_ad.html %}

eBay's approach is a little more unique. In this case, `MinimumAdvertisedPrice` is nested inside `DiscountPriceInfo`, which is nested in `Item`, which is nested in `ItemArray`. (Note also that this response is in XML instead of JSON.)

<a href="http://developer.ebay.com/Devzone/shopping/docs/CallRef/FindPopularItems.html" class="noExtIcon"><img src="images/ebaycode.png" alt="eBay nested example" /></a>

Here's the response documentation:

<a href="http://developer.ebay.com/Devzone/shopping/docs/CallRef/FindPopularItems.html" class="noExtIcon"><img src="images/ebayexampleresponse.png" alt="eBay example response" /></a>

It's also interesting how much detail eBay includes for each item. Whereas the Twitter writers appear to omit descriptions, the eBay authors write small novels describing each item in the response.

## Three-column designs

Some APIs put the response in a right column so you can see it while also looking at the resource description and parameters. Stripe's API made this three-column design popular:

<a href="https://stripe.com/docs/api#charge_object" class="noExtIcon"><img src="images/stripetripanedesign.png" alt="Stripe's tri-column design" /></a>

Stripe's design juxtaposes the sample response in a right side pane with the response schema in the main window. The idea is that you can see both at the same time. The description won't always line up with the response, which might be confusing. Still, separating the response example from the response schema in separate columns helps differentiate the two.

A lot of APIs have modeled their design after Stripe's. For example, see <a href="https://github.com/tripit/slate">Slate</a>, <a href="https://github.com/sourcey/spectacle">Spectacle</a>, or <a href="http://readme.io">readme.io</a>.

Should you use a three-column layout with your API documentation? Maybe. However, if the response example and description doesn't line up, the viewer's focus is somewhat split, and the user must resort to more up-and-down scrolling. Additionally, if your layout uses three columns, your middle column will have some narrow constraints that don't leave much room for screenshots and code examples.

The MYOB Developer Center takes an interesting approach in documenting the JSON in their APIs. They list the JSON structure in a table-like way, with different levels of indentation. You can move your mouse over a field for a tooltip description, or you can click it to have a description expand below. The use of tooltips enables the rows of the example and the description to line up perfectly.

To the right of the JSON definitions is a code sample with real values. When you select a value, both the element in the table and the element in the code sample highlight at the same time.

<a href="http://developer.myob.com/api/accountright/v2/generalledger/account/#GET" class="noExtIcon"><img src="images/myobjsondoc.png" alt="MYOB JSON doc approach" /></a>

This approach facilitates scanning, and the popover + collapsible approach allows you to compress the table so you can jump to the part you're interested in.

However, this approach requires more manual work from a documentation point of view. Still, if you have long JSON objects, it might be worth it.

## Embedding dynamic responses

Sometimes responses are generated dynamically based on API calls to a test system. For example, look at the [Rhapsody API](https://developer.rhapsody.com/api) and click an endpoint &mdash; the response is generated dynamically.

Another API with dynamic responses is the [Open Weather API](https://openweathermap.org/current). When you click a link in the "Examples of API calls" section, such as [http://samples.openweathermap.org/data/2.5/weather?q=London](http://samples.openweathermap.org/data/2.5/weather?q=London,uk&appid=b1b15e88fa797225412429c1c50c122a1), you see the response dynamically returned in the browser.

<a href="http://samples.openweathermap.org/data/2.5/weather?q=London,uk&appid=b1b15e88fa797225412429c1c50c122a1" class="noExtIcon"><img class="medium" src="images/dynamicresponseinbrowser.png"/></a>

The Citygrid API, which we explored in the [requests example topic](docapis_doc_sample_requests.html), also dynamically generates responses.

This approach works well for GET requests that return public information. However, it probably wouldn't scale for other methods (such as POST or DELETE) or which request authorization.

## What about status codes?

The responses section sometimes (briefly) lists the possible status and error codes returned with the responses. However, because these codes are usually common across all endpoints in the API, status and error codes are often documented in their own section, apart from a specific endpoint's documentation. I cover this topic in [Documenting status and error codes](docapis_doc_status_codes.html).

## Response example and schema for the surfreport endpoint

For the `surfreport/{beachId}` endpoint that we've been exploring in our [sample API scenario](docapis_new_endpoint_to_doc.html), let's create a section that shows the response example and schema. Here's my approach for these sections:

<div class="docSample">
{% include_relative surfreport_response.html %}
</div>

## Next steps

Now that you've completed the [API reference tutorial](docapis_api_reference_tutorial_overview.html), you're ready to either critique or create your own API reference topic. See the next topic, [Activity: Critique or create an API reference topic](docapis_api_reference_activity.html).
