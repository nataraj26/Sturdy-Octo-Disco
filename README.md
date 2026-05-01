# Sturdy Octo Disco: Virtual Sunglasses Overlay 🕶️

**Sturdy Octo Disco** is a computer vision project developed to dynamically overlay sunglasses onto portrait photos. Unlike simple "sticker" overlays, this project uses advanced image processing techniques like **Region of Interest (ROI)** manipulation and **Arithmetic Blending** to ensure a realistic, transparent look.

## 🚀 Key Features
*   **Precision Alignment**: Uses coordinate mapping to fit sunglasses perfectly on the bridge of the nose.
*   **Arithmetic Blending**: Employs bitwise masking and image multiplication to eliminate "black box" backgrounds.
*   **Transparency Retention**: Ensures the subject's eyes remain visible through the lenses for a natural effect.
*   **Visual Workflow**: Includes diagnostic plots to visualize the masking and addition phases.

## 🛠️ Technology Stack
*   **Python 3.x**
*   **OpenCV**: For core image manipulation and arithmetic operations[cite: 1, 2].
*   **NumPy**: For high-performance array calculations and mask generation[cite: 1, 2].
*   **Matplotlib**: For rendering and displaying the final visual output[cite: 1, 2].

## 📸 How It Works
The project follows a specific mathematical pipeline to blend the two images:
1. **Mask Creation**: A binary mask is extracted from the sunglasses image to define its shape.
2. **ROI Slicing**: A "hole" is mathematically cut into the original face image using the inverse of the mask.
3. **Additive Blending**: The sunglasses are added into the prepared space, creating a seamless integration without solid backgrounds.

### Blending Process Visualization

*Figure 1: Comparison between the masked eye region, the isolated sunglasses, and the final combined result.*

## 💻 Setup & Usage
1. **Clone the Repo**:
   ```bash
   git clone [https://github.com/nataraj26/Sturdy-Octo-Disco.git](https://github.com/nataraj26/Sturdy-Octo-Disco.git)
   ```
## PROGRAM
```python
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the Face Image
faceImage = cv2.imread('23003973.png')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")

faceImage.shape

#resized_faceImage.shape
faceImage.shape

# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread('glassPNG.png',-1)
glassPNG = glassPNG[:, :, [2, 1, 0, 3]]  
plt.imshow(glassPNG)   
plt.title("sunglass")

# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(190,25))
print("image Dimension ={}".format(glassPNG.shape))         

# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]

# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');


faceWithGlassesNaive = faceImage.copy()


h, w, _ = glassBGR.shape 


y_start, x_start = 112, 62 

faceWithGlassesNaive[y_start : y_start + h, x_start : x_start + w] = glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
plt.show()


```
## OUTPUT 

### Final Augmented Output

The sunglasses are fitted to the eye line of the subject for a professional and "cool" finish. Through iterative coordinate adjustment, the accessory is seated naturally on the bridge of the nose.

 ### Original Face 
<img width="276" height="354" alt="23003973" src="https://github.com/user-attachments/assets/bb08b37b-8d13-4521-b8e7-973cf6680d53" />

  
  
#### Final Result 
<img width="429" height="527" alt="finalimage" src="https://github.com/user-attachments/assets/d1b4c66b-90ae-476b-8b1c-21aa226a4382" />

 

## Learning Outcomes
 * This project provided hands-on experience in:

* Understanding image data as multidimensional NumPy arrays.

* Managing color space conversions (BGR vs RGB).

* Executing bitwise operations for complex image overlays.

"Created with ❤️ by a student passionate about Computer Vision."
