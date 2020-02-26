---
layout: post
comments: true
title:  "Adding Disqus to your Static Jekyll Site!"
date:   2020-01-30 15:45:26 +0500
categories: jekyll update
permalink: /adding-disqus-to-jekyll/
---

Okay so, I thought why not start the blog with something relatively simple and which I have done recently so maybe others can also easily do it.
If you have got your static jekyll site and want to add comments on the amazing articles that you would write in the future, look no further.


At first you want to make sure that you have registered on the [Disqus][disqus-signUp] site and that you know what your `shortname` is.

After that you want to add a directory named `_includes` to your folder you are working in and add a file in it named `disqus_comments.html` and then add the following universal code provided to you when you were setting up the disqus account. Which will look like this:


{% highlight html %}
 

    <div id="disqus_thread"></div>
    <script>
      var disqus_config = function () {
        this.page.url = PAGE_URL; // Replace PAGE_URL with your page's canonical URL variable
          this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
      };

      (function() {  // DON'T EDIT BELOW THIS LINE
        var d = document, s = d.createElement('script');

        s.src = 'https://shortname.disqus.com/embed.js'; // here will be the variable for your shortname in place of example written like this " {{ site.disqus.shortname }} " 

        s.setAttribute('data-timestamp', +new Date());
        (d.head || d.body).appendChild(s);
      })();
    </script>
{% endhighlight %}

The above code will be wrapped in and if statement `if page.comments != false` and  
`jekyll.environment ==production`; By default the jekyll.environment is set to `developement` which disables the comments hence it needs to be changed to production for disqus comments to work. It can be done by running the following command:

`JEKYLL_ENV=production bundle exec jekyll buid`

Now we need to update the `_config.yml` file as follows:

{% highlight ruby %}
  disqus:
    shortname: yourShortName
{% endhighlight %}

That is it for setting up the variables, now all you have to do is add
`comments: true` in post's YAML front matter(you need to specify it for every post so that you can disable comments of any post you wish to).

 
{% highlight ruby %}
  ---
  comments: true
  ---
{% endhighlight %}

Thats it your disqus comment box should be visible below your posts.
If you have any questions feel free to ask me.

_Note:
  In my case I could not get around to changing the environment variable so I have removed the condition for enviornment variable for now so that disqus appears here. I will update the article as soon as I find the way to change the enviornment variable._
  
  _You may also have to wait a couple of hours before the disqus box starts showing properly on your published site._

  _You also want to take into consideration that after every push or update you make to your site it may take disqus to appear after a few minutes or hours._


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
[disqus-signUp]: https://disqus.com/profile/login/
[troubleshooting-guide]: https://help.disqus.com/en/articles/1717301-i-m-receiving-the-message-we-were-unable-to-load-disqus
