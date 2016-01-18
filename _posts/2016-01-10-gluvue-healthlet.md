---
title: 'Public GluVue GCM data viewing app a big win'
author: eliot
layout: post
permalink: /gluvue-healthlet
---

<img src="/images/gluvue-screeshot.png" alt="GluVue GCM Data Tool Homepage Screenshot" />

Standford Children's Hospital [gluvue](https://gluvue.stanfordchildrens.org) tool is a single-focused, interactive health app - maybe it's a "healthlet" like a [mathlet](http://mathlets.org/mathlets/)? - that aggregates and visualizes data from a continuous glucose monitoring devices. It's publicly available so for anyone to use. Check out the "Working Demo" off the home screen and play around with it. To use your own data, just [format the GCM data into a simple json structure and post it to an HTTP endpoint](https://gluvue.stanfordchildrens.org/docs/integrate). Since the data contains no PII, there's no additional setup or auth layer necessary. Easy peasy.

Here's why they created it, from the [about page](https://gluvue.stanfordchildrens.org/about/):

"In 2015, the Food and Drug Administration (FDA) approved secure remote monitoring which allows passive CGM data entry from a mobile device into the electronic health record (EHR). The new challenge is in receiving, reviewing, and recognizing patterns in the data because typical views via EHR are cumbersome and non-intuitive."

I love GluVue because:

* it's super focused. It's trying to do one thing and do it well. Something that EHR providers haven't been able to provide yet.
* it has an extremely low barrier for EHR integrations *and* direct patient adoption. Someone has already created the [GluVue Submission Project](http://gluvue.cwconsulting.net/) that helps individuals format and post their own data for various devices into the app. Rockin!
* the visualization and metrics are very digestible and easily understood.

The pending meaningful use rule for stage 3 that supports patient-facing APIs to allow integrations with third-party tools is wonderful. And so are initiatives like FHIR. They are absolutely part of the dreamy future where patient care is improved by further liberating the underlying data. But there are many questions around how these tools are going to evolve and be standardized, how they are going to be secured and still allow for deep integrations. Then there's the significant technical infrastructure investment that providers will need to make to adopt these initiatives.

So while we wait and work on that, GluVue shows that we can leverage more granular tools and simple integration mechanisms that provide a means for patients and orgs to use shared, community-built tools for meaningful and important analysis *right now*. So cool. I just wish the app was open source. Maybe soon? :)
