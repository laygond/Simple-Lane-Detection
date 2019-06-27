# Finding Lane Lines on the Road
Very simple pipeline to detect the line segments in an image, then average/extrapolate them and draw them onto the image for display. The project makes use of Canny edge detection, Hough Transform, and RANSAC to find for each lane line a second order polynomio fit. This repo uses [Udacity's CarND-LaneLines-P1 repo](https://github.com/udacity/CarND-LaneLines-P1) as a base template and guide. 

![alt text](README_images/simple_lane_detection.gif)


## Directory Structure
```
.Simple-Lane-Detection
├── demo.ipynb                   # Main file
├── .gitignore                   # git file to prevent unnecessary files from being uploaded
├── README_images                # Images used by README.md
│   └── ...
├── README.md
└── Udacity_dataset
    ├── examples                 # images used by demo.ipynb and a pair of ground truth videos
    │   └── ...
    ├── test_images              # input images
    │   └── ...
    ├── test_images_output       # output directory generated automatically once you run demo.ipynb
    │   └── ...
    ├── test_videos              # input videos
    │   └── ...
    └── test_videos_output       # output directory generated automatically once you run demo.ipynb
        └── ...
```

## Demo File

#### Dataset
The demo file makes use of Udacity's dataset to show results. However, once you have run and understood the `demo.ipynb`, feel free to try your own dataset by changing the input directory from the 'Read in Test Image' and 'Read in Test Video' sections from the demo file. The results of your own dataset will be displayed in an utput directory generated automatically by `demo.ipynb` at the same directory level as your input directory.

#### Helper Functions
- `region_of_interest` keeps the region of the image defined by the user while the rest of the image is set to black.
- `ransac_polyfit` finds the best 2nd order model coefficients by randomly testing subsets of a lane's line 
- `line_slope_classifier` classifies pairs of pixel coordinates as left or right lane line based on the pair's line slope. It also allows the user to increase the density of points belonging to left or right lane line.
- `draw_lines` makes use of `region_of_interest`, `ransac_polyfit`, and `line_slope_classifier` to draw the left and right lines of the vehicle's current lane with a user defined color and thickness.
- `draw_roi_box` this is a visual helper. It draws a contour of color around the region of interest to visually identify it. 
- `draw_hough_lines` this is a visual helper. It draws all hough lines with random colors to visually identify them.

#### Pipeline 
This is the process through which each image or video frame goes through.


![alt text original image](README_images/before.png)

![alt text](README_images/pipeline.png)

![alt text](README_images/after.png)



## Drawbacks and improvements

From the challenge video one can identify that the techniques implemented are good for determining lines on on the road but has issues extrapolating those lines. `line_slope_classifier` function needs improvement since it fails when the lane has steep curves. Also the second order polinomial line models for each line should share the same `a` coefficient in `ay^2+by+c` since both lines curve in the same direction. We will deal with this issues in our next repo.
