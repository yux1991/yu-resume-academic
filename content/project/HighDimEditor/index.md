This project is used for editing the images in the curvelet domain. It allows visualization of the curvelet structure and applying threshold denoise for each wedge in the curvelet domain.

## Requirements
- matplotlib 3.3.1
- numpy 1.19.2
- pillow 7.2.0
- pyct 1.0
- pyqt5 5.15.1
- pyqtchart 5.15.1
- pyqtdatavisualization 5.15.1
- rawpy 0.15.0
- scipy 1.5.2
    
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
