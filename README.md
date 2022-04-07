# frequency-domain-filtering using FOURIER transform
The Fourier Transform is an important image processing tool which is used to decompose an image into its sine and cosine components. The output of the transformation represents the image in the Fourier or frequency domain, while the input image is the spatial domain equivalent. In the Fourier domain image, each point represents a particular frequency contained in the spatial domain image.
The DFT (Discrete Fourier Transform) is the sampled Fourier Transform and therefore does not contain all frequencies forming an image, but only a set of samples which is large enough to fully describe the spatial domain image. The number of frequencies corresponds to the number of pixels in the spatial domain image, i.e., the image in the spatial and Fourier domain are of the same size.
For a square image of size N×N, the two-dimensional DFT is given by:
![image](https://user-images.githubusercontent.com/84698110/162195003-a648d7f9-245c-4a8e-99c3-d76e9013d618.png)
where f(a,b) is the image in the spatial domain and the exponential term is the basis function corresponding to each point F(k,l) in the Fourier space. The equation can be interpreted as: the value of each point F(k,l) is obtained by multiplying the spatial image with the corresponding base function and summing the result.
The basis functions are sine and cosine waves with increasing frequencies, i.e. F(0,0) represents the DC-component of the image which corresponds to the average brightness and F(N-1,N-1) represents the highest frequency.
In a similar way, the Fourier image can be re-transformed to the spatial domain.  The inverse Fourier transform is given by:
![image](https://user-images.githubusercontent.com/84698110/162195064-aafd3d24-3696-4b17-825e-baad0f1685b4.png)
![image](https://user-images.githubusercontent.com/84698110/162195085-9b7ad13d-aa51-4124-9b6d-2cae619faeba.png)
Using these two formulas, the spatial domain image is first transformed into an intermediate image using N one-dimensional Fourier Transforms. This intermediate image is then transformed into the final image, again using N one-dimensional Fourier Transforms. Expressing the two-dimensional Fourier Transform in terms of a series of 2N one-dimensional transforms decreases the number of required computations.
 Even with these computational savings, the ordinary one-dimensional DFT has N^2 complexity. This can be reduced to N\log_2{N} if we employ the Fast Fourier Transform (FFT) to compute the one-dimensional DFTs. This is a significant improvement, in particular for large images. There are various forms of the FFT and most of them restrict the size of the input image that may be transformed, often to N=2^n where n is an integer.


There are two type of Fourier filtering 
•	Low pass filter: only low frequency (gentle amplitude) is retained, which will blur the image.
•	High pass filter: only high frequency is reserved (the amplitude is intense), which will enhance the image details.
OpenCV mainly includes cv2.dft() and cv2.idft() functions. For FFT (fast Fourier transform) in OpenCV, the input image needs to be converted to float32 and the output will be complex output, which means we need to extract the magnitude out of this Complex number.
Rearranges a Fourier transform X by shifting the zero-frequency
The magnitude of the function is 20.log(abs(f)), For values that are 0 we may end up with indeterminate values for log. So, we can add 1 to the array to avoid seeing a warning. dft_shift[:, :,0] will be a real part dft[:, :, 1] will be an imaginary part.
In this magnitude spectrum, we want to apply or block off all the central regions or central pixels. Circular HPF (High Pass Filter) mask, the centre circle is 0, remaining all ones only high frequencies are allowed. Otherwise apply a Circular LFP (Low Pass Filter) mask, the centre circle is 1 remaining all zeros, only allows low frequency components.
Apply mask and inverse DFT - Multiply Fourier transformed image (values)with the mask values.
Now we have an origin at the centre of the image, so we need to move the origin back to the top left of the image. This is the undo process of f_ishift= np.fft.fftshift(fshift)ft this shifting process already did.Inverse DFT to convert back to image domain from the frequency domain will be complex numbers. Thus find the magnitude spectrum of the image domain and plot the final results
