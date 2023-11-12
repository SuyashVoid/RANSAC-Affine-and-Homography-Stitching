# Image Stitching

## Introduction

This project is to stitch two or more images together using SIFT, RANSAC and custom image stitching code.

## Usage

Head to the 3rd last cell for (Affine-stitch) or last/2nd-last cell (for Homography) of the notebook and change the image paths to the images you want to stitch together. Then run all the cells.

## Results - Affine Stitching

|                      Left                       |                       Right                       |
| :---------------------------------------------: | :-----------------------------------------------: |
| ![Left-Img](/Media/q1/smol/parliament-left.jpg) | ![Right-Img](/Media/q1/smol/parliament-right.jpg) |

| Stitched |
| :--------------------:|
|![Stitched](/Results/q1AffineStitch.jpg)|

## Results - Homography Stitching 1

|                Left                |                 Mid                  |                Right                |
| :--------------------------------: | :----------------------------------: | :---------------------------------: |
| ![Left-Img](/Media/q2/smol/lt.jpg) | ![Right-Img](/Media/q2/smol/mid.jpg) | ![Right-Img](/Media/q2/smol/rt.jpg) |

| Stitched |
| :--------------------:|
|![Stitched](/Results/q2.png)|

## Results - Homography Stitching 2

|                 Left                 |                  Mid                   |                 Right                 |
| :----------------------------------: | :------------------------------------: | :-----------------------------------: |
| ![Left-Img](/Media/q2_3/smol/lt.jpg) | ![Right-Img](/Media/q2_3/smol/mid.jpg) | ![Right-Img](/Media/q2_3/smol/rt.jpg) |

| Stitched |
| :--------------------:|
|![Stitched](/Results/q2_3.png)|

## Analysis and Discussion

- Combining image into a panaroma is harder than it seems. Some transforms can cause the image to be mapped in negative coordinates, which is a problem. So the transform matrix has to be modified by the minimum x and y coordinates of the image to make sure the image is mapped in positive coordinates.
  - Then, the other image to be stitched has to be shifted by the same amount to make sure the images are stitched properly.
  - This is done in the `stitchImages` function in the notebook.
- I used an eroded mask instead of max to blend the images and avoid the black aliased line. This ensures we don't introduce artifacts that come along with max blending and imperfect homography warping (when overlayed).
- For pruning the keypoints, I picked the top x keypoints with the highest response.
- Trimming the final image after stitching is important to remove the black borders that come along with the stitching process as I started with a canvas larger than necessary to avoid cropping out any part of the image (and running into shape related bugs since it's hard to fiigure the output dimensions exactly).
