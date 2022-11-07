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
  - title: Applied Scientist
    company: Amazon
    company_url: 'https://www.amazon.com/'
    company_logo: org-amz
    location: Seattle, WA
    date_start: '2021-05-24'
    date_end: ''
    description: |2-
        Responsibilities include:

        * Built machine learning models to forecast critical quantities such as shuttle transactions and warehouse transfer arrivals for sales and operations planning at Amazon, saving at least several million dollars per year.
        * Designed new features and expanded the existing ones to support both in-cabin and remote voice based car control capabilities across different regions of the world in the Alexa automotive domain. 
        * Reduced all forms of frictions by building statistical models to derive accurate interpretation of the customer utterances using the latest natural language processing and machine learning technologies.

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

  - title: Research Assistant
    company: Rensselaer Polytehnic Institute
    company_url: 'https://www.rpi.edu/'
    company_logo: org-rpi
    location: Troy, NY 
    date_start: '2015-12-01'
    date_end: '2019-12-31'
    description: |2-
        Responsibilities include:
        
        * Systematically studied the structure, morphology, and electrical transport properties of high-quality SnS epitaxial thin films grown by physical vapor deposition (PVD).
        * Studied the magnetism in VS_2 and MoS_2 using magneto-optical Kerr effect (MOKE) and magnetic force microscopy (MFM).
        * Extracted the three-dimensional probability density distribution of the diffracted electron waves from the preprocessed RHEED datasets by learning the parameters of a Gaussian mixture model.
        * Simulated thousands of crystal domains based on the Voronoi tessellation using Monte Carlo methods, in order to be combined with the experimentally extracted features for model parameter estimation.
        * Estimated the unknown statistics such as the lattice constant, grain size, and preferred orientations from the RHEED images with a Bayesian regression approach.


design:
  columns: '2'
---
