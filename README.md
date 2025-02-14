# Computer-Vision-Convolution-Cross_Correlation
The main reason for this project is to have a deep understanding of how a convolution and a cross correlation works.

## Convolution:
  - Convolution is a fundamental operation in image processing and computer vision. It involves applying a mathematical operation between two functions, typically an input image and a filter or kernel. The convolution operation produces a new image, known as the output or feature map, by sliding the filter over the input image and computing the weighted sum of the overlapped pixel values.
    - <ins>**Kernel**</ins>: A small matrix of numbers defining the operation to be applied to the input image.
    - <ins>**Sliding Window Operation**</ins>: The kernel is moved over the input image, and at each position, the corresponding pixels are multiplied and summed to produce a value for the output image.
    - <ins>**Boundary Handling**</ins>: Special handling is required for convolution at image boundaries to maintain accuracy, often achieved through padding techniques like zero-padding or symmetric padding.
    - <ins>**Output Image Size**</ins>: The size of the output image depends on the size of the input image, kernel size, and padding. Typically, the output image is smaller than the input due to the convolution operation.
    ### Edge Detection

    Building a function that takes in two 2D arrays as input - a filter and an image. Convolution is performed on these image arrays to output a filtered image. Instead of using a predefined function `cv2.filter2D` or `cv2.GaussianBlur` or `cv2.medianBlur`. Padding is an intermediary step performed as and when an issue with the input image's boundary is missed from convolving. Padding is used so no image information is lost. Both Horizontal and Vertical edges can be found with a different set of kernels for each kind of edges. these kernels are called 1D Filters.

    ![Image with Individual Edges detected](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/DER_X_Y_CAMERA.png)
    > The X_derivative Image depicts the detected horizontal edges from the image.
    > The Y_derivative Image Depicts the detected vertical edges from the image.

    On one of the either images, if another edge detection is performed, we get all the possible edges of the image, in essence, performing a convolution with a vertical kernal on the `X_derivative image`, the output will be depicting all the possible edges in the image.
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Image with all edges detected](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/2D_filtered_camera.png)
    > This image contains all the possible edges from the input.
      #### Blurring

      <ins>**Blur using 1D filters**</ins>
      Consider G<sub>x</sub> and G<sub>y</sub> to be respective Gaussian 1D filters. Convolving one of these filters with the input image, the output will be a respective blur. $$X_{blur} = G_x * InputImg$$ $$Y_{blur} = G_y * InputImg$$ 
      > These operations will result in respective blurred images.
      
      ![Image with X blurs](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/Gaussian_X_filtered.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
      ![Image with Y blurs](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/Gaussian_Y_filtered.png)

      > The Gaussian Horizontal Filtered is X<sub>blur</sub>. The Gaussian Vertical Filtered is Y<sub>blur</sub>.
      
      - **Similar to finding all the edges of the image, convolving either of the blurred images with the other Gaussian 1D kernel will result in a Gaussian Blur of the whole image.**

       &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Gaussian Blurred image](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/Gaussian_filtered.png)

      - **Edge Detection of the Blurred images can be computed by using the previous horizontal and vertical kernels and convolving them with the blurred images.**
      ![Gaussian Blurred image Edges](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/Gaussian_X_Y_derivatives.png)
      > The X_deriv Gauss image is considered to be xderiv and the Y_deriv Gauss image to yderiv for computing the gradient magnitude.

      - **To compute the gradient magnitude of the image, we use the formula, $$GradMag = \sqrt{xderiv^2 + yderiv^2}$$**
      
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![gradient Magnitude image](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/Gradient_magnitude_Camera.jpg)
      >This image depicts the gradient magnitude of the input image.
      #### Thresholding
    - **Applying otsu thresholding to the input Gradient Magnitude image brings out the most significant edges automatically.**
    
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Otsu thresholded image](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/binary_edge_camera.png)
    ### Zero Crossings

    - To the above computed Gaussian blurred image, apply a 3 x 3 Laplacian filter.
    - Finally, apply a 3x3 procedure for detection of zero-crossings by adhering to the principle of "detecting pixels with positive values that possess at least one negative neighbor".
    - Once a convolution between gaussian blurred image and a laplacian filter is done, we get the result to be Laplacian of Gaussian `LoG` image.

    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![LoG image](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/LoG_Camera.png)
    > This image depicts the laplacian of Gaussian of the input image.

    **We scan every pixel in the Laplacian-filtered, Gaussian-smoothed image that has a positive value. Examine all eight of the nearby pixels for each of these types of pixels to see if any of them have negative values. If at least one of the adjacent pixels in the output image is negative, then that pixel is considered an edge. To capture only the strongest of the edges, another minor threshold is used.**

    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Otsu thresholded image](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/Edge_detection_Zero_Crossing_Camera.png)
    >Zero Crossing Edges a.k.a. Strong Edges.
    
## Correlation
- Image correlation is a technique in computer vision and image processing used to measure the similarity between two images or distinct areas within the same image. It involves comparing intensity values or patterns in corresponding pixels or regions to calculate a numerical similarity measure. This method slides one image (the template or kernel) over another (the reference or search image), calculating similarity at each position. Image correlation is widely used in applications like object detection, motion tracking, image registration, and stereo vision. It enables the identification of objects or patterns in images, tracks their movements, aligns images for further analysis, and detects changes or differences.

  - <ins>**Correlation Operation**</ins>: Correlation is another fundamental operation in image processing and computer vision. It involves measuring the similarity between two functions, typically an input image and a template or kernel. Unlike convolution, correlation does not involve flipping the kernel.
  - <ins>**Kernel or Template**</ins>: Similar to convolution, a kernel or template is used in correlation to define the operation. However, unlike convolution, the kernel is not flipped during correlation.
  - <ins>**Sliding Window Operation**</ins>: Correlation also employs a sliding window operation, where the kernel is moved over the input image. At each position, the corresponding pixels are multiplied and summed to produce a value for the output image.
  - <ins>**Boundary Handling**</ins>: As with convolution, special handling may be required for correlation at image boundaries to maintain accuracy. Various padding techniques can be employed to handle edge cases.
  - <ins>**Output Image Size**</ins>: Like convolution, the size of the output image in correlation depends on the size of the input image and the kernel. Typically, the output image has dimensions similar to the input image.

## Template Matching

- In image processing and computer vision, template matching with correlation is a technique used to identify particular items or patterns within a broader image. First, a template image that depicts the desired pattern is chosen. This template is slid across various portions of the bigger image, and a similarity measure is computed, usually using cross-correlation or normalized cross-correlation. This metric expresses how closely each overlapping area of the image matches the template. Peaks in the matching score serve as potential matches by showing where the template most closely resembles a certain area of the image. The system locates occurrences of the template inside the enlarged image by identifying these peaks, making it possible to identify specific items or patterns.

- The steps involved in Template Matching are:
    - Setting up the template image by calculating its mean, maximum, and minimum values. Next. To ensure that the final template has a mean value of 0.0, normalize the template image by deducting the mean value from each pixel value.
    - Using the zero-mean template picture as a mask, perform cross-correlation between the original and template images.
    - When some areas of the image closely match the template, this procedure produces peak values, or maxima. The modified correlation image is thresholded at 60% of 255 (150), producing peaks for every match in the set. In order to make visual inspection and verification easier, peaks are superimposed onto the original image.
 
  ### Zero Mean Template

  To obtain the zero-mean template, the template must first be normalized. We calculate the template image's mean, minimum, and maximum intensity values. Then, we subtract the template's mean value from each pixel in the template image to create the zero-mean template.

  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Zero Mean Template](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/animal-family-25-template.jpg)

  > This is the Zero Mean Template of the to-be-found texture from the input image.
### Cross - Correlation 
- Cross-correlation between the original image and the zero mean template image is the next step in the process. The image is padded in accordance with the template size to guarantee compliance. (Image height - template height) divided by (Image width - template width) yields the correlation image's size. Then, cross-correlation is run between the template and any area where the image overlaps.

<img src = "https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/animal-family-25.jpg" width = "400" height = "600"/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src = "https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/Correlation_mon.png" width = "400" height = "600"/>

 ### Thresholding and Peaks Generation
 - The process ends with the application of a threshold and the identification of peaks. As the template gets closer to a specific overlapped location, the intensity value in the cross-correlation output image rises. As a result, the image's peak values indicate the best fit for the template in the provided image. These peak values are located by scanning the correlation image, which is above the threshold of 60% of 255. To aid in visual inspection and verification, the locations found after the scan are superimposed onto the original image. Several other thresholds are experimented and documented as given below.

<img src = "https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/60threshmon.png" width = "300" height = "400"/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src = "https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/80threshmon.png" width = "300" height = "400"/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src = "https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/100threshmon.png" width = "300" height = "400"/>

>The images show the result with increasing threshold. The template is matched lesser and lesser as the threshold increases. With a 60% threshold, there are 5 matches between the template and the input image. With 80% threshold, there is only 1 match to the template and the input image. This is the correct match to the template and the input image. With a 100% threshold,m there is no match to the template and the input image.

|Threshold|Number of matches|
|  :----:  |  :----------:  |
|60%|5|
|80%|1|
|100%|0|
  
