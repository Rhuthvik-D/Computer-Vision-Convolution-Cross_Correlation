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
    ![Image with all edges detected](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/2D_filtered_camera.png)
    > This image contains all the possible edges from the input.
      #### Blurring

      <ins>**Blur using 1D filters**</ins>
      Consider G<sub>x</sub> and G<sub>y</sub> to be respective Gaussian 1D filters. Convolving one of these filters with the input image, the output will be a respective blur. $$X_{blur} = G_x * InputImg$$ $$Y_{blur} = G_y * InputImg$$ 
      > These operations will result in respective blurred images.
      
      ![Image with X blurs](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/Gaussian_X_filtered.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
      ![Image with Y blurs](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/Gaussian_Y_filtered.png)

      > The Gaussian Horizontal Filtered is X<sub>blur</sub>. The Gaussian Vertical Filtered is Y<sub>blur</sub>.
      
      - **Similar to finding all the edges of the image, convolving either of the blurred images with the other Gaussian 1D kernel will result in a Gaussian Blur of the whole image.**

       ![Gaussian Blurred image](https://github.com/Rhuthvik-D/Computer-Vision-Convolution-Cross_Correlation/blob/main/Resulting%20photos/Gaussian_X_Y_Full_filtered.png)
      
