---
layout: post
title: "Portfolio of work with Australia Post"
date: 2019-07-29
permalink: /aus-post-work/
img: https://upload.wikimedia.org/wikipedia/commons/thumb/7/75/2006-2013_Mercedes-Benz_Sprinter_(W_906)_SWB_van%2C_Australia_Post_(2018-11-22).jpg/640px-2006-2013_Mercedes-Benz_Sprinter_(W_906)_SWB_van%2C_Australia_Post_(2018-11-22).jpg
published: true
tags: ["australia post", "report" ]
---

Australia Post is a huge and hugely complicated organisation. They have amazing data (variety, volume, velocity, ...) and to be honest, I was still getting my head around it after almost 2 1/2 years working there!

This post is a summary of the work I was involved with during by time with Australia Post.

**StarTrack Regional Rates Dashboard**

* Provides transparency to regional managers over regional delivery agents’ rates
* Tools: SAP HANA (SQL), Tableau 

**Chian of Responsibility Dashboard**

* Reporting heavy-vehicle safety compliance
* Tools: Alteryx, SAP HANA (SQL), Tableau
 
**StarTrack Subaccount Irregularity Analysis**

* Irregularity analysis of StarTrack subaccount charge data
* Quantification of size of irregularities
* Tools: Python

**Parcel Locker Optimal Placement Analysis**

* Combined Post and publicly available data to assist decision-making to team charged with Parcel Locker rollout
* Tools: SAP HANA, Python, Tableau

**StarTrack Sales Opportunity Analysis**

* Dashboard and analysis for monitoring the progress of sales *opportunities*
* Created feedback-loop and enabled process improvement
* Tools: SAP HANA, Tableau

**Site Access and Leave Analysis**

* Analysis of irregularities in HR data
* Tools: Python, Tableau

**LPO Revenue Analysis**

* Analysis of LPO revenue, staffing and business model 
* Tools: Python

**Transaction fraud detection**

* Random forest model developed to detect fraudulent online transactions
* Results: Model had a recall of ~30% at a false-positive rate of 1:2000
* Tools: Alteryx, R

**Delivery Altering System (DAS) Dashboard**

* Reporting and monitoring DAS implementation
* Strong feedback on requirements elicitation process
* Tools: Tableau, SQL

**GRC Automated Risk Documentation**

* Tool to turn data in risk register into risk summary PDFs for ERC and ARC reporting
* Turned a very manual and onerous process by the risk managers into a fully automated process that allowed the risk managers to focus on the risk content
* Tools: Python, WK HTML to PDF, Markdown (python library)

**Injury Prevention Onboarding Process Analysis**

* Tested effectiveness of new on-boarding processes
* Used bootstrapping to estimate measurement error in injury rates
* Positive client feedback on data viz
* Tool: Python

**Happy Parcels**

* Development of dashboard to summarise parcel *happiness* (i.e. likelihood to experience delays &c.) for call centre agents
* Goals: reduce AHT, reduce repeat calls, increase NPS
* Tools: Google Cloud Platform, BigQuery, Tableau

Technical presentations:
* **Edward Tufte's philosophy on data viz** - I am a massive fan of [Tufte's work](https://www.edwardtufte.com/tufte/)
* **Scatter-density plots** - a method for visualizing correlations between continuous variables with both areas of low and high density ([see implementation examples here](https://stackoverflow.com/questions/20105364/how-can-i-make-a-scatter-plot-colored-by-density-in-matplotlib))
* **Bootstrapping for parameter estimation**
