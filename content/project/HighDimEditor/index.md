---
title: HighDimEditor
summary: Edit images in the curvelet domain
tags:
- Computer Vision
date: "2021-10-31"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: Lena in the curvelet domain
  focal_point: Smart

links:
- icon: github
  icon_pack: fab
  name: GitHub Repository
  url: https://github.com/yux1991/HighDimEditor
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

This project is used for editing the images in the curvelet domain. It allows visualization of the curvelet structure and applying threshold denoise for each wedge in the curvelet domain.
    
## Modules 
- browser: browse files inside the working directory
- canvas: display original image, processed image and their difference
- digital_tile: configure the number of scales and number of azimuth in digital tiling of the curvelet space
- dynamic_viewer: interactive visualization of the selected wedges in the curvelet domain
- main: the main module
- process: the backend processes

## Demonstrations

1. Apply threshold denoise to the image on selected regions in the curvelet domain:

![denoise](https://user-images.githubusercontent.com/38077812/111381638-f84ba480-8673-11eb-814f-55afeb1dee1f.gif)

2. View the curvelet domain structure of an image by the wedge index:

![curvelet](https://user-images.githubusercontent.com/38077812/111381706-0bf70b00-8674-11eb-966d-0dad36ff0d59.gif)
