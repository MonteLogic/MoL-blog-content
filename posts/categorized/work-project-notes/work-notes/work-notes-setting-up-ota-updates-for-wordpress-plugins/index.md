---
title: "Work Notes: Setting up OTA updates for WordPress plugins"
date: "2023-04-21"
---

So I have to have the plugin on my server, here is the link to the zip which is publicly available. (https://ec.wp2mag.com/ec-plus-fundraiser/zips/ec-plus-fundraiser.zip)

The official\* [docs](https://make.wordpress.org/core/2020/07/30/recommended-usage-of-the-updates-api-to-support-the-auto-updates-ui-for-plugins-and-themes-in-wordpress-5-5/) on this topic.

...

I like this testing functionality to check if a php function is being fired in relation to the page:

```
echo '<script>alert(5);</script>';
```
