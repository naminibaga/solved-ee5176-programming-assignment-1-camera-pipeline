Download Link: https://assignmentchef.com/product/solved-ee5176-programming-assignment-1-camera-pipeline
<br>



<h1>1         Demosaicing</h1>

Demosaicing is a process of interpolating the red, green and blue channels from the raw pixel image. Here we will try to fill in the missing pixel values from the sampled raw images through interpolation. Kindly zoom in and view RawImage1.mat to get an idea on how raw image looks like.

The CFA for ‘RawImage1.mat’ is ‘RGGB’ whose mask is provided in the file ‘bayer1.mat’. In ‘bayer1.mat’ a value of 1 at a particular pixel means that only ‘red’ value is sampled at that pixel. Similarly values of ‘2’ and ‘3’ mean that only ‘green’ and ‘blue’ values are sampled at those pixels. The task here is to reconstruct the full colour image from the undersampled raw sensor data. Two popular ways of filling in missing data on a 2D grid are <em>bilinear </em>and <em>bicubic </em>interpolation. Here, we will try both the methods and compare the results.

Note that you have to interpolate only the missing values in the grid of pixels. For instance, at a pixel where the channel ‘blue’ is already sampled you need to interpolate only the ‘red’ and ‘green’ values from the image grid. Use Matlab built-in function griddata to query all missing pixel values at once, instead of querying it patchwise.

<ol>

 <li>a) Perform bilinear interpolation of the missing pixels in each color channel R, G and B to reconstruct a full color image from RawImage1 with the CFA provided in ‘b1.mat’ [5 marks] b) Perform bicubic interpolation of the missing pixels in each color channel R, G and B to reconstruct a full color image from RawImage1 with the CFA provided in ‘b1.mat’. Compare the reconstructed full colour image with that obtained using bilinear interpolation. [3 marks]</li>

 <li>Do demosaicing for RawImage1.mat using pattern ‘rggb’ with matlab built-in function ‘demosaic’ and compare with previous two reconstructed images [2 marks]</li>

 <li>What assumptions are you making while interpolating the missing pixel values and what will happen when the assumptions do not hold? [2 marks]</li>

 <li>Now demosaic the image ‘kodim19.mat’ which has been sampled with the CFA pattern ‘RGGB’ (provided in kodim cfa.mat). For reference the true colour image ‘kodim19.png’ is given in the data folder. Compare the demosaiced image with the actual image and comment your observations. (The image ‘kodim19.png’ is obtained from <a href="http://r0k.us/graphics/kodak/">Kodak dataset)</a> [3 marks]</li>

</ol>

<h1>2         White Balancing and Tone Mapping</h1>

Next process in the pipeline is white balancing. Here you will do white-balancing for all three raw images RawImage1, RawImage2 and RawImage3 in each subsection. Note that you have to perform demosaicing for RawImage2 and RawImage3 before white-balancing. The CFA for RawImage2 is ‘grbg’ (bayer2.mat) and for RawImage3 it is ‘rggb’(bayer3.mat). Use the code from the previous problem to demosaic the images RawImage2 and RawImage3.

There are basically three ways to do White-balancing –

<ol>

 <li>Assume the average color of the scene to be gray and then do white balancing. [2 marks]</li>

 <li>Assume that the brightest pixel to be specular highlight and should therefore be white. Use pixel coordinate (x, y) =

  <ol start="2">

   <li>(830, 814) for RawImage1 [1 mark] ii) (1165, 280) for RawImage2. [1 mark] iii) (175, 675) for RawImage3. [1 mark]</li>

  </ol></li>

 <li>Assume that some part of the scene to be neutral. Use pixel coordinate (x, y) =

  <ol start="2">

   <li>(2000, 435) for RawImage1 [1 mark] ii) (445, 715) for RawImage2. [1 mark] iii) (1550, 565) for RawImage3. [1 mark]</li>

  </ol></li>

 <li>Perform tone mapping on each of the above images using the following two methods:

  <ol>

   <li>Histogram equalization [2 marks] ii) Gamma correction for the gamma values of 0.5, 0.7 and 0.9 [3 marks]</li>

  </ol></li>

</ol>

<h1>3         Image denoising</h1>

Here in this part you will use bilateral filtering operation for denoising. The bilateral filter is controlled by two parameters <em>σ<sub>s </sub></em>and <em>σ<sub>r</sub></em>. As we know, <em>σ<sub>s </sub></em>controls the spatial weighing whereas the <em>σ<sub>r </sub></em>controls the alignment of image intensities. Ideally we would like to locally estimate the noise and adjust both the parameters accordingly but given the cost here we would go with single set of parameters. To estimate the noise we will choose a constant region in the image (coordinates are given below) and calculate the standard deviation along all the three channels R, G and B. Now denoise individual channels with window size as 11, <em>σ<sub>s </sub></em>as 2.5 and for <em>σ<sub>r </sub></em>=1<em>.</em>95×<em>σ<sub>n</sub></em>, where <em>σ<sub>n </sub></em>is noise standard deviation in the corresponding colour channel. For the bilateral filtering, use the supplied function bfilter2.m.

For RawImage2 use the rectangular region with coordinates: top-left (705,924) and bottomright (765,984) in (row,column) order. For other raw images choose a region on your own and do the denoising as mentioned above. [5 marks]

3.1      Questions:

<ol>

 <li>You have to construct a Gaussian blurring kernel with a variance <em>σ </em>for denoising an image. As you know, Gaussian function has infinite support. In order to implement tractably, you need to truncate the Gaussian function to a finite size. For a given Gaussian kernel with variance <em>σ</em>, at what point will you choose to truncate the function and why? [2 marks]</li>

 <li>For a given <em>σ<sub>n </sub></em>how would you choose the value for <em>σ<sub>r</sub></em>? What would happen if <em>σ<sub>r </sub></em>≤ <em>σ<sub>n </sub></em>or <em>σ<sub>r </sub>&gt;&gt; σ<sub>n</sub></em>? [3 marks]</li>

</ol>