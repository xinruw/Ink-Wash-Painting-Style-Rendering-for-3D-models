
CS535 Final Project 
 -- Chinese Ink-Wash Painting Style Rendering
=================================
Name:  Xinru Wang
Email: xinruw AT purdue.edu

# Overview
A GPU-based Chinese ink-wash painting style rendering program
for any 3D animal models.
## Keywords
Non-Photorealistic Rendering (NPR), Ink Wash Painting.

# Usage
base_glfw\base_glfw.exe
1. The left half of GUI screen displays the original 3D animal model.
2. The right half of the screen is the rendered picture.
3. Users can change to another model/background by opening a .obj/.jpg file from the menu.
4. To finely control the position of the object in the picture, users can scale the object by scrolling the mouse wheel, or rotate it by clicking the mouse button and then dragging the object, or translate it by pressing the up/down/left/right key on the keyboard.

# Methods
1. Inner shading: 
    1) Ambient light: Simply add a constant to the object color.
    2) Diffuse light: Firstly add three distinct light sources above the model. Then for each fragment, calculate the dot product of the light vector and the normal vector. A dot product close to or less than 0 indicates a darker place, while a dot product close to 1 means this region is exposed to the light.
    3) Sample color from a 1D texture according to the dot product of light vector and normal vector. Apply a Gaussian filter to smooth the texture and to imitate the ink-wash effect.
2. Contouring
    1) Silhouette detection: Calculate the dot product of view vector and the normal vector. A silhouette is where the dot product is close to 0.
    2) Set a threshold, e.g. 0.5, for the dot product. Any value below this threshold is considered a silhouette, which should be colored black. Use the square of it as the color value(0 is black and 1 is white). Any value above the threshold is mapped to 1.
    3) Contour twice for a better simulation of the brush stroke. Contour using both the original value and the mapped value of the dot product.
3. Background Blending
    Multiply the object color and the background color.
