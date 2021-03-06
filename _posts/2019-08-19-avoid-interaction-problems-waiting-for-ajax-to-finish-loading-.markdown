---
layout: post
title: Avoid interaction problems waiting for ajax to finish loading.
date: 2019-08-19 10:32:00
description: How to avoid loading interaction problems waiting for ajax to finish loading.
img: xhr-pending.png
tags:
  - Selenium
  - Java
---

Many web interactions send xhr requests, not waiting for this requests to finish ends up with problems of elements not ready to be click or missing elements in the UI, to avoid this we can add a simple method that waits for the requests to finish.

**Wait for xhr to finish**

{% highlight java %}
public static void waitUntilJqueryIsDone(int timeoutInSeconds) {
    until(driver(), (d) ->
    {
      try {
        Boolean isJqueryCallDone = (Boolean) ((JavascriptExecutor) driver()).executeScript("return jQuery.active==0");
        return isJqueryCallDone;
      } catch (Exception e) {
        return e.getMessage().contains("jQuery is not defined");
      }
    }, timeoutInSeconds);
  }
{% endhighlight %}

Above method helps us to wait for all xhr interactions to finish to continue.

Try it and comment if it worked for you.