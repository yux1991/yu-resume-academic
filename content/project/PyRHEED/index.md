---
title: PyRHEED
summary: RHEED analysis and simulation
tags:
- Computer Vision
date: "2021-10-31"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: PyRHEED
  focal_point: Smart

links:
- icon: github
  icon_pack: fab
  name: GitHub Repository
  url: https://github.com/yux1991/PyRHEED
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

## Modules 
- broadening: batch automatic fit of the RHEED line profiles
- browser: browse files inside the working directory
- canvas: display images, draw shapes and take user input
- configuration: change default configurations
- cursor: display cursor-related information
- generate_report: generate a report that visualize the fitting results
- graph_3D_surface: visualize the 3D surface in reciprocal space
- kikuchi: simulate the Kikuchi pattern from a non-reconstructed crystal surface
- main: the main module
- manual_fit: manually fit the RHEED line profile to initialize the fitting parameters
- my_widgets: customized widgets
- plot_chart: a customized widget based on QChart, for visualization of the fitting results
- preference: modify default settings
- process: the backend processes
- process_monitor: monitor the consumption of memory (not complete)
- profile_chart: a customized widget based on QChart, for visualization of the line scan profiles
- properties: control the dynamic parameters of the program
- reciprocal_space_mapping: construct the 2D/3D reciprocal space map and the pole figure
- scenario: select or customize a scenario, then run the scenario
- simulate_RHEED: simulate the diffraction pattern from a given atomic structure. This module is also capable of generating structures containing translational antiphase domain (APD) model and calculating the corresponding diffraction pattern. 
- statistical_factor: calculate the statistical factor assuming a Markov process 
- test: the test module
- translational_antiphase_domain: calculate the 1D and 2D profile from a translational APD model
- window: the main window of the application
- write_scenario: write the default scenario

## Demonstrations
1. Extract line profiles:

![line](https://user-images.githubusercontent.com/38077812/111377405-9a688e00-866e-11eb-8ef2-b25386f10d27.gif)


2. Extract features on a sphere:

![tilt](https://user-images.githubusercontent.com/38077812/111377452-aa806d80-866e-11eb-91eb-8a7f103c2077.gif)


3. Construct azimuthal RHEED:

![Azimuth](https://user-images.githubusercontent.com/38077812/111377562-cbe15980-866e-11eb-8c64-5fa6137a0d96.gif)


4. Vertical scan:

![Vertical](https://user-images.githubusercontent.com/38077812/111377572-ce43b380-866e-11eb-8b8f-e6ccd2e74a68.gif)


5. 3D surface view:

![surface](https://user-images.githubusercontent.com/38077812/111377787-1236b880-866f-11eb-8e52-60f3235085df.gif)


6. Regression analysis:

![fit](https://user-images.githubusercontent.com/38077812/111377799-16fb6c80-866f-11eb-96cd-f01dff3425ab.gif)


7. Interactive data visualization:

![report](https://user-images.githubusercontent.com/38077812/111377803-18c53000-866f-11eb-94ff-4ea16daaef3e.gif)


8. Kikuchi line simulation:

![kikuchi](https://user-images.githubusercontent.com/38077812/111377813-1bc02080-866f-11eb-8043-28bc199f8cd5.gif)


9. Domain boundary statistics:

![simulation](https://user-images.githubusercontent.com/38077812/111377823-1f53a780-866f-11eb-8b26-4638de0200c0.gif)
