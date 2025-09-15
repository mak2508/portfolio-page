---
layout: page
title: SIHA
description: System for Integrated Health Analytics
# img: assets/img/12.jpg
importance: 4
category: work
---

[SIHA](https://siha.qcri.org) (System for Integrated Health Analytics) is a platform developed at QCRI that extracts, unifies, and provides health data from various wearable devices through a unified API infrastructure. This tool was built for use in various research projects including diabetes studies in collaboration with [Weil Cornell Medicine](https://weill.cornell.edu/) and [Hamad Hostpital](https://www.hamad.qa/EN/Pages/default.aspx) (biggest hospital in Qatar).

## Key Features

**Data Processing & Integration**
- Developed YAML interface for [TASRIF](https://github.com/qcri/tasrif), an open-source time-series data processing tool
- Automated collection and harmonization of wearable device data using [Celery](https://docs.celeryq.dev/en/stable/userguide/workers.html) workers
- Standardized data formats for cross-device compatibility, including Huawei, Garmin, Fitbit, Apple, and Samsung watches.

**Secure Infrastructure**
- RESTful API with role-based access controls and OAuth2 authentication to ensure private patient data is secure
- Created on-premise deployment script pulling images from MS Azure for secure deployment

**Analytics & Insights**
- Statistical analysis tools for health trends
- Interactive dashboards for data visualization
- Export capabilities for research and reporting

**Mobile Application**
Took ownership over end-to-end development of the Mobile Application.
- Migrated app to null-safety and BLOC architecture pattern
- Updated UI/UX and created new screens using Flutter for a new coherant brand identity
- Implemented new Team Competitions feature for user engagement

The Mobile Application was a key delivarable for a $\sim$\$3million grant to build a health system across public hospitals in Qatar.
