# Workshop--1-Adding-Sunglasses-to-Your-Passport-Photo-Using-OpenCV

# **Name:** KAMLESH P

# **Register Number:** 212225240067  

## Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

### Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.
### Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations
### How to Use:
- Clone this repository.
- Add your passport-sized photo to the images folder.
- Run the script to see your "cool" transformation!
### Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows


```
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
```
# Load the Face Image
faceImage = cv2.imread('6.JPEG')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
```
faceImage.shape
```
```
#resized_faceImage.shape
faceImage.shape
```
```
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread('sunglasses.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
```
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(500, 186))
print("image Dimension ={}".format(glassPNG.shape))
```

```
# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```
```
# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
```
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[350:536,315:815]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```

```
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[350:536,315:815]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```

```
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[350:536,315:815]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```


### OUTPUT:

#### Original Face Image

<img width="398" height="523" alt="Screenshot 2026-11-06 225727" src="https://github.com/user-attachments/assets/6431b6d7-9dd8-4896-aead-66bec8073a04" />


#### Sunglass Image

<img width="656" height="355" alt="Screenshot 2026-11-06 225811" src="https://github.com/user-attachments/assets/61677fc3-3237-431b-85cf-e127fe0e9a40" />


#### Sunglass with colour channel and with alpha channel

<img width="1228" height="274" alt="Screenshot 2026-11-06 225846" src="https://github.com/user-attachments/assets/e78f5e7b-6ec7-4569-a784-523b965b5500" />


#### Image with Sunglass

<img width="626" height="482" alt="Screenshot 2026-11-06 225909" src="https://github.com/user-attachments/assets/0f44db95-eb3f-49cf-b5ab-43e864e06013" />



#### Augumented Eye and Sunglasses 

<img width="1234" height="225" alt="Screenshot 2026-11-06 225930" src="https://github.com/user-attachments/assets/3efb1a6c-8fdc-47d6-afe0-51f5159ec15b" />


#### Image with and without sunglasses

<img width="1244" height="767" alt="Screenshot 2026-11-06 225951" src="https://github.com/user-attachments/assets/0ca6f9bd-6974-4306-8656-46b871da8da9" />


### RESULT:
Thus, the Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing has been done and verified successfully.
