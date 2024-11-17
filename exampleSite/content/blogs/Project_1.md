---
title: "Predictive Maintenance ML System for Industrial Pumps with Cloud Deployment"
date: 2021-10-15T19:53:33+05:30
draft: false
author: "Rahul Pushparajan"
tags:
  - Python
  - Docker
  - AWS
image: /images/projects/Project1.jpg
description: "An end-to-end ML system that predicts industrial pump failures using sensor data, featuring real-time monitoring through a Streamlit dashboard and robust cloud deployment on AWS"
toc: 
---

In realtime Industrial Automation scenarios, the monitoring and maintenance of assets and field devices for a continuous, smooth and efficient run time is important. 

There are many industrial devices and equipments which have intelligent capabilities and has various measuring parameters that are used to monitor its present operating condition and to calculate its performance on long run.

This project aims in predicting the chances of failure of an Industrial motor, used in various environment such as in water treatment systems, power and utility generation, chemical or pharmaceutical production systems or in petrochemical industries.

## Approach

Here I have created a synthetic dataset considering few input parameters such as :

- Pressure (PSI)
- Temperature (degC)
- Vibration (mm/s)
- FLow Rate (gal/min)

and few output parameters such as :

- Power (kW)
- RPM 

The dataset was created using the below code snippet:

<script src="https://gist.github.com/pushparajanrahul/26cebe5f2ab80d46f532e3209543b14f.js"></script>

   [Built-in Shortcodes](https://gohugo.io/content-management/shortcodes/#use-hugo-s-built-in-shortcodes) for rich content, along with a [Privacy Config](https://gohugo.io/about/hugo-and-gdpr/) and a set of Simple Shortcodes that enable static and no-JS versions of various social media embeds.

## Gist Simple Shortcode
```
{{< gist pushparajanrahul 26cebe5f2ab80d46f532e3209543b14f "data_generator.py" >}}
```
<br>
{{< gist pushparajanrahul 26cebe5f2ab80d46f532e3209543b14f "data_generator.py" >}}
<br>



## Twitter Simple Shortcode
```
{{</* tweet GoHugoIO 1315233626070503424 */>}}
```
<br>
{{< tweet GoHugoIO 1315233626070503424 >}}
<br>



## Vimeo Simple Shortcode
```
{{</* vimeo 146022717 */>}}
```
<br>
{{< vimeo 146022717 >}}
<br>



## Youtube Simple Shortcode
```
{{</* youtube w7Ft2ymGmfc */>}}
```
<br>
{{< youtube w7Ft2ymGmfc >}}
<br>

## Theme Custom Shortcodes

These shortcodes are not Hugo built-ins, but are provided by the theme.

### Responsive Images with Cloudinary

You can learn more about this [here](https://cloudinary.com/documentation/responsive_images).

Set the `cloudinary_cloud_name` parameter in your site config to use this shortcode.

```
{{</* dynamic-img src="/my/image/on/cloudinary" title="A title for the image" */>}}
```

Note that you do not include the file extension (e.g. `.png`) in the `src` parameter, as the shortcode will automatically determine the best quality and format for the user's device.

Optionally, you can customize the general CSS styles for the image:

```
{{</* dynamic-img src="/my/image/on/cloudinary" title="A title for the image" style="max-width:60%" */>}}
```
