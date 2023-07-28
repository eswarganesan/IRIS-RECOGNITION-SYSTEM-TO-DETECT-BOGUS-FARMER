# IRIS-RECOGNITION-SYSTEM-TO-DETECT-BOGUS-FARMER

Today, in the field of agriculture, still the old-fashioned ways of identifying farmers with their names or IDs are being used, due to which there have been a lot of bogus farmers who took advantage of this, in the context of government schemes, funds etc. Since, farmers have a great deal of physical activity and often get injured; fingerprint recognition isn’t the most efficient biometric authentication. To solve this and detect the bogus farmers, we, in our project are coming up with an Iris Recognition system to uniquely identify the farmers. Iris recognition is a popular research field in the biometrics, and it plays an important role in automatic recognition. Given sufficient training data, some approaches have achieved good performance on iris recognition. However, when the training data are limited, overfitting may occur. Iris scanning is the process of using visible and near-infrared light to take a high contrast photograph of a person's iris. For this, the farmers will have to take their iris scan with proper details provided. Thus, having data to detect the bogus farmers from genuine farmers. This way the field of biometrics can majorly benefit the agriculture sector.


STEP:0 –
SELECTING CAPTURED IMAGE AND IMAGE FOR COMPARISON
DESCRIPTION:
Step:0 image acquisition process
In this step, Image captured and image for comparison are selected from the database (MATLAB DRIVE)

STEP:1 – IMAGE ACQUISITION PROCESS
DESCRIPTION:
Step:1 (PRE-PROCESSING)
Output of the raw image is shown for initial identification

STEP:2 – GRAYSCALE CONVERSION
DESCRIPTION:
Raw image is converted into Grayscale image for minimising the computational requirements, time and t increase accuracy of the image components. Also, grayscale conversion is the basic necessary for image pre processing and convert image for pixel friendly.

STEP:3 – SUBTRACTION OF GRAYSCALE IMAGE
DESCRIPTION:
In case, if the image has to much brightness and more contrast after converting it into grayscale image, it is subtracted to much lower brightness for convenience.

STEP:4 – HISTOGRAM OF IMAGES
DESCRIPTION:
Initial histogram of the two images are generated and compared which represents the initial pixel statistics for comparison. Image is first converted to a 8-bit for the pixels representation.

STEP:5 – CROPPED IMAGE DESCRIPTION:
Images are cropped to eliminate unwanted details shown in the image. Cropping the image requires to note down the co-ordinates from both ends which covers the iris and pupil area.

STEP:6 – RESIZED IMAGE
DESCRIPTION:
Images are resized since cropping changes the whole resolution of the image. Images are resized to 256x256 resolution so that they can be represented as unsigned 8-bit image.

STEP:7 – SMOOTHENING OF IMAGE USING GAUSSIANFILTER
DESCRIPTION:
The re-sized images are smoothened using a Gaussian filter since smoothening helps in better composition and clarity of the image and removes unwanted detail.
IMAGE SEGMENTATION:

STEP:8 – CANNY EDGE DETECTION
DESCRIPTION:
Caany Filter Edge Detection remains the best edge detection method out of all others. Images are being used with canny edge detection to detect the edges of the iris and pupil perimeter. Intensities can be raised according to our requirement. Also, edge detection in this automatically uses hysteresis thresholding to get the most out of the details and bring out the clearer edge.

STEP:9 – GAMMA CORRECTION (optional)
DESCRIPTION:
Gamma Correction used to correct the canny edge detected image to adjust the contrast and clarity of the image. It is optional and is upto the user’s requirement for effective segmentation

STEP:10 – EDGE DETECTION USING SOBEL FILTER (optional)
DESCRIPTION:
Using Sobel filter which is another edge detection method to identify the edges. It is more intense than canny edge detection and could find more edges present in the eye image.
Now that the edges are well detected, hence, the images are suitable and eligible for segmenation process. Segmentation involves extracting the area between the borders of iris and pupil of the eye image.

STEP:11 -HOUGH’S TRANSFORM TO DRAW IRIS AND PUPIL PERIMETER
DESCRIPTION:
Hough’s Transform is used to detect the circular edges present as the shape of iris and pupil. Noting down the coordinates of the centre position of the iris and pupil is necessary to find out the radius of them required for Hough’s Transform to detect the circles. Hough’s Transform remains an excellent method for segmenting the iris and pupil region separately.
Requirement: coordinate of the centres, diameter/radius of iris and pupil to draw an arc throughout and draw the lines of circle covering the iris and pupil perimeter.
The main advantage of the Hough transform technique is that it is tolerant to gaps in feature boundary descriptions and is relatively unaffected by image noise and localise irises very effectively.
The Hough transform method requires the threshold values to be chosen for edge detection, and this may result in critical edge points being removed, thus resulting in failures to detect circles/arcs.

STEP:12 – STRETCHING NORMALISED IMAGES (AREA COVERED BY THE PERIMETER)
DESCRIPTION:
Normalisation of the images are carried out after Hough’s Transform. Normalization produces a 2D array with horizontal dimensions of angular resolution and vertical dimensions of radial resolution. The area covered by the concentric circle drawn using hough’s transform depicts the iris region which is required excluding the pupil region. The iris region of both the images are extracted from the whole eye image and normalised so they are represented flatly. Daugman’s Rubber sheet normalisation method is used here for normalising the images. The images are mapped to same size of rectangular region. “Rubber Sheet” is produced linearly stretching and compressing the iris region to a standard size frame for both images for feature extraction and matching.
Required Input Parameters: Cordinates of the centers of pupil and iris, Radii of Iris, Radii of pupil
Images are required to be saved in the MATLAB DRIVE for selecting them for comparison and Matching in the next step as for Hamming Distance Calculation.

STEP:13-ENHANCEMENT OF NORMALISED IRIS IMAGES
DESCRIPTION:
Normalised images are selected from the MATLAB DRIVE which had been saved in the drive in the previous step. Enhancement of the Normalised Iris images takes place here using Histogram Equalisation for better quality and enhancement of the image. Enhancement is also needed for Feature extraction and encoding of the normalised iris image for comparison.

STEP:14 AND 15-EXTRACTION AND MATCHING USING HAMMING DISTANCE:
DESCRIPTION:
The enhanced normalised images are allowed for feature extraction using Gabor wavelet Filter which takes the wavelength as pixels. So, giving the pixels as 256x256 which will create the magnitude and phase of the texture filter with required orientation. Default orientation is given as 0◦. Now the features are extracted using Gabor Filter, the iris images need to get encoded to binary number 8 bits for measuring the hamming distance.
STEP:15(B) ( TO SHOW SAME IRIS RESULT, USING IDENTICAL IMAGES)
DESCRIPTION:
The feature extracted enhanced normalised images are encoded using a MATLAB function(dec2bin) which converts decimal matrix to Binary numbers with required 8 bits. Now, the images are converted to binary 8 bit numbers, they are ready for comparison and matching using Hamming distance.

HAMMING DISTANCE:
The Hamming Distance was chosen as a matching metric, which gave a measure of how many bits disagreed between the two images. When the hamming distance of two images is calculated, one template is shifted left and right bitwise and a number of hamming distance values are calculated from successive shifts, in order to account for rotational inconsistencies. False Acceptance rate is calculated through this process. Generally, Daugman’s Threshold goes with 0.5. Here, it is minimised to 0.3 after experimenting with different images.
Algorithm for hamming distance is given in the code below.
0 <= HD <= 0.3 = SAME IRIS
0.3 < HD <= 0.4 = UNCERTAIN, use different iris images or please run the whole test again
HD > 0.4 = DIFFERENT IRIS
