---
layout: post
title: asyncio rate limit example
---

Occassionally, you have to work with REST api's that have strict limits to the number of calls you can make. Here is a quick example of how to implement a rate limiter in asyncio

{% gist acb66a19da0e7f9373e3ae8969583a91 %}
