---
# An instance of the Experience widget.
# Documentation: https://wowchemy.com/docs/page-builder/
widget: experience

# This file represents a page section.
headless: true

# Order that this section appears on the page.
weight: 40

title: Experience
subtitle:

# Date format for experience
#   Refer to https://wowchemy.com/docs/customization/#date-format
date_format: Jan 2006

# Experiences.
#   Add/remove as many `experience` items below as you like.
#   Required fields are `title`, `company`, and `date_start`.
#   Leave `date_end` empty if it's your current employer.
#   Begin multi-line descriptions with YAML's `|2-` multi-line prefix.
experience:
  - title: Data Scientist
    company: Amazon
    company_url: 'https://www.amazon.com/'
    company_logo: org-amz
    location: Bellevue, WA
    date_start: '2021-05-24'
    date_end: ''
    description: |2-
        Responsibilities include:
        
        * Held meetings with the customers to understand the business scope, establish project timeline, present the updates, and reach agreement on the final deliveries.
        * Performed exploratory data analysis and feature engineering to remove outliers, impute missing data and characterize the stationarity/correlation of the raw data.
        * Build the multivariate encoder-decoder attention model with two-head outputs that overcomes the conventional methods’limitations in long-term forecasting and sparse inputs.
        * Deployed the models on native Amazon web service (NAWS) and provided launch support to the customers.
        
  - title: Seismic Imager
    company: CGG
    company_url: 'https://www.cgg.com/'
    company_logo: org-cgg
    location: Houston, TX
    date_start: '2020-01-06'
    date_end: '2021-02-26'
    description: |2-
        Responsibilities include:
        
        * Provided optimal quality control for the input seismic time series data by querying and analyzing information from billions of seismic records with SQL and Hadoop/Spark big-data tools.
        * Processed petabytes of seismic image sets by separating noise from signal using sparse representation, correcting artifacts with convolution/correlation, and applying interpolation with compressed sensing techniques.
        * Created high-fidelity 3D seismic images and velocity models by solving the optimization problem to minimize the square loss between model and data through an iterative gradient descent method.

design:
  columns: '2'
---
