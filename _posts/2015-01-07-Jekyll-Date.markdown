---
layout: blogs_item
title: GithubPages+Jekyll模板中各类型对象的方法介绍
author: AcePeak
categories:
  - 积累
tags:
  - 转载
  - Jekyll
  - Liquid
---

Jekyll 使用Liquid来处理模板数据。在建立中文博客的过程中，常常会苦于无法在文章中显示中文或阿拉伯数字形式日期的问题，而网上绝大多数给出的方案都只是官方的文档给出的 {{ page.date | date_to_string }}。为了能够了解Jekyll模板中不同对象究竟有哪些可以使用的方法，写下此文。

在Liquid中，以上面的语句为例，page为object对象，page.date为attribute属性，后面的date_to_string叫做filter过滤器。请参考Liquid官网[关于Objects的介绍](http://docs.shopify.com/themes/liquid-documentation/objects)。而在Jekyll中page被叫做Global Variables全局变量，而每个全局变量拥有的多个属性被称为子变量，如Site全局变量的子变量为Site Variables。 请参考官网的[变量介绍一页](http://jekyllrb.com/docs/variables/)。

不同的属性拥有不同的类型，有的属于数组，有的属于字符，有的属于日期时间等等，下面分别介绍不同类型属性的过滤器：

#数组过滤器

主要包括以下对象：

> * site.pages
> * site.posts
> * site.related_posts
> * site.static_files
> * site.html_pages
> * site.collections
> * site.data
> * site.documents
> * site.categories
> * site.categories.CATEGORY
> * site.tags
> * site.tags.TAG
> * site.[CONFIGURATION_DATA]
> * page.categories
> * page.tags
> * paginator.posts

###join

{% highlight ruby %}
{% raw %}{{ product.tags | join: ', ' }}{% endraw %}
{% endhighlight %}
=>
{% highlight ruby %}{% raw %}tag1, tag2, tag3
{% endraw %}
{% endhighlight %}

###first

{% highlight ruby %}{% raw %}<!-- product.tags = "sale", "mens", "womens", "awesome" -->
{{ product.tags | first }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}sale{% endraw %}
{% endhighlight %}

{% highlight ruby %}{% raw %}{% if product.tags.first == "sale" %}
    This product is on sale!
{% endif %}{% endraw %}{% endhighlight %}


###last

{% highlight ruby %}{% raw %}<!-- product.tags = "sale", "mens", "womens", "awesome" -->
{{ product.tags | last }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}awesome{% endraw %}{% endhighlight %}

{% highlight ruby %}{% raw %}{% if product.tags.last == "sale" %}
    This product is on sale!
{% endif %}{% endraw %}{% endhighlight %}

###map

{% highlight ruby %}{% raw %}<!-- collection.title = "Spring", "Summer", "Fall", "Winter" -->
{% assign collection_titles = collections | map: 'title' %}
{{ collection_titles }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}SpringSummerFallWinter
{% endraw %}
{% endhighlight %}

###size

{% highlight ruby %}{% raw %}{{ 'is this a 30 character string?' | size }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}30
{% endraw %}
{% endhighlight %}

###sort

{% highlight ruby %}{% raw %}<!-- products = "a", "b", "A", "B" -->
{% assign products = collection.products | sort: 'title' %}
{% for product in products %}
   {{ product.title }}
{% endfor %}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}A B a b
{% endraw %}{% endhighlight %}

#HTML标签过滤器


###img_tag

{% highlight ruby %}{% raw %}{{ 'smirking_gnome.gif' | asset_url | img_tag: 'Smirking Gnome', 'cssclass1 cssclass2' }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<img src="//cdn.shopify.com/s/files/1/0147/8382/t/15/assets/smirking_gnome.gif?v=1384022871" alt="Smirking Gnome" class="cssclass1 cssclass2" />
{% endraw %}
{% endhighlight %}

###script_tag

{% highlight ruby %}{% raw %}{{ 'shop.js' | asset_url | script_tag }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<script src="//cdn.shopify.com/s/files/1/0087/0462/t/394/assets/shop.js?28178" type="text/javascript"></script>
{% endraw %}
{% endhighlight %}

###stylesheet_tag

{% highlight ruby %}{% raw %}{{ 'shop.css' | asset_url | stylesheet_tag }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<link href="//cdn.shopify.com/s/files/1/0087/0462/t/394/assets/shop.css?28178" rel="stylesheet" type="text/css" media="all" />
{% endraw %}{% endhighlight %}


#数学函数过滤器


> 主要包括以下对象：
> * paginator.per_page
> * paginator.total_posts
> * paginator.total_pages
> * paginator.page
> * paginator.previous_page
> * paginator.previous_page_path
> * paginator.next_page
> * paginator.next_page_path


###ceil

{% highlight ruby %}{% raw %}{{ 4.6 | ceil }}
{{ 4.3 | ceil }} {% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}5
5
{% endraw %}
{% endhighlight %}

###divided_by

{% highlight ruby %}{% raw %}<!-- product.price = 200 -->
{{ product.price | divided_by: 10 }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}20
{% endraw %}
{% endhighlight %}

###floor

{% highlight ruby %}{% raw %}{{ 4.6 | floor }}
{{ 4.3 | floor }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}4
4
{% endraw %}
{% endhighlight %}

###minus

{% highlight ruby %}{% raw %}<!-- product.price = 200 -->
{{ product.price | minus: 15 }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}185

{% endraw %}
{% endhighlight %}

###plus

{% highlight ruby %}{% raw %}<!-- product.price = 200 -->
{{ product.price | plus: 15 }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}215

{% endraw %}
{% endhighlight %}

###round

{% highlight ruby %}{% raw %}{{ 4.6 | round }}
{{ 4.3 | round }}
{{ 4.5612 | round: 2 }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}5
4
4.56
{% endraw %}
{% endhighlight %}

###times

{% highlight ruby %}{% raw %}<!-- product.price = 200 -->
{{ product.price | times: 1.15 }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}230{% endraw %}
{% endhighlight %}

###modulo

{% highlight ruby %}{% raw %}{{ 12 | modulo:5 }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}2
{% endraw %}
{% endhighlight %}

#货币函数过滤器


###money

{% highlight ruby %}{% raw %}{{ 145 | money }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- if "HTML without currency" is ${{ amount }} -->
$1.45
<!-- if "HTML without currency" is €{{ amount_no_decimals }} -->
€1
{% endraw %}
{% endhighlight %}

###money_with_currency

{% highlight ruby %}{% raw %}{{ 1.45 | money_with_currency }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- if "HTML with currency" is ${{ amount }} CAD -->
$1.45 CAD
{% endraw %}
{% endhighlight %}

###money_without_currency

{% highlight ruby %}{% raw %}{{ 145 | money_without_currency }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}1.45
{% endraw %}
{% endhighlight %}


#字符串过滤器


> 主要包括以下对象：
> * page.content
> * page.title
> * page.excerpt
> * page.url
> * page.id
> * page.path


###append

{% highlight ruby %}{% raw %}{{ 'sales' | append: '.jpg' }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}sales.jpg
{% endraw %}
{% endhighlight %}

###camelcase

{% highlight ruby %}{% raw %}{{ 'coming-soon' | camelcase }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}ComingSoon
{% endraw %}
{% endhighlight %}

###capitalize

{% highlight ruby %}{% raw %}{{ 'capitalize me' | capitalize }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}Capitalize me

{% endraw %}
{% endhighlight %}

###downcase

{% highlight ruby %}{% raw %}{{ 'UPPERCASE' | downcase }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}uppercase
{% endraw %}
{% endhighlight %}

###escape

{% highlight ruby %}{% raw %}{{ "<p>test</p>" | escape }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %} <!-- The <p> tags are not rendered -->
<p>test</p>
{% endraw %}
{% endhighlight %}

###handle/handleize

{% highlight ruby %}{% raw %}{{ '100% M & Ms!!!' | handleize }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}100-m-ms
{% endraw %}
{% endhighlight %}

###md5

{% highlight ruby %}{% raw %}<img src="http://www.gravatar.com/avatar/{{ comment.email | remove: ' ' | strip_newlines | downcase | md5 }}" />{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<img src="http://www.gravatar.com/avatar/2a95ab7c950db9693c2ceb767784c201" />
{% endraw %}
{% endhighlight %}

###newline_to_br

{% highlight ruby %}{% raw %}{% capture var %}
One
Two
Three
{% endcapture %}
{{ var | newline_to_br }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}One <br>
Two<br>
Three<br>
{% endraw %}
{% endhighlight %}

###pluralize

{% highlight ruby %}{% raw %}{{ cart.item_count }}
{{ cart.item_count | pluralize: 'item', 'items' }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}3 items
{% endraw %}
{% endhighlight %}

###prepend

{% highlight ruby %}{% raw %}{{ 'sale' | prepend: 'Made a great ' }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}Made a great sale

{% endraw %}
{% endhighlight %}

###remove

{% highlight ruby %}{% raw %}{{ "Hello, world. Goodbye, world." | remove: "world" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}Made a great saleHello, . Goodbye, .
{% endraw %}
{% endhighlight %}

###remove_first

{% highlight ruby %}{% raw %}{{ "Hello, world. Goodbye, world." | remove_first: "world" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}Hello, . Goodbye, world.
{% endraw %}
{% endhighlight %}

###replace

{% highlight ruby %}{% raw %}<!-- product.title = "Awesome Shoes" -->
{{ product.title | replace: 'Awesome', 'Mega' }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}Mega Shoes
{% endraw %}
{% endhighlight %}

###replace_first

{% highlight ruby %}{% raw %}<!-- product.title = "Awesome Awesome Shoes" -->
{{ product.title | replace_first: 'Awesome', 'Mega' }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}Mega Awesome Shoes
{% endraw %}
{% endhighlight %}

###slice

{% highlight ruby %}{% raw %}{{ "hello" | slice: 2 }}
{{ "hello" | slice: 1, 3 }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}e
ell
{% endraw %}{% endhighlight %}

{% highlight ruby %}{% raw %}{{ "hello" | slice: -3, 2  }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}el
{% endraw %}
{% endhighlight %}

###split

{% highlight ruby %}{% raw %}{% assign words = "Uses cheat codes, calls the game boring." | split: ' ' %}
First word: {{ words.first }}
First word: {{ words[0] }}
Second word: {{ words[1] }}
Last word: {{ words.last }}
All words: {{ words | join: ', ' }}
{% for word in words %}
{{ word }}
{% endfor %}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}First word: Uses
First word: Uses
Second word: cheat
Last word: boring.
All words: Uses, cheat, codes,, calls, the, game, boring.

Uses cheat codes, calls the game boring.
{% endraw %}
{% endhighlight %}

###strip

{% highlight ruby %}{% raw %}{{ '   too many spaces      ' | strip }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}too many spaces
{% endraw %}
{% endhighlight %}

###lstrip

{% highlight ruby %}{% raw %}{{ '   too many spaces           ' | lstrip }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- Notice the empty spaces to the right of the string -->
too many spaces
{% endraw %}
{% endhighlight %}

###rstrip

{% highlight ruby %}{% raw %}{{ '   too many spaces      ' | rstrip }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}                 too many spaces
{% endraw %}
{% endhighlight %}

###strip_html

{% highlight ruby %}{% raw %}{{ "<h1>Hello</h1> World" | strip_html }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}Hello World
{% endraw %}
{% endhighlight %}

###strip_newlines

{% highlight ruby %}{% raw %}{{ product.description | strip_newlines }}{% endraw %}{% endhighlight %}

###truncate

{% highlight ruby %}{% raw %}{{ "The cat came back the very next day" | truncate: 10 }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}The cat...
{% endraw %}
{% endhighlight %}

###truncatewords

{% highlight ruby %}{% raw %}{{ "The cat came back the very next day" | truncatewords: 4 }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}The cat came back...
{% endraw %}
{% endhighlight %}

###uniq

{% highlight ruby %}{% raw %}{% assign fruits = "orange apple banana apple orange" %}
{{ fruits | split: ' ' | uniq | join: ' ' }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}orange apple banana
{% endraw %}
{% endhighlight %}

###upcase

{% highlight ruby %}{% raw %}{{ 'i want this to be uppercase' | upcase }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}I WANT THIS TO BE UPPERCASE
{% endraw %}
{% endhighlight %}


###url_escape

{% highlight ruby %}{% raw %}{{ "<hello> & <shopify>" | url_escape }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}%3Chello%3E%20&%20%3Cshopify%3E
{% endraw %}
{% endhighlight %}


###url_param_escape

{% highlight ruby %}{% raw %}{{ "<hello> & <shopify>" | url_param_escape }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}%3Chello%3E%20%26%20%3Cshopify%3E
{% endraw %}
{% endhighlight %}


###number_of_words

{% highlight ruby %}{% raw %}{{ page.content | number_of_words }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}1337
{% endraw %}
{% endhighlight %}


###array_to_sentence_string

{% highlight ruby %}{% raw %}{{ page.tags | array_to_sentence_string }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}foo,bar,and baz
{% endraw %}
{% endhighlight %}



#日期过滤器


> 主要包括以下对象：
> * site.time
> * page.date


{% highlight ruby %}{% raw %}{{ article.published_at | date: "%a, %b %d, %y" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}Tue, Apr 22, 14
{% endraw %}
{% endhighlight %}

###%a:Abbreviated weekday.

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%a" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- Sat -->
{% endraw %}
{% endhighlight %}

###%A:Full weekday name.

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%A" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- Tuesday -->
{% endraw %}
{% endhighlight %}

###%b:Abbreviated month name.

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%b" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- Jan -->
{% endraw %}
{% endhighlight %}

###%B:Full month name

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%B" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- January -->
{% endraw %}
{% endhighlight %}

###%c:Preferred local date and time representation

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%c" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- Tue Apr 22 11:16:09 2014 -->
{% endraw %}
{% endhighlight %}

###%d:Day of the month, zero-padded (01, 02, 03, etc.).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%d" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 04 -->
{% endraw %}
{% endhighlight %}

###%-d:Day of the month, not zero-padded (1,2,3, etc.).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%-d" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 4 -->
{% endraw %}
{% endhighlight %}

###%D:Formats the date (dd/mm/yy).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%D" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 04/22/14 -->
{% endraw %}
{% endhighlight %}


###%e:Day of the month, blank-padded ( 1, 2, 3, etc.).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%e" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 3 -->
{% endraw %}
{% endhighlight %}

###%F:Returns the date in ISO 8601 format (yyyy-mm-dd).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%F" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 2014-04-22 -->
{% endraw %}
{% endhighlight %}


###%H:Hour of the day, 24-hour clock (00 - 23).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%H" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 15 -->
{% endraw %}
{% endhighlight %}

###%I:Hour of the day, 12-hour clock (1 - 12).


{% highlight ruby %}{% raw %}{{ article.published_at | date: "%I" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 7 -->
{% endraw %}
{% endhighlight %}


###%j:Day of the year (001 - 366).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%j" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 245 -->
{% endraw %}
{% endhighlight %}


###%k:Hour of the day, 24-hour clock (1 - 24).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%k" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 14 -->
{% endraw %}
{% endhighlight %}


###%m:Month of the year (01 - 12).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%m" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 04 -->
{% endraw %}
{% endhighlight %}


###%M:Minute of the hour (00 - 59).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%M" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!--53-->
{% endraw %}
{% endhighlight %}


###%p:Meridian indicator (AM/PM).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%p" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- PM -->
{% endraw %}
{% endhighlight %}


###%r:12-hour time (%I:%M:%S %p)

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%r" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 03:20:07 PM -->
{% endraw %}
{% endhighlight %}


###%R:24-hour time (%H:%M)

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%R" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 15:21 -->
{% endraw %}
{% endhighlight %}


###%T:24-hour time (%H:%M:%S)

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%T" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 15:22:13 -->
{% endraw %}
{% endhighlight %}


###%U:The number of the week in the current year, starting with the first Sunday as the first day of the first week.

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%U" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 16 -->
{% endraw %}
{% endhighlight %}


###%W:The number of the week in the current year, starting with the first Monday as the first day of the first week.

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%W" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 16 -->
{% endraw %}
{% endhighlight %}


###%w:Day of the week (0 - 6, with Sunday being 0).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%w" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 2 -->
{% endraw %}
{% endhighlight %}


###%x:Preferred representation for the date alone, no time. (mm/dd/yy).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%x" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 04/22/14 -->
{% endraw %}
{% endhighlight %}


###%X:Preferred representation for the time. (hh:mm:ss).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%X" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 13:17:24 -->
{% endraw %}
{% endhighlight %}


###%y:Year without a century (00.99).

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%y" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 14 -->
{% endraw %}
{% endhighlight %}


###%Y:Year with a century.

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%Y" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- 2014 -->
{% endraw %}
{% endhighlight %}


###%Z:Time zone name.

{% highlight ruby %}{% raw %}{{ article.published_at | date: "%Z" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- EDT -->
{% endraw %}
{% endhighlight %}


###date_to_xmlschema

{% highlight ruby %}{% raw %}{{ site.time | date_to_xmlschema }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}2008-11-17T13:07:54-08:00
{% endraw %}
{% endhighlight %}


###date_to_string

{% highlight ruby %}{% raw %}{{ site.time | date_to_string }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}17 Nov 2008
{% endraw %}
{% endhighlight %}


###date_to_long_string

{% highlight ruby %}{% raw %}{{ site.time | date_to_long_string }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}17 November 2008
{% endraw %}
{% endhighlight %}


#其他过滤器


###default

{% highlight ruby %}{% raw %}Dear {{ customer.name | default: "customer" }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- if customer.name is nil -->
Dear customer
{% endraw %}
{% endhighlight %}

###default_errors

{% highlight ruby %}{% raw %}{% if form.errors %}
      {{ form.errors | default_errors }}
{% endif %}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- if form.errors returned "email" -->
Please enter a valid email address.
{% endraw %}
{% endhighlight %}

###default_pagination

{% highlight ruby %}{% raw %}{{ paginate | default_pagination }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<span class="page current">1</span>
<span class="page"><a href="/collections/all?page=2" title="">2</a></span>
<span class="page"><a href="/collections/all?page=3" title="">3</a></span>
<span class="deco">&hellip;</span>
<span class="page"><a href="/collections/all?page=17" title="">17</a></span>
<span class="next"><a href="/collections/all?page=2" title="">Next &raquo;</a></span>
{% endraw %}
{% endhighlight %}

###highlight

{% highlight ruby %}{% raw %}{{ item.content | highlight: search.terms }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<!-- If the search term was "Yellow" -->
<strong class="highlight">Yellow</strong> shirts are the best!
{% endraw %}
{% endhighlight %}

###highlight_active_tag

{% highlight ruby %}{% raw %}<!-- collection.tags = ["Cotton", "Crew Neck", "Jersey"] -->
{% for tag in collection.tags %}
    {{ tag | highlight_active | link_to_tag: tag }}
{% endfor %}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}<a title="Show products matching tag Cotton" href="/collections/all/cotton"><span class="active">Cotton</span></a>
<a title="Show products matching tag Crew Neck" href="/collections/all/crew-neck">Crew Neck</a>
<a title="Show products matching tag Jersey" href="/collections/all/jersey">Jersey</a>
{% endraw %}
{% endhighlight %}

###json

{% highlight ruby %}{% raw %}var content = {{ pages.page-handle.content | json }};{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}var content = "\u003Cp\u003E\u003Cstrong\u003EYou made it! Congratulations on starting your own e-commerce store!\u003C/strong\u003E\u003C/p\u003E\n\u003Cp\u003EThis is your shop\u0026#8217;s \u003Cstrong\u003Efrontpage\u003C/strong\u003E, and it\u0026#8217;s the first thing your customers will see when they arrive. You\u0026#8217;ll be able to organize and style this page however you like.\u003C/p\u003E\n\u003Cp\u003E\u003Cstrong\u003ETo get started adding products to your shop, head over to the \u003Ca href=\"/admin\"\u003EAdmin Area\u003C/a\u003E.\u003C/strong\u003E\u003C/p\u003E\n\u003Cp\u003EEnjoy the software,  \u003Cbr /\u003E\nYour Shopify Team.\u003C/p\u003E";
{% endraw %}
{% endhighlight %}

###weight_with_unit

{% highlight ruby %}{% raw %}{{ product.variants.first.weight | weight_with_unit }}{% endraw %}{% endhighlight %}
=>
{% highlight ruby %}{% raw %}24.0 kg
{% endraw %}
{% endhighlight %}
