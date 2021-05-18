# Harris Corner Detection

Harris Corner Detector is a corner detection operator that is commonly used in computer vision algorithms to extract corners and infer features of an image.

## Harris Corner Detector function
```
cv2.cornerHarris(img, blockSize, ksize, k)
```
The arguments here mean:
1) img - Input image, it should be grayscale and float32 type.
2) blockSize - It is the size of neighbourhood considered for corner detection
3) ksize - Aperture parameter of Sobel derivative used.
4) k - Harris detector free parameter in the equation.

## Advantages
1) It is simple to compute, and is fast enough. 
2) Also, it is popular because it is rotation, scale and illumination variation independent.

## Results
![alt text](https://github.com/aswarth123/Image-Processing-OpenCV/blob/master/HarrisCornerDetection/images/input.jpg) <br> Input image <br><br><br>
![alt text](https://github.com/aswarth123/Image-Processing-OpenCV/blob/master/HarrisCornerDetection/images/output.jpg) <br> Output image

## Links for more information
You can go through this [link](https://aishack.in/tutorials/harris-corner-detector/) for understanding the mathematics behind it.
