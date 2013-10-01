---
layout: post
title:  "Recursively Scraping A Blog With Scrapy"
date:   2012-03-13 17:54:16
author: Milinda Pathirage
categories: python scrapy
excerpt: This is a sample post explaining capabilities of Jekyll framework for beginners. You need to put all your posts under _posts directory.
---

[Scrapy](http://scrapy.org) is a web crawling and scraping framework
written in python. The framework is really simple to understand and easy
to get started with. If you know little bit of Python, you should be
able to build your own web scraper within few minutes. In this post I'm
going to describe how you can use Scrapy to build recursive blog
crawler. Building a recursive scraper using Scrapy is pretty simple, yet
it's getting started guide doesn't help people who are unfamiliar with
the framework to write a recursive scraper.

I'm going to use [blog.scrapy.org](http://blog.scrapy.org) as the target
blog and techniques I am discussing will work on other sites as well
with simple changes to information extraction queries. If you are new to
Scrapy it's required to read the [Scrapy tutorial](http://doc.scrapy.org/en/latest/intro/tutorial.html) first.
I also assume that you have Scrapy [installed](http://doc.scrapy.org/en/latest/intro/install.html) in your machine.

Let's create a Scrapy project first using following command:

{% highlight bash %}
scrapy startproject scrapy_sample
{% endhighlight %}

## Defining the scrapy item
Next step is to define the Item which is the container Scrapy spider
used to store the scraped data. I'm going to extract the blog post link,
post title and text content of the post. So my Item definition will look like
following.

{% highlight python %}
from scrapy.item import Item, Field

class ScrapySampleItem(Item):
    title = Field()
    link = Field()
    content = Field()
{% endhighlight %}

## Implementing the spider

Our spider will define initial URL to download content from, how to
follow pagination links and how to extract blog posts in a page and
creating items from the posts.

Your spider class must be a subclass of [scrapy.spider.BaseSpider](http://doc.scrapy.org/en/latest/topics/spiders.html#scrapy.spider.BaseSpider) and
you need to define three main mandatory attributes.

- **name** : Unique identifier for the spider
- **start_urls** : List of URLs to begin crawling
- **parse()** : Method which will be called with the downloaded
  [Response](http://doc.scrapy.org/en/latest/topics/request-response.html#scrapy.http.Response) object for each start URL. Code related to parsing and data
  extraction will go under this.
	

Our spider implementation will look like following:

{% highlight python %}
from scrapy.spider import BaseSpider
from scrapy.selector import HtmlXPathSelector
from scrapy.http.request import Request
from scrapy_sample.items import ScrapySampleItem

class ScrapyOrgSpider(BaseSpider):
    name = "scrapy"
    allowed_domains = ["scrapy.org"]
    start_urls = ["http://blog.scrapy.org/"]

    def parse(self, response):
        hxs = HtmlXPathSelector(response)

        next_page =
            hxs.select("//div[@class='pagination']/a[@class='next_page']/@href").extract()
        if not not next_page:
            yield Request(next_page[0], self.parse)

        posts = hxs.select("//div[@class='post']")
        items = []
        for post in posts:
            item = ScrapySampleItem()
            item["title"] = post.select("div[@class='bodytext']/h2/a/text()").extract()
            item["link"] = post.select("div[@class='bodytext']/h2/a/@href").extract()
            item["content"] = post.select("div[@class='bodytext']/p/text()").extract()
            items.append(item)
        for item in items:
            yield item
{% endhighlight %}

First we create [HtmlXpathSelector](http://doc.scrapy.org/en/latest/topics/selectors.html#scrapy.selector.HtmlXPathSelector) giving the response object.
This will allow you to select elements in response HTML using [XPath](http://www.w3.org/TR/xpath) [selectors](http://doc.scrapy.org/en/latest/topics/selectors.html#topics-selectors). Then we extract the link to the next page of the blog using **"//div[@class='pagination']/a[@class='next_page']/@href"** XPath selector and selector you need to use in your code will depend on the web site you are going to crawl. Once we get the URL of the next page we check whether there are any URLs in the retirned list by selector, because last page will not have a next page link and Scrapy will throw a error when tried to go to empty URL while in the last page of the crawl. Main trick here is we are returning a python generator for the recursive call. You can learn more about reason behind this from this [stackoverflow conversation](http://stackoverflow.com/questions/231767/the-python-yield-keyword-explained). Last thing we are doing inside our parse method is extracting blog posts in the current page and creating list of Scrapy Items for blog posts.

## Running the scraper

Now you can execute your scraper by  running following command while in
the root directory of your Scrapy project.
{% highlight bash %}
scrapy crawl scrapy
{% endhighlight %}

Scrapy allows you to save the scraped items into a JSON formatted file.
All you have to do is add **-o filename.json -t json** option to previous
crawl command. This will save the scraped items into a JSON file with
the given name.

You can find more information about Scrapy from [here](http://doc.scrapy.org/en/latest/index.html#section-basics). I strongly recommend you to read the full documentation if you like to dig deeper into Scrapy.

<div class="alert alert-success">
<strong>Source code for the sample can be found <a href="https://github.com/milinda/Scrapy-Sample">here</a>.</strong>
</div>

