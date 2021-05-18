# ORB (Oriented FAST and Rotated BRIEF)

This algorithm was brought up by Ethan Rublee, Vincent Rabaud, Kurt Konolige and Gary R. Bradski in their paper [*ORB: An efficient alternative to SIFT or SURF in 2011*](http://www.willowgarage.com/sites/default/files/orb_final.pdf). It is a good alternative to SIFT and SURF in computation cost, matching performance and mainly the patents.

ORB is basically a fusion of FAST keypoint detector and BRIEF descriptor with many modifications to enhance the performance.

* First it uses FAST to find keypoints,
* Then it applies Harris corner measure to find top N points among them.<p>
It also use pyramid to produce multiscale-features.


## How Fast(Features from Accelerated and Segments Test) is used in ORB:
--------------

Given a pixel p in an array fast compares the brightness of p to surrounding 16 pixels that are in a small circle around p. These pixels are then sorted into three classes (lighter than p, darker than p or similar to p). If more than 8 pixels are darker or brighter than p than it is selected as a keypoint. Keypoints found by fast gives us information of the location of determining edges in an image.

![FAST](https://miro.medium.com/max/554/0*CZ2Ub21iuBOgpMDb.jpg)

However, FAST features do not have an orientation component and multiscale features. So it uses a multiscale image pyramid to produce multiscale-features. Once orb has created a pyramid it uses the fast algorithm to detect keypoints in the image. By detecting keypoints at each level orb is effectively locating key points at a different scale. In this way, ORB is partial scale invariant.

![FAST_ORIENTATION](https://miro.medium.com/max/375/0*wGPpgnPImtwLb8NX.png)

But FAST doesn’t compute the orientation and descriptors for the features, so this is where BRIEF comes in the role.

## How Brief(Binary robust independent elementary feature) is used in ORB:
-----------------

Brief takes all keypoints found by the fast algorithm and converts it into a binary feature vector so that together they can represent an object.

It starts by smoothing image using a Gaussian kernel in order to prevent the descriptor from being sensitive to high-frequency noise.

![BRIEF](https://miro.medium.com/max/875/1*8v4ZvgwE0DYiCzQDRvno1A.png)

The matching performance of BRIEF falls off sharply for in-plane rotation of more than a few degrees. ORB proposes a method to steer BRIEF according to the orientation of the keypoints.
Using the orientation of the patch, its rotation matrix is found and rotates the BRIEF to get the rotated version.

rBRIEF shows significant improvement in the variance and correlation over steered BRIEF.

ORB specifies the rBRIEF algorithm as follows:
1) Run each test against all training patches.
2) Order the tests by their distance from a mean of 0.5, forming the vector T.
3) Greedy search

## Advantages of ORB
-------------
* ORB is an efficient alternative to SIFT or SURF algorithms used for feature extraction.
* Computing cost in case of ORB is less as compared to SIFT or SURF.
* Matching performamce of ORB is higher than other such algorithms.
* SIFT and SURF are patented and you are supposed to pay them for its use, whereas ORB is not patented.

## ORB in OpenCV
---------------
In OpenCv, we have to create an ORB object with the function, cv2.ORB() or using feature2d common interface. It has a number of optional parameters, out of which the most useful ones are nFeatures, scoretypes, etc.

* nFeatures denotes maximum number of features to be retained (by default 500)
* scoreType denotes whether Harris score or FAST score to rank the features (by default, Harris score) etc.
* WTA_K decides number of points that produce each element of the oriented BRIEF descriptor.<br>
By default it is two, ie selects two points at a time.<br>
In that case, for matching, NORM_HAMMING distance is used.<br>
If WTA_K is 3 or 4, which takes 3 or 4 points to produce BRIEF descriptor, then matching distance is defined by NORM_HAMMING2.<br>

**References:**

>[OpenCv Docs](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_feature2d/py_orb/py_orb.html)

>[Medium](https://medium.com/data-breach/introduction-to-orb-oriented-fast-and-rotated-brief-4220e8ec40cf)
