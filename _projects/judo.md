---
layout: page
title: Judo
description: web-based traffic simulation
# img: assets/img/3.jpg
importance: 2
category: work
---

Judo is a web application for efficient visualization of traffic simulation data generated using [QarSUMO](https://arxiv.org/abs/2010.03289), a distributed solution built by QCRI on top of an open source micro-traffic simulator, [SUMO](https://www.eclipse.org/sumo/) to accomplish faster simulation times.

Judo takes the output from QarSUMO/SUMO and imports this data into a [geo-spatial database (POSTGIS)](https://postgis.net), exposed through a [FastAPI](https://postgis.net) backend, connected to an [Angular](https://angular.io) frontend, using [PIXI.js](https://pixijs.com) for web graphics.
