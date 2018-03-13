# **Finding Lane Lines on the Road**

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./dev_images/ImgOriginal.jpg "Original"
[image2]: ./dev_images/ImgGrayscale.jpg "Grayscale"
[image3]: ./dev_images/ImgBlur.jpg "Blur"
[image4]: ./dev_images/ImgCanny.jpg "Canny"
[image5]: ./dev_images/ImgMaskLeft.jpg "MaskLeft"
[image6]: ./dev_images/ImgMaskRight.jpg "MaskRight"
[image7]: ./dev_images/ImgHoughLeft.jpg "Hough Left"
[image8]: ./dev_images/ImgHoughRight.jpg "Hough Right"
[image9]: ./dev_images/ImgWeighted.jpg "Weighted"

[image10]: ./test_videos_output/solidWhiteRight.mp4 "SolidWhiteRight"
[image11]: ./test_videos_output/solidWhiteRight.mp4 "Solid Yellow Left"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

Original image shows here.

![alt text][image1]

My pipeline consisted of following steps in sequence.

#### 1. Convert the images to grayscaled image (grayscale)

![alt text][image2]

#### 2. Convert the image to blur image using gaussian blur filter (gaussian_blur)

![alt text][image3]

#### 3. Canny detection (canny)
    - LowThreshold to 20% of maximum grayscale
    - HighThreshold to 60% of maximum grayscale

![alt text][image4]

#### 4. Mask off other than 'LEFT side'of interested region (region_of_interest)

![alt text][image5]

#### 5. Hough Transform to detect only one best line (hough_lines)
    - Detect only the 1st Line among detected lines

![alt text][image7]
#### 6. Mask off other than 'RIGHT side'of interested region (region_of_interest)
![alt text][image6]

#### 7. Hough Transform to detect only one best line (hough_lines)
    - Detect only the 1st Line among detected lines

![alt text][image8]

#### 8. Display Weighted image (weighted_img)

![alt text][image9]

The 'Helper functions' are also modified for better detection.

1. region_of_interest():
    - I separated two different mask to detect the best lane for each 'Left', and 'Right' side from Hough line detections.
2. draw_lines():
    - Extrapolated detected Lines toward yMAX.
    - Reject Horizontal lines which is in (-5deg < Slop < +5deg) to eliminate other than Lane.
3. hough_lines():
    - Modified thickness to 15.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be:

1. Road is not straight, but, curved rapidly
2. Road is not straight, but, turn to right or left
3. Road has different color, due to patched repair


### 3. Suggest possible improvements to your pipeline

Possible improvements from my current pipeline are:

1. Sometimes road color change caused wrong detection from the 'Optional Challenge Example'.
2. Possibly detect given width of lane, instead of just one line detection
