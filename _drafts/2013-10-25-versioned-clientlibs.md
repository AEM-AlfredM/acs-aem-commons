---
layout: feature
title: Versioned Clientlibs
description: Set your TTLs on Clientlib JS/CSS to infinity and beyond!
date: 2013-10-01 23:39:29
thumbnail: /images/verisoned-clientlibs/thumbnail.png
categories: features
tags: new
---

## Purpose

Allow CSS and JavaScript served via AEM Clientlibs to be cached client-side with long TTLs.

## How to Use

Add a Sling rewriter configuration node (example below) that includes the `versioned-clientlibs` transformer type to you project. 

The URIs to clienlibs will be rewritten in the format `/path/to/clientlib.last-modified-timestamp.js`

### Note

This re-writer does **NOT** support

* URIs embedded in CSS or JavaScript, including: background-images, web fonts, etc. 
* Relative URIs 
	* etc/clientlibs/mysite/styles.css
* URIs including a scheme
	* http://example.com/etc/clientlibs/mysite/styles.css
	* //example.com/etc/clientlibs/mysite/styles.css
* URIs to non-AEM HtmlClientLibrary resources
	* /etc/designs/mysite.css
 
## Rewriter Configuration Node

	/apps/myapp/config/rewriter/versioned-clientlibs.xml

{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="sling:Folder"
    contentTypes="[text/html]"
    enabled="{Boolean}true"
    generatorType="htmlparser"
    order="{Long}1"
    serializerType="htmlwriter"
    transformerTypes="[linkchecker,versioned-clientlibs]"/>
{% endhighlight %}        