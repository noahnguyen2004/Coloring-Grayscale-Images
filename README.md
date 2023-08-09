# Coloring-Grayscale-Images

(insert image here)

Nowadays, there has been a lot of different tools and applications that edit your pictures seamlessly. You can use those to make funny photoshops, amazing AI generated photos, or even colorize the black & white images that you took from 50 years ago! But have you ever thought how all those tools were built under the hood?

In this notebook, we will dive into the why, the how, and the mathematical aspects of human's perception of colors. We will explore a color space that mimics human's perception of colors better and better as we go deeper into the notebook.

Additional notes: In this notebook, the math of how transferring among color spaces works is not required in order to understand the project, so feel free to skip any 'mathy' parts :)

Prerequisite: Understanding of basic linear algebra

- Vector, Matrix muliplication
- Transpose matrix
- Linear transformation, non-linear transformation

## Outline
1. Introduction to color spaces
Grayscale color space
RGB color space
XYZ color space
Lab color space
2. Data preprocessing
Identify the input of the model
Convert into appropriate color space
Feature scaling
3. Train model
Identify the appropriate model to find the colors for the input
4. Diagnostics (bias, variance, error analysis)

   
## What are Grayscale images?
(insert image here)

Simply, a Grayscale image consists of different shades of gray, ranging from pure black to pure white. It's called 'Grayscale' as we only see black and white colors, but no colors like Red, Green, Blue.

To make things clear, think of a black and white image on a TV from the 1950s, compared to a colored image on the TV in your house right now.

### Grayscale image as Matrix representation
Now the Grayscale image can be represented as a 2D image of width and height, with only 1 channel, as there are only black and white colors.

In mathematical terms, they are represented as a matrix with row and column. Each element stands for the pixel value, ranges from 0 to 255. It's also the range of the shades of gray, from pure black to pure white, respectively.

(insert image here)

Source: https://www.researchgate.net/figure/Matrix-for-certain-area-of-a-grayscale-image-17_fig3_325569674

0 = pure black
255 = pure white
This explanation will be used to define a Grayscale image as a NumPy array later in this notebook.

## Why RGB images?
(insert image here)

Source:https://www.bbc.co.uk/news/business-46125741

Before the outbreak of technology, we usually watch TVs with a screen with only Grayscale images. RGB images are born after many researches on human's perception of colors, with the purpose of bringing more realistic visuals to people.

Nowadays, RGB images are used for images display in our electronic devices.

## What is the LAB color space?
We have introduced the RGB color space, which is used to approximate human's perception of colors. But there's another color space that does the same job but performs much more accurate: LAB color space.

(insert image here)

Really, the only difference of LAB color space is that it can approximate to human's vision better than RGB does. But here comes the more interesting part: How differently does LAB function compared to RGB?

### What do components in the LAB color space mean?
To make everything clear, we will compare the difference of the functionality between RGB and LAB.

RGB: it's separated into 3 components

R: red channel
G: green channel
B: blue channel
Each channel ranges from 0 to 255, representing the amount of contribution of that color to the RGB image

LAB: it's separated into 3 components

L: lightness channel, ranging from 0 to 100, with 0 of black, and 100 of white
a: green-red channel, ranging from -a (green), to a (red)
b: yellow-blue channel, ranging from -b (blue), to b (yellow)
Okay, so how does LAB perform better than RGB exactly?
This is related to our human's visual system. In the RGB color space, its channels only represent the intensity of a single color to create a colored image. However, human doesn't perceive color in a linear fashion. We see colors in pairs: green-red, blue-yellow; therefore, we need a non-linear color space that constructs these pairs. Thus, LAB color space is designed.

Now imagine a random color point in the figure above. This color point is the point where we are looking with our eyes at. It's values are in the following:

x-axis: a value that hues between green and red
y-axis: a value that hues between blue and yellow
z-axis: a value that hues between black and white
We can see a color point in the LAB color space has a variation of all green, red, blue, yellow, and the lightness colors. This is exactly how human's vision works.

### Why LAB?
LAB is made up from L, a, b channels, and the L channel is exactly the grayscale channel, which will be passed in as the input for the model, and the target will be the ab channels stacked on top of each other. Thus, a transformation from RGB color space to LAB color space is preferred.

