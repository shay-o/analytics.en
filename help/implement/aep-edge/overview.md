---
title: Implement Adobe Analytics with Adobe Experience Platform Edge
description: Overview of using XDM data from Experience Platform in Adobe Analytics
exl-id: 7d8de761-86e3-499a-932c-eb27edd5f1a3
feature: Implementation Basics
---
# Implement Adobe Analytics with Adobe Experience Platform Edge

Adobe Experience Platform Edge allows you to send data destined to multiple products to a centralized location. Experience Edge forwards the appropriate information to the desired products. This concept allows you to consolidate implementation efforts, especially spanning multiple data solutions.

Adobe offers three main ways to send data to Experience Edge:

* **[Adobe Experience Platform Web SDK](web-sdk/overview.md)**: Use the Web SDK extension in Adobe Experience Platform Data Collection to send data to Edge.
* **[Adobe Experience Platform Mobile SDK](mobile-sdk/overview.md)**: Use the Mobile SDK extension in Adobe Experience Platform Data Collection to send data to Edge.
* **[Adobe Experience Platform Edge Network Server API](server-api/overview.md)**: Send data directly to Edge using an API.



## How Adobe Analytics handles Experience Edge data

Data sent to Experience Edge has to conform to schemas based on [XDM (Experience Data Model)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en). XDM gives you flexibility in what fields are defined as part of events. When events are routed from Experienc Edge to Adobe Analytics, they are translated into Adobe Analytics' native data structure. You can see how XDM fields are mapped to the Adobe Analytics data structure [here](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en).

### Defining page views and link events

The two main kinds of events in Adobe Analytics are page views and link events. Those events are defined based on certain combinations of XDM fields that correspond to Analytics fields set by AppMeasurement when making pageview (aka `s.t()` ) and link event (aka `s.tl()` )  calls.

The following logic is applied to data sent to the Adobe Experience Edge and forwarded to Adobe Analytics.

| XDM payload contains... | Adobe Analytics... |
|---|---|
| `web.webPageDetails.name` or `web.webPageDetails.URL` and no `web.webInteraction.type` | considers payload a **page view** |
| `web.webInteraction.type` and (`web.webPageDetails.name` or `web.webPageDetails.url`) | considers payload a **link event** <br/>`web.webPageDetails.name` and `web.webPageDetails.URL` are set to `null` |

Note that certain XDM fields that may appear to be related to page views or link events, like `eventType`, `web.webPageDetails.pageViews`, or `web.webInteraction.linkEvents` are completely implementation agnostic and have no relevance for Adobe Analytics.

{style="table-layout:auto"}

