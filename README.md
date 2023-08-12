# CT Reconstruction

Shir Nitzan, Timor Baruch, Hadar Pur

Submitted as a project report for the AI for Healthcare course, IDC, 2023

## Overview
The radon transformation is a process that involves taking several projections of an image and creating a sinogram, which is a linear representation of the original image.

We apply the radon transformation for three different images: Shepp-Logan head phantom and geometric images (such as circle and line). For example, the sinogram presents a global view of the head phantom’s density distribution.
The sinogram helps visualise how the CT scanning process acquires information about the internal structures of the head phantom. We can see that high-density areas, such as the skull, appear as bright lines or curves, while lower-density regions are represented by darker areas. The sinogram also demonstrates how the CT system acquires information about the internal structures of the head phantom through multiple projections at various angles.

Step 1 provides an understanding of the radon transform, sinogram generation, and the link between the head phantom’s density distribution and the synthetic projections. This foundation is essential for the next steps in the assignment, where we will use filtered back projection and iterative reconstruction techniques to reconstruct the original image from the sinogram.


<p align="center"">
  <img src="https://github.com/HadarPur/RU-HC-CTReconstruction/blob/main/figs/fig1.png" alt="drawing" width="800"/>
</p>

<p align="center"">
  <img src="https://github.com/HadarPur/RU-HC-CTReconstruction/blob/main/figs/fig2.png" alt="drawing" width="800"/>
</p>

<p align="center"">
  <img src="https://github.com/HadarPur/RU-HC-CTReconstruction/blob/main/figs/fig3.png" alt="drawing" width="800"/>
</p>

## Angle Reconstruction
In the code, we define a function that takes a sinogram and a list of projection angles as input, and returns the reconstructed image using the filtered back projection algorithm. We then reconstruct images using different numbers of projection angles (18, 24, 90, 120, 180, 240, 360).
As we vary the number of projection angles in CT image reconstruction, we observe changes in the quality of the reconstructed image. Generally, increasing the number of projection angles improves the image quality - the mean square error is smaller. For example, when we use 180 projection angles, the reconstructed image is of higher quality and shows more details of the brain structures and lesions than when we use only 90 projection angles.

The number of projection angles used in CT image reconstruction has a significant impact on the resulting image quality and computational time. More projection angles generally lead to higher image quality by reducing artifacts and noise in the reconstructed image. However, this also increases the computational time required for the reconstruction process. On the other hand, using fewer projection angles can result in faster reconstruction times, but may also lead to decreased image quality due to incomplete or noisy sinograms. Therefore, the choice of the number of projection angles used in CT image reconstruction depends on the desired trade-off between image quality and computational time, and a balance must be struck to achieve accurate and efficient image reconstruction.

<p align="center"">
  <img src="https://github.com/HadarPur/RU-HC-CTReconstruction/blob/main/figs/fig4.png" alt="drawing" width="800"/>
</p>

<p align="center"">
  <img src="https://github.com/HadarPur/RU-HC-CTReconstruction/blob/main/figs/fig5.png" alt="drawing" width="800"/>
</p>

<p align="center"">
  <img src="https://github.com/HadarPur/RU-HC-CTReconstruction/blob/main/figs/fig6.png" alt="drawing" width="800"/>
</p>

## Back projection
Back projection is a simple method for reconstructing an image from the sinogram. It generates a blurred image with noticeable artifacts due to the inherent low-pass filtering that occurs during the Radon transform. This effect is more noticeable when there are fewer projection angles.

The filtered back projection (FBP) is a widely used method for performing the inverse Radon transform and reconstructing images. It is one of the fastest methods available and involves applying a filter to the fourier transformed projections. The filter serves to remove noise and other artifacts from the reconstructed image. When the back projection is performed without a filter, the resulting image is often very blurry and noisy, as can be seen in the images attached below, opposed to when using a filter. It happens because the back projection method relies on the actual fourier transformed projections which can contain noise and other artifacts that contribute to a blurry and noisy reconstructed image. The FBP incorporates a filtering step that removes unwanted components before back projecting the sinogram data. This step helps to reduce artifacts such as streaks and blurring, resulting in a more accurate and cleaner image reconstruction compared to back projection without filtering. Therefore, it is essential to apply a filter to obtain a more accurate and reliable image reconstruction.

Examples for the head phantom with and without filters on different number of angles:

<p align="center"">
  <img src="https://github.com/HadarPur/RU-HC-CTReconstruction/blob/main/figs/fig7.png" alt="drawing" width="800"/>
</p>


<p align="center"">
  <img src="https://github.com/HadarPur/RU-HC-CTReconstruction/blob/main/figs/fig8.png" alt="drawing" width="800"/>
</p>


<p align="center"">
  <img src="https://github.com/HadarPur/RU-HC-CTReconstruction/blob/main/figs/fig9.png" alt="drawing" width="800"/>
</p>


### SIRT
In order to apply an algebraic iterative reconstruction technique, we chose to use SART. SART (Simulta- neous Algebraic Reconstruction Technique) is an iterative algorithm used in computed tomography (CT) for reconstructing images from sinograms. It is a type of iterative reconstruction method that refines the reconstructed image progressively by solving a system of linear equations representing the CT image re- construction problem. It offers advantages in terms of noise reduction, edge preservation, and robustness to incomplete or noisy data. By applying SART, we can achieve high-quality image reconstructions, with improvements in image quality observed throughout the iterative process. However, the computational cost associated with iterative methods are higher, as they can be more demanding than analytical methods like filtered back projection.

Although even after the first iterations the reconstructed image looks good, we can see that as the number of iterations increases, the SART reconstruction typically becomes more accurate, with the error between the reconstructed image and the true image decreasing.

Examples for the head phantom image:

<p align="center"">
  <img src="https://github.com/HadarPur/RU-HC-CTReconstruction/blob/main/figs/fig10.png" alt="drawing" width="800"/>
</p>

