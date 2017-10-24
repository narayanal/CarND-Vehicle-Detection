
Please refer to the file TrainingData.ipynb (Python note book file)
and TrainingData.html (html copy of python notebook file)


1. Explain how (and identify where in your code) you extracted HOG features from the training images.

I started by reading in all the `vehicle` and `non-vehicle` images.  For sample output of car and noncar image. check the output of cell 3 in TrainingData.ipynb 

I have downloaded data set from links given in readme.txt file. The images are in png format.
I have converted images in jpg format and used it through out. (it is possible to use png format also)

Check the output in cell 2 for training set counts, and test accuracy details

in the cell 1, there is function defined "get_hog_features" which will extract hog features.
the values choosen for orientation, pixels_per_cell, cell_per_block are 9,8,2

2. Explain how you settled on your final choice of HOG parameters.

I tried various combinations of parameters and combination of orientation, pixels_per_cell, cell_per_block are 9,8,2 gave satisfactory results.

I have choosen color format as "YCrCb"

3. Describe how (and identify where in your code) you trained a classifier using your selected HOG features (and color features if you used them).

I trained a linear SVM using following parameters. Please cell refer to the cell 2 in python notebook

color_space = 'YCrCb' # Can be RGB, HSV, LUV, HLS, YUV, YCrCb
orient = 9  # HOG orientations
pix_per_cell = 8 # HOG pixels per cell
cell_per_block = 2 # HOG cells per block
hog_channel = 'ALL' # Can be 0, 1, 2, or "ALL"
spatial_size = (32, 32) # Spatial binning dimensions
hist_bins = 32    # Number of histogram bins
spatial_feat = True # Spatial features on or off
hist_feat = True # Histogram features on or off
hog_feat = True # HOG features on or off
y_start_stop = [400, 656]

Sliding Window Search
1. Describe how (and identify where in your code) you implemented a sliding window search.  How did you decide what scales to search and how much to overlap windows?

I started using sliding window searh with the y coordinates y_start_stop = [400, 656]
I have choosen sliding windows of 3 different sizes, 64, 96, 128 which has produced good results
Refer to the code present in function "process_image"

2. Show some examples of test images to demonstrate how your pipeline is working.  What did you do to optimize the performance of your classifier?

Ultimately I searched on two scales using YCrCb 3-channel HOG features plus spatially binned color and histograms of color in the feature vector, which provided a nice result.
I started using sliding window searh with the y coordinates y_start_stop = [400, 656]
I have choosen sliding windows of 3 different sizes, 64, 96, 128 which has produced good results
Refer to the code present in function "process_image"

1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (somewhat wobbly or unstable bounding boxes are ok as long as you are identifying the vehicles most of the time with minimal false positives.)
Here's a [link to my video result](./white.mp4)

2. Describe how (and identify where in your code) you implemented some kind of filter for false positives and some method for combining overlapping bounding boxes.

I recorded the positions of positive detections in each frame of the video.  From the positive detections I created a heatmap and then thresholded that map to identify vehicle positions.  I then used `scipy.ndimage.measurements.label()` to identify individual blobs in the heatmap.  I then assumed each blob corresponded to a vehicle.  I constructed bounding boxes to cover the area of each blob detected.  

Refer to the output of process_image function. you can see the vehicles are identified for all test images

Discussion

1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

Currently, generation of video is taking more than 30 minutes, since we have used three different windows of size 64, 96, 128.
I have to use the methods described in the lecture "Hog sub-sampling" and reduce the processing time
