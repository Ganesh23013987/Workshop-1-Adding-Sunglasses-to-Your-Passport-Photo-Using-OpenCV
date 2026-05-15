# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look
Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
Detects the face in an image.
Places a stylish sunglass overlay perfectly on the face.
Works seamlessly with individual passport-size photos.
Customizable for different sunglasses styles or photo types.
## Technologies Used:
Python
OpenCV for image processing
Numpy for array manipulations
## How to Use:
Clone this repository.
Add your passport-sized photo to the images folder.
Run the script to see your "cool" transformation!
## Applications:
Learning basic image processing techniques.
Adding flair to your photos for fun.
Practicing computer vision workflows.

## Program:
### NAME: GANESH D
### REG.NO: 21222324035

```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

```
# Load the Face Image
faceImage = cv2.imread('Ganesh D.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
<img width="550" height="550" alt="image" src="https://github.com/user-attachments/assets/f47b43c1-6a63-4516-a0c9-166e271ed980" />
```
faceImage.shape
```
<img width="318" height="55" alt="image" src="https://github.com/user-attachments/assets/576d1342-296b-4ee6-bc13-1674244ee5c4" />

```
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread('sunglass.jpg',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
<img width="1268" height="512" alt="image" src="https://github.com/user-attachments/assets/dd048097-599b-42c4-b8df-512fa0e5f52d" />
```
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(1000,400))
print("image Dimension ={}".format(glassPNG.shape))
```
<img width="563" height="61" alt="image" src="https://github.com/user-attachments/assets/ad4796ae-4832-4911-81d2-c25f831c6727" />

```
# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]

# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
<img width="550" height="550" alt="image" src="https://github.com/user-attachments/assets/dbd43f6f-283b-49dd-ba00-a4def12822e4" />

```
# Make a copy
faceWithGlassesNaive = faceImage.copy()

# Resize sunglass image properly
glassBGR = cv2.resize(glassBGR,(230,75))

# Fix sunglasses exactly on eye region
faceWithGlassesNaive[190:265,165:395] = glassBGR

# Display output
plt.figure(figsize=(8,8))
plt.imshow(faceWithGlassesNaive[:,:,::-1])

plt.show()
```
<img width="618" height="724" alt="image" src="https://github.com/user-attachments/assets/025b34d5-e9d0-462d-9c80-005bac7d32c5" />

```
# Resize sunglass and mask
glassBGR = cv2.resize(glassBGR,(230,75))
glassMask1 = cv2.resize(glassMask1,(230,75))

# Create 3-channel mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))
glassMask = glassMask.astype(np.float32)/255.0

# Convert sunglass to float
glassBGR = glassBGR.astype(np.float32)

# Make copy
faceWithGlassesArithmetic = faceImage.copy()

# Correct coordinates for your image
y1,y2 = 190,265
x1,x2 = 165,395

# Extract eye ROI
eyeROI = faceWithGlassesArithmetic[y1:y2,x1:x2].astype(np.float32)

# Blend sunglass with face
maskedEye = eyeROI * (1-glassMask)
maskedGlass = glassBGR * glassMask
eyeRoiFinal = maskedEye + maskedGlass

# Put final image back
faceWithGlassesArithmetic[y1:y2,x1:x2] = eyeRoiFinal.astype(np.uint8)

# Show outputs
plt.figure(figsize=[20,20])

plt.subplot(131)
plt.imshow(maskedEye[...,::-1].astype(np.uint8))
plt.title("Masked Eye Region")

plt.subplot(132)
plt.imshow(maskedGlass[...,::-1].astype(np.uint8))
plt.title("Masked Sunglass Region")

plt.subplot(133)
plt.imshow(faceWithGlassesArithmetic[:,:,::-1])
plt.title("Augmented Eye and Sunglass")

plt.show()
```
<img width="1075" height="425" alt="image" src="https://github.com/user-attachments/assets/07cf3d78-12da-4749-ab34-0704c7fe8cad" />

```
original = faceImage.copy()

glassBGR=cv2.resize(glassBGR,(230,75)); mask=cv2.merge((cv2.resize(glassMask1,(230,75)),)*3)/255.0
roi=faceImage[190:265,165:395].astype(np.float32)
faceImage[190:265,165:395]=(roi*(1-mask)+glassBGR.astype(np.float32)*mask).astype(np.uint8)

plt.figure(figsize=(10,10))
plt.subplot(121); plt.imshow(original[:,:,::-1]); plt.title("Original Image")
plt.subplot(122); plt.imshow(faceImage[:,:,::-1]); plt.title("With Sunglasses")
plt.show()
```
<img width="944" height="548" alt="image" src="https://github.com/user-attachments/assets/ea137e95-7f8d-4ca6-a704-9a89bff4a472" />


## RESULT:
Thus, the Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing was successfully executed.
