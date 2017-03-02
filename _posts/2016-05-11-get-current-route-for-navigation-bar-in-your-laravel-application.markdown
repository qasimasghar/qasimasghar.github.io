---
layout: post
title:  "Get current route for navigation bar in your Laravel application"
date:   2016-05-11 18:47:29 +0000
categories: laravel
---
Any navigation bar would need an active class applied to each link when a user has navigated to the corresponding page.

Doing that in Laravel with a helper function is clean and easy.

## Add helper file

First you must create a helpers.php file in your project.

This can be created under the app directory.

{% highlight bash %}
/app/helpers.php
{% endhighlight %}

The helpers.php file needs to be registered in your composer.json file under *autoload*.

{% highlight json %}
"autoload": {
        "files" : [
            "app/helpers.php"
        ]
},
{% endhighlight %}

## Create helper function

You can use the _helper.php_ file to declare functions that can be used anywhere in your Laravel application. 

Below is a basic function that will compare the current route to a specified parameter and return an active class if true.

{% highlight php %}
<?php

if (! function_exists('currentRouteActive')) {
    function currentRouteActive($routeName)
    {
        if (Route::getCurrentRoute()->getName() === $routeName) {
            return ' class=active';
        }
    }
}
{% endhighlight %}

This means if the user is currently on a page related to any route on a navigation bar, the related link will be have an active class that can be highlighted through styling.

## Add helper function to blade template

The helper function can be added to a blade file containing the navigation element.

{% highlight php %}
<nav>
    <ul>
        <li {{ currentRouteActive('home') }}>
            <a href="{{ route('home') }}">Home</a>
        </li>
        <li {{ currentRouteActive('about') }}>
            <a href="{{ route('about') }}">About</a>
        </li>
        <li {{ currentRouteActive('contact') }}>
            <a href="{{ route('contact') }}">Contact</a>
        </li>
    </ul>
</nav> 
{% endhighlight %}

The basic example above shows how this can be used in blade file.

## Summary

Adding helper functions to your application can help you write clean code that is easy to maintain. 

Although using helper functions seems very convenient, it can be easy to add functions in there that would be better suited in classes of their own. To get an idea of what sort of functions should be included in helper files, you should refer to the default helpers included in Laravel.

## Like this?

If you like this article, please follow me at [@qasimaasghar](https://twitter.com/qasimaasghar){:target="_blank"} to keep up to date on my thoughts.

If I've made a mistake in something I have written please tweet me and help me make it right!