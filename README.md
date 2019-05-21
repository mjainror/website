

Setup Ruby on Mac (If you have linux or Windows I hope you know how to set it up yourself)
		
		export PATH="/usr/local/opt/openssl/bin:$PATH"  > ~/.bash_profile
		sudo xcode-select --install
		brew install rbenv
		eval "$(rbenv init -)" --> ~/.bash_profile
		rbenv install 2.4.2
		rbenv global 2.4.2
		gem install bundler
		bundle install

-	bundle exec jekyll build

Run the website in your browser: http://127.0.0.1:4000/

Now check the folder _site for the compiled files.

### The Plugin to fix:
_plugins/jekyll-multiple-languages-plugin/jekyll-multiple-languages-plugin.rb


### Problem 1: 

Under _site/id/artikel-saya/index.html search for ReplaceMe

This is what you will find:

```
<article class="post h-entry article">
    <header class="post-header">
        <h1 class="post-title p-name">ReplaceMe</h1>
    </header>
…
```

This is wrong.  ReplaceMe should have been “ReplaceMe Indonesian”.

### Solution:
Under /myarticle.md you see: 
```
title: ReplaceMe
title_id: ReplaceMe Indonesian
```

But it currently always picks title only. It doesn’t respect the languages. For example if you look at the perma links:

```
permalink: /my-article/
permalink_id: /artikel-saya/
```

You will see that the website picks the correct perma link for Indonesian. It would be ideal to have the same for title.

### Problem 2:

Open _includes/head.html

Search this part:
```
{% if page.summary %}
<meta name="description" content="{{ page.summary | escape }}">
{% endif %}
{%if page.tags %}
<meta name="keywords" content="{{ page.tags | join: ', ' | escape }}"/>
{%endif %}
```

I like the same thing here: 
```
summary: Summary in English
summary_id: Summary in Indonesian
```

AND

```
tags: [test1,test2]
tags_id: [ind1,ind2]
```

Let me know if any questions.

Thanks,









