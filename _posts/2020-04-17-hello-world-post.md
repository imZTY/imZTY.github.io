---
layout: post
title:  "Hello world Post!"
date:   2020-04-17 17:35:50 +0800
categories: jekyll update
permalink: /:categories/:year/:month/:day/:title/
zty:
   yml:
      hello: hello front matter
tags: taga, tagb
excerpt_separator: <!--more-->
---
You’ll find this post in your `_posts` directory. <!--more-->Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

{{ page.zty.yml.hello }}

//itr: page.tags[i]
//len: page.tags.size
{{ page.tags }}

Jekyll requires blog post files to be named according to the following format:
`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

<!-- {% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %} -->

```ruby
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

![首页](https://upload-images.jianshu.io/upload_images/8463645-62686f28d517c842.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

|a|b微软雅黑|c|
|:-|:-|:-|
|11111  一 |2 二微软雅黑 |3333333 三|
|1|222222|3|

>Hello world

Hi,
1. abc
2. def
3. ghj

hello,
* 123
* 456
* 789


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
