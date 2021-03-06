---
title: What is a REST API?
permalink: /docapis_what_is_a_rest_api.html
keywords:
course: "Documenting REST APIs"
weight: 1.3
sidebar: docapis
section: introtoapis
path1: /docapis_introtoapis.html
redirect_from:
- /docapis_what-is-a-rest-api/
---

This course is all about learning by doing, but while *doing* various activities, I'll periodically pause and dive into some more abstract concepts to fill in more detail. This is one of those deep dive moments. Here we'll dive into what a REST API is, comparing it to other types of APIs like SOAP. REST APIs have common characteristics but no definitive protocols like their predecessors did.


{% if site.format == "web" %}
* TOC
{:toc}
{% endif %}

## What is an API?

In general, an API (or Application Programming Interface) provides an interface between two systems. It's like a cog that allows two systems to interact with each other. In this case, the two systems are computers that interact programmatically through the API.

<figure><a class="noCrossRef" href="http://bit.ly/1DexWM0" class="noExtIcon"><img class="medium" class="small" src="images/spinning_gears.jpg" alt="Spinning gears. By Brent 2.0. Flickr." /></a><figcaption>spinning gears by Brent 2.0</figcaption></figure>

Jim Bisso, an experienced API technical writer in the Silicon Valley area, describes APIs by using the analogy of your computer's calculator. When you press buttons, functions underneath are interacting with other components to get information. Once the information is returned, the calculator presents the data back to the GUI.

<img class="small" src="images/calculator.png" alt="calculator" />

{% include random_ad.html %}

APIs often work in similar ways. When you push a button in an interface, functions underneath also get triggered to go and retrieve information. But instead of retrieving information from within the same system, web APIs call remote services on the web to get their information.

Ultimately, developers use API calls behind the scenes to pull information into their apps. A button on a GUI may be internally wired to make calls to an external service. For example, the embedded Twitter or Facebook buttons that interact with social networks, or embedded Youtube videos that pull a video in from youtube.com, are powered by web APIs underneath.

## APIs that use HTTP protocol are "web services"

A "web service" is a web-based application that provides resources in a format consumable by other computers. Web services include various types of APIs, including both REST and SOAP APIs. Web services are basically request and response interactions between clients and servers (a computer makes the request for a resource, and the web service provides the response).

All APIs that use HTTP protocol as the transport format for requests and responses can be classified as "web services."

## Language agnostic

With web services, the client making the request for the resource and the API server providing the response can use any programming language or platform &mdash; it doesn't matter because the message request and response are made through a common HTTP web protocol.

This is part of the beauty of web services: they are language agnostic and therefore interoperable across different platforms and systems. When documenting a REST API, it doesn't matter whether the API is built with Java, Ruby, Python, or some other language. The requests are made over HTTP, and the responses are returned through HTTP.

Each programming language that makes the request will have a different way of submitting a web request and parsing the response, but the way requests for each language are made and the responses retrieved are common operations for the programming language and not usually specific to a particular REST API.

## SOAP APIs are the predecessor to REST APIs

Before REST became the most popular web service, SOAP (Simple Object Access Protocol) was much more common. To understand REST a little better, it helps to have some context with SOAP. This way you can see what makes REST different.

### SOAP used standardized protocols and WSDL files

SOAP is a standardized protocol that requires XML as the message format for requests and responses. As a standardized protocol, the message format is usually defined through something called a WSDL file (Web Services Description Language).

The WSDL file defines the allowed elements and attributes in the message exchanges. The WSDL file is machine readable and used by the servers interacting with each other to facilitate the communication.

SOAP messages are enclosed in an "envelope" that includes a header and body, using a specific XML schema and namespace. For an example of a SOAP request and response format, see [SOAP vs REST Challenges](http://www.soapui.org/testing-dojo/world-of-api-testing/soap-vs--rest-challenges.html).

### Problems with SOAP and XML: Too heavy, slow

The main problem with SOAP is that the XML message format is too verbose and heavy. It is particularly problematic with mobile scenarios where file size and bandwidth are critical. The verbose message format slows processing times, which makes SOAP interactions lethargic.

SOAP is still used in enterprise application scenarios (especially with financial institutions) with server-to-server communication, but in the past 5 years, SOAP has largely been replaced by REST, especially for APIs on the open web.

## REST is a style, not a standard

Like SOAP, REST (REpresentational State Transfer) uses HTTP as the transport protocol for the message requests and responses. However, unlike SOAP, REST is an architectural style, not a standard protocol. This is why REST APIs are sometimes called _RESTful_ APIs &mdash; REST is a general style that the API follows.

A RESTful API might not follow all of the official characteristics of REST as outlined by [Dr. Roy Fielding](https://en.wikipedia.org/wiki/Roy_Fielding), who first described the model. Hence these APIs are "RESTful" or "REST-like." (Some developers insist on using the term "RESTful" when the API doesn't fulfill all the characteristics of REST, but most people just refer to them as REST APIs regardless.)

## Requests and Responses

The following diagram shows the general model of a REST API:

{% if site.format == "pdf" or site.format == "kindle" %}
<img class="medium" src="images/restapi_restapi.png" alt="REST API" />
{% elsif site.format == "web" %}
<img class="medium" src="images/restapi_restapi.svg" alt="REST API" />
{% endif %}

As you can see, there's a request and a response between a client to the API server. The client and server can be based in any language, but HTTP is the protocol used to transport the message. This request-and-response pattern is fundamentally how REST APIs work.

### Any message format can be used with REST

As an architectural style, you aren't limited to XML as the message format. REST APIs can use any message format the API developers want to use, including XML, JSON, Atom, RSS, CSV, HTML, and more.

Despite the variety of message format options, most REST APIs use JSON (JavaScript Object Notation) as the default message format. This is because JSON provides a lightweight, simple, and more flexible message format that increases the speed of communication. The lightweight nature of JSON also allows for mobile processing scenarios and is easy to parse on the web using JavaScript. In contrast, with XML you have to use XSLT to parse and process the content.

### REST focuses on resources accessed through URLs

Another unique aspect of REST is that REST APIs focus on *resources* (that is, *things*, rather than actions) and ways to access the resources. Resources are typically different types of information. You access the resources through URLs (Uniform Resource Locators), just like going to a URL in your browser retrieves an information resource. The URLs are accompanied by a method that specifies how you want to interact with the resource.

Common methods include GET (read), POST (create), PUT (update), and DELETE (remove). The endpoint usually includes query parameters that specify more details about the representation of the resource you want to see. For example, you might specify (in a query parameter) that you want to limit the display of 5 instances of the resource.

### Sample URLs for a REST API

Here's what a sample endpoint might look like:

```
http://apiserver.com/homes?limit=5&format=json
```

The endpoint shows the whole path to the resource. However, in documentation, we usually separate out this URL into more specific parts:

* The **base path** (or base URL or host) refers to the common path for the API. In the example above, the base path is `http://apiserver.com`.
* The **endpoint** refers to the end path of the endpoint. In the example above, `/homes`.
* The `?limit=5&format=json` part of the endpoint contains query string parameters for the endpoint.

In the example above, this endpoint would get the "homes" resource and limit the result to 5 homes. It would return the response in JSON format.

You can have multiple endpoints that refer to the same resource. Here's one variation:

```
http://apiserver.com/homes/{home id}
```

This might be an endpoint that retrieves a home resource that contains a particular ID. What is transferred back from the server to the client is the "representation" of the resource. The resource may have many different representations (showing all homes, homes that match certain criteria, homes in a specific format, and so on), but here we want to see a home with a particular ID.

{: .tip}
The relationship between resources and methods is often described in terms of "nouns" and "verbs." The resource is the noun because it is an object or thing. The verb is what you're doing with that noun. Combining nouns with verbs is how you form the language in REST.

We'll explore endpoints in much more depth in the sections to come. But I wanted to provide a brief overview here.

### The web itself follows REST

The terminology of "URIs" and "GET requests" and "message responses" transported over "HTTP protocol" might seem unfamiliar, but really this is just the official REST terminology to describe what's happening. Because you've used the web, you're already familiar with how REST APIs work &mdash; the web itself essentially follows a RESTful style.

If you open a browser and go to http://idratherbewriting.com, you're really using HTTP protocol (`http://`) to submit a GET request to the resource available on a web server. The response from the server sends the content at this resource back to you using HTTP. Your browser is just a client that makes the message response look pretty.

{% if site.format == "pdf" or site.format == "kindle" %}<img class="medium" src="images/restapi_www.png" alt="Web as REST API" />
{% elsif site.format == "web" %}<img class="medium" src="images/restapi_www.svg" alt="Web as REST API" />
{% endif %}

You can see this response in curl if you open a terminal prompt and type `curl http://idratherbewriting.com`. (This assumes you have curl installed.)

Because the web itself is an example of RESTful style architecture, the way REST APIs work will likely become second nature to you.

### REST APIs are stateless and cacheable

REST APIs are also stateless and cacheable. Stateless means that each time you access a resource through an endpoint, the API provides the same response. It doesn't remember your last request and take that into account when providing the new response. In other words, there aren't any previously remembered states that the API takes into account with each request.

The responses can also be cached in order to increase the performance. If the browser's cache already contains the information asked for in the request, the browser can simply return the information from the cache instead of getting the resource from the server again.

Caching with REST APIs is similar to caching of web pages. The browser uses the last-modified-time value in the HTTP headers to determine if it needs to get the resource again. If the content hasn't been modified since the last time it was retrieved, the cached copy can be used instead. This increases the speed of the response.

REST APIs have other characteristics, which you can dive more deeply into on this [REST API Tutorial](http://www.restapitutorial.com/lessons/whatisrest.html). One of these characteristics includes links in the responses to allow users to page through to additional items. This feature is called HATEOAS, or Hypermedia As The Engine of Application State.

Understanding REST at a higher, more theoretical level isn't my goal here, nor is this knowledge necessary to document a REST API. However, there are a number of more technical books, courses, and websites that explore REST API concepts, constraints, and architecture in more depth that you can consult if you want to. For example, check out [Foundations of Programming: Web Services by David Gassner](https://www.lynda.com/Software-Development-tutorials/Foundations-Programming-Web-Services/126131-2.html) on lynda.com.

### REST APIs don't use WSDL files, but some specs exist

An important aspect of REST APIs, especially in terms of documentation, is that they don't use a WSDL file to describe the elements and parameters allowed in the requests and responses.

Although there is a possible WADL (Web Application Description Language) file that can be used to describe REST APIs, they're rarely used since the WADL files don't adequately describe all the resources, parameters, message formats, and other attributes the REST API. (Remember that the REST API is an architectural style, not a standardized protocol.)

In order to understand how to interact with a REST API, you have to *read the documentation* for the API. Hooray! This makes the technical writers' role extremely important with REST APIs.

Some formal specifications &mdash; for example, such [OpenAPI](pubapis_swagger_intro.html) and [RAML](pubapis_raml.html) &mdash; have been developed to describe REST APIs. When you describe your API using the OpenAPI or RAML specification, tools that can read those specifications (like [Swagger UI](pubapis_swagger.html) or the [RAML API Console](pubapis_raml.html#deliver-doc-through-the-api-console-project) will generate an interactive documentation output.

The OpenAPI specification document can take the place of the WSDL file that was more common with SOAP. Tools like [Swagger UI](pubapis_swagger.html) that read the specification documents are usually interactive (featuring API Consoles or API Explorers) and allow you to try out REST calls and see responses directly in the documentation.

But don't expect the Swagger UI or RAML API Console documentation outputs to include all the details users would need to work with your API. For example, these outputs won't include info about [authorization keys](docapis_more_about_authorization.html), details about workflows and interdependencies between endpoints, and so on. The Swagger or RAML output usually contains reference documentation only, which typically only accounts for a third of the total needed documentation.

Overall, REST APIs are more varied and flexible than SOAP APIs, and you almost always need to read the documentation in order to understand how to interact with a REST API. As you explore REST APIs, you will find that they differ greatly from one to another (especially the format and display of their documentation sites), but they all share the common patterns outlined here. At the core of any REST API is a request and response transmitted over the web.

## Additional reading

* [REST: a FAQ](https://medium.com/@diogo.lucas/rest-a-faq-b3cd7ed62828), by Diogo Lucas
* [Learn REST: A RESTful Tutorial](http://www.restapitutorial.com/), by Todd Fredrich
