---
title: PyRHEED
summary: RHEED analysis and simulation
tags:
- Computer Vision
date: "2021-10-31"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: Domain boundaries simulation
  focal_point: Smart

links:
- icon: github
  icon_pack: fab
  name: Follow
  url: https://github.com/yux1991
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
# slides: example
---

This project is used for reflection high energy electron diffraction (RHEED) data analysis and theoretical simulation. RHEED is an electron diffraction technique using a relatively high energy (5~30 keV) beam of electrons with a grazing incident angle. It is very surface sensitive, with a penetration depth of only a few nanometers. Since the scattering factor of electrons is about four orders magnetude higher than that of X-ray, RHEED is especially suitable to characterize 2D materials such as graphene which can hardly be detected using XRD. Another merit of RHEED is that the spot size is very large (~1 cm), which enables it to measure the wafer-scale average of the material's properties including the lattice constants, grain orientation distribution and even defect density.

It is written and tested with Python 3.6.6 (64 bit). The GUI is created using PyQt5. The simulate_RHEED module utilized the pymatgen library to read CIF files and create structures. Major features include:

* RHEED raw image process using rawpy and intensity profile extraction which is accelerated by numpy vecterization. Construction of 2D reciprocal space map and pole figure is automated. The 3D data could be saved as `*.vtp` format, which could be processed by paraview.
* Batch fit RHEED line profiles with pre-defined peak functions (including Gaussian function and Voigt function) and save the formatted results.
* Visualize the fit results and generate a report.
* Simulate the statistical factor from a Markov process, assuming a certain distribution of step density on a hexagonal surface. More details are disscussed in the paper by Spadacini et al. (DOI: 10.1016/0039-6028(83)90492-2).
* Read the crystal structure from a CIF file and create a customized structure by stacking different crystalline materials together. Calculate the diffraction pattern from this structure based on the kinematic diffraction theory.
* Simulate the reciprocal 3D structure from a given structure. The atomic model can be created within this program. It is especially designed to simulate the diffraction from a 2D translational antiphase domain model, see details in the paper by Lu et al. (DOI: 10.1016/0039-6028(81)90541-0).
