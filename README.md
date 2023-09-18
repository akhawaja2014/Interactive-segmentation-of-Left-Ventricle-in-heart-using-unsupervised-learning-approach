# Interactive segmentation of the Left Ventricle in the heart using an Unsupervised learning approach

## Authors: Arsalan Khawaja & Bui Thien Bao
Arsalan Khawaja is currently a joint PhD Student at NTNU, Norway, and the University of Burgundy, France. His past experience includes intern researcher at the Endoscopy and Computer Vision (EnCoV) Research Group at Clermont-Ferrand, France, and as a Research Assistant at the Institute of Space Technology, Islamabad. His area of interest is Interactive Machine Learning, Image registration, Reflectance Transformation Imaging, and Control theory. Currently, he is working on developing Optimization Algorithms for Reflectance Transformation Imaging. Link to LinkedIn Profile https://www.linkedin.com/in/arsalankhawaja/

Thien Bao BUI is a graduate in the domain of Computer Vision. He has an International Master in Computer Vision and Robotics (VIBOT) from the University of Burgundy, France. He likes to work on challenging tasks in the fields of Image Processing, Deep Learning, and 3D Geometry. He is currently working in SurgAR (Surgical Augmented Reality https://surgar-surgery.com/ ) as a Software engineer. 


## Executable File
The link to executable file (for Ubuntu) can be found in the repository as well as in this link: https://drive.google.com/file/d/1QV_SJl5ikvbxa1Ck75qKnBAoV_62Aivq/view?usp=sharing

## What this Project is about?
Left Ventricle is an integral part of the heart. It pumps blood into the body. Cardiovascular diseases are quite common in the modern world. The health of the heart can be studied using the left ventricle. Most heart diseases can be diagnosed by retrieving important information from systole and diastole operations of the heart via effective medical imaging analysis of Left Ventricle (LV). The segmentation of the Left Ventricle plays an important role in retrieving the ejection fraction (a parameter which indicates the heart’s health). Since Magnetic Resonance Images (MRI) are noisy and not really perfect, scientific community is always curious to find more efficient, reliable, robust and more accurate segmentation methods to calculate ejection fraction.
 In this project, a combination of smoothing algorithm, K-means algorithm and border following algorithm is implemented.
 

### Index Terms
K-means, Python, Border Following Algorithm, Left Ventricle, Adaptive Smoothing, Clustering, Hough Transform.

## How to Implement the Project / Understanding of Code
In order to help normal users who are not familiar with
coding, this tool is created with a very friendly GUI allowing
them to perform instance segmentation on image in a very
simple way. We created this tool using PyQt5 - a free software
developed by the British firm Riverbank Computing. Here is
a screenshot of our application. The details of how to use it
is mentioned below.


![GitHub Logo](/Report_files/gui.PNG)

* Load Nifti image: The button used to browse to a 4D
nifti image. Our application works only on this type of
file.
* After loading the nifti file, its information regarding
number of slices and number of images of each slices
as well as the first 2D image of the current slice are
displayed on screen. For example, the current nifti file is
from patient015. There are total 21 slices in this file. The
first image of the first slice is displayed automatically on
the screen. The image will be rotated and flipped before
displaying to give the best orientation of the heart. Below
the image is a horizontal bar help switching between
images.
* Run: This button is used to perform segmentation on
the current image. Our application allows performing
segmentation only on one image at a time. Users need
to change the image on the left before continuing
segmenting.
* Calculate: This button is used to perform calculation the
End Diastolic and End Systolic volume as well as the
ejection fraction. It will take 2 inputs: the ED and ES slice
number on the left. Users need to specify them before
click on calculate button.

Python programming language was used for the
implementation. The
following subsections take us step by step through the ladder
of project.
To begin with, fine tuning the smoothing algorithm is
considered as the most time-consuming task of this paper,
since we need to find a group of hyper-parameters that works
for nearly 2000 different images. It is ideal when this algorithm
helps highlighting the difference between the left ventricular
and its surrounding pixels. In order to achieve it, we also apply
the contrast stretching technique on the smoothed image. The
following figure illustrates the difference between a good and
a bad smoothing effect (image taken from the patient 20, 1st
ED slice).

![GitHub Logo](/Report_files/goodbadsmoothing.PNG)

The left image is a bad smoothing image since it cannot highlight
the difference between the left ventricular cavity and its surrounding pixels, on
the contrary to the right image which is a good smoothing image. It affects
badly the result of the segmentation since the K-means algorithm depends
heavily on the pixel intensities. Indeed, the left image gives 0% as the result
for Dice metric, while the right image gives 94%.

For K-means clustering, we set the number of cluster k = 3.
It seems to be the optimal choice in our case. In this dataset,
it is recognized that the pixel intensity of the left ventricular
is not homogeneous for a larger number of images. Therefore,
when we set the value of k greater than 3, the left ventricle
will be separated. It is shown in this figure below (image taken
from patient 25, 6th ED slice):

![GitHub Logo](/Report_files/k3.PNG)

In addition, there are a lot of images in which the pixels
surrounding and inside left ventricle are similar. If we set
k = 2, the left ventricle could be enlarged. It also affects
the accuracy of our algorithm.
For the implementation of border following algorithm, it is
necessary to mention that this algorithm can work only on
Fig. 10. The left image is a bad smoothing image since it cannot highlight
the difference between the left ventricular cavity and its surrounding pixels, on
the contrary to the right image which is a good smoothing image. It affects
badly the result of the segmentation since the K-means algorithm depends
heavily on the pixel intensities. Indeed, the left image gives 0% as the result
for Dice metric, while the right image gives 94%.
Fig. 11. The right image is the result with k = 4. The left ventricle is
clearly separated, on the contrary to the left image with k = 3.
binary image. If we set k = 2, no action need to take. In
case we set k > 2, we need to process the clustered image
before passing it to this function. It can be done by separating
each cluster from each other. The number of binary images
therefore will be equal to the number of cluster. Then we
apply border algorithm on each image and get the contour
that satisfy our condition.
By testing various set of

## Understanding of dataset /Input
The dataset is provided by Dijon University Hospital Center.
It comprises of 100 Magnetic Resonance examinations,
dividing into 5 classes: Normal, Systolic heart failure
with infarction, Dilated cardiomyopathy, Hypertrophic
cardiomyopathy, Abnormal right ventricle. All images are
short axis slices, in Nifti format. The ground truth label
field is label as 0,1,2,3 representing pixels located in the
background, right ventricular cavity, myocardium and left
ventricular cavity. Therefore, preprocessing the ground truth
label is necessary since our task concerns only the left
ventricular cavity. The number of images of each examination
is various. In this paper, we use only the images from the
end diastolic and end systolic slices of each patient. The bar
graph following is for illustration.


![GitHub Logo](/Report_files/esed.PNG)


 

## Anatomy of Heart
The heart is made up of four chambers: two upper chambers known as the left atrium and right atrium and two lower chambers called the left and right ventricles. These are shown in following figure.

![alt text](Report_files/heart.PNG)

The left ventricle is considered an important part of the cardiovascular system. It is thought off as a pump that supplies blood to the body. The mass of the left ventricle, as estimated by magnetic resonance imaging, averages 143 g± 38. 4 g, with a range of 87 – 224 g. 
Another important thing to discuss are the two phases of the cardiac cycle. They are called Systole and Diastole. They occur as the heart beats, pumping blood through a system of blood vessels that carry blood to every part of the body. Systole occurs when the heart contracts to pump blood out, and diastole occurs when the heart relaxes after contraction. 
## What is Ejection Factor?
Ejection fraction (EF) refers to how well your left ventricle (or right ventricle) pumps blood with each heart beat. The ejection fraction can be calculated as follows:

![first](https://latex.codecogs.com/gif.latex?%5Cbegin%7Bequation%7D%20%5Cmathrm%7BEF%7D%3D%5Cfrac%7BV_%7B%5Cmathrm%7Bendo%7D%7D%5Cleft%28t_%7B%5Cmathrm%7BD%7D%7D%5Cright%29-V_%7B%5Cmathrm%7Bendo%7D%7D%28t%5Cmathrm%7Bs%7D%29%7D%7BV_%7B%5Cmathrm%7Bendo%7D%7D%5Cleft%28t_%7B%5Cmathrm%7BD%7D%7D%5Cright%29%7D%5Clabel%7Beq%3A-9%7D%20%5Cend%7Bequation%7D)

Here note that V_endo is the volume of the inner walls of the heart,V_endo(tD) =max_t[V_endo(t)] is the end-diastolic volume and V_endo(tS) = mint[V_endo(t)] is the end-systolic volume.

## Methodology of the Project
The flowchart demonstrates
work flow. Neccessary iterations were done to find the optimal combination
of all algorithm parameters with the goal of acheiving the highest
accuracy possible.


![GitHub Logo](/Report_files/methodology.PNG)

### Pre Processing
We considered Feature-Preserving Adaptive Smoothing Method (FPASM) as a pre processing step
for our project. Adaptive smoothing is a class of typical nonlinear smoothing techniques
that has been studied for many years.

The idea is to adapt pixel intensities to the local attributes of
an image on the basis of discontinuity measures. Note that in this
algorithm there are two kind of discontinuities, Local and Contextual
discontinuity. This novel approach joins these both discontinuities
to preserve edges and at same time smooths images. It is brilliant.

In order to measure local discontinuities, we define four detectors
for pixel $(x,y)$ along four directions. These four directions are
vertical (V), horizontal (H), diagonal (D), and counter-diagonal (C),
respectively. Accordingly, four detectors are defined as

![img](http://latex.codecogs.com/svg.latex?%5Cbegin%7Bequation%7D%0D%0A%5Cbegin%7Barray%7D%7Bc%7D%0D%0AE_%7BH_%7Bxy%7D%7D%3D%5Cleft%7CI_%7Bx%2B1%2Cy%7D-I_%7Bx-1%2Cy%7D%5Cright%7C%5C%5C%0D%0AE_%7BV_%7Bxy%7D%7D%3D%5Cleft%7CI_%7Bx%2Cy%2B1%7D-I_%7Bx%2Cy-1%7D%5Cright%7C%5C%5C%0D%0AE_%7BC_%7Bxy%7D%7D%3D%5Cleft%7CI_%7Bx%2B1%2Cy%2B1%7D-I_%7Bx-1%2Cy-1%7D%5Cright%7C%5C%5C%0D%0AE_%7BD_%7Bxy%7D%7D%3D%5Cleft%7CI_%7Bx%2B1%2Cy-1%7D-I_%7Bx-1%2Cy%2B1%7D%5Cright%7C%0D%0A%5Cend%7Barray%7D%5Clabel%7Beq%3A%7D%0D%0A%5Cend%7Bequation%7D)

Here I_(x,y) is the intensity of pixel (x,y). To be more clear
we constructed this figure to demonstrate.

![GitHub Logo](/Report_files/localdisc.png)

we define the local discontinuity as:

![img](http://latex.codecogs.com/svg.latex?%5Cbegin%7Bequation%7D%0D%0AE_%7Bxy%7D%3D%5Cfrac%7BE_%7BH_%7Bxy%7D%7D%2BE_%7BV_%7Bxy%7D%7D%2BE_%7BC_%7Bxy%7D%7D%2BE_%7BD_%7Bxy%7D%7D%7D%7B4%7D%5Clabel%7Beq%3A-1%7D%0D%0A%5Cend%7Bequation%7D)

In order to detect contextual discontinuities, we use spatial variance
to make a measure. First, we define a contextual neighborhood associated
with pixel (x;y), Nxy(R):

![img](http://latex.codecogs.com/svg.latex?%5Cbegin%7Bequation%7D%0D%0AN_%7Bxy%7D%28R%29%3D%5C%7B%28i%2Cj%29%7Cx-R%5Cleq+i%5Cleq+x%2BR%2Cy-R%5Cleq+j%5Cleq+y%2BR%5C%7D%5Clabel%7Beq%3A-2%7D%0D%0A%5Cend%7Bequation%7D)


Note that, here R(R>1) is a parameter that determines the size
of this contextual neighborhood. The contextual neighborhood is defined
here without explicitly counting image boundaries. The parameter R
describes a spatial scale or a resolution that critically determines
results of the contextual discontinuity measure. We calculate the
mean of pixels on N_{xy}(R) as:

![img](http://latex.codecogs.com/svg.latex?%5Cbegin%7Bequation%7D%0D%0A%5Cmu_%7Bxy%7D%28R%29%3D%5Cfrac%7B%5Csum_%7B%28i%2Cj%29%5Cin+N_%7Bxy%7D%28R%29%7DI_%7Bi%2Cj%7D%7D%7B%5Cleft%7CN_%7Bxy%7D%28R%29%5Cright%7C%7D%5Clabel%7Beq%3A-3%7D%0D%0A%5Cend%7Bequation%7D)


and the spatial variance can be calculated as:


![img](http://latex.codecogs.com/svg.latex?%5Cbegin%7Bequation%7D%0D%0A%5Cbegin%7Baligned%7D%5Csigma_%7Bxy%7D%5E%7B2%7D%28R%29++%3D%5Cfrac%7B%5Csum_%7B%28i%2Cj%29%5Cin+N_%7Bxy%7D%28R%29%7D%5Cleft%28I_%7Bi%2Cj%7D-%5Cmu_%7Bij%7D%28R%29%5Cright%29%5E%7B2%7D%7D%7B%5Cleft%7CN_%7Bxy%7D%28R%29%5Cright%7C%7D%5C%5C%0D%0A++%3D%5Cfrac%7B%5Csum_%7B%28i%2Cj%29%5Cin+N_%7Bxy%7D%28R%29%7DI_%7Bi%2Cj%7D%5E%7B2%7D%7D%7B%5Cleft%7CN_%7Bxy%7D%28R%29%5Cright%7C%7D-%5Cleft%28%5Cfrac%7B%5Csum_%7B%28i%2Cj%29%5Cin+N_%7Bxy%7D%28R%29%7DI_%7Bi%2Cj%7D%7D%7B%5Cleft%7CN_%7Bxy%7D%28R%29%5Cright%7C%7D%5Cright%29%5E%7B2%7D%0D%0A%5Cend%7Baligned%7D%0D%0A%5Clabel%7Beq%3A-4%7D%0D%0A%5Cend%7Bequation%7D)

 The normalized can be written as:
 
 ![img](http://latex.codecogs.com/svg.latex?%5Cbegin%7Bequation%7D%0D%0A%5Ctilde%7B%5Csigma%7D_%7Bxy%7D%5E%7B2%7D%28R%29%3D%5Cfrac%7B%5Csigma_%7Bxy%7D%5E%7B2%7D%28R%29-%5Csigma_%7B%5Cmin%7D%5E%7B2%7D%28R%29%7D%7B%5Csigma_%7B%5Cmax%7D%5E%7B2%7D%28R%29-%5Csigma_%7B%5Cmin%7D%5E%7B2%7D%28R%29%7D%5Clabel%7Beq%3A-5%7D%0D%0A%5Cend%7Bequation%7D%0D%0A)

The smoothing algorithm as shown in equation  runs through
the entire image updating each pixels intensity value I_{xy}^{t},
where t is the iteration value.

![img](http://latex.codecogs.com/svg.latex%5Cbegin%7Bequation%7D%0D%0AI_%7Bxy%7D%5E%7Bt%2B1%7D%3DI_%7Bxy%7D%5E%7Bt%7D%2B%5Ceta_%7Bxy%7D%5Cfrac%7B%5CSigma_%7B%28i%2Cj%29%5Cin+N_%7Bxy%7D%281%29%2F%5B%28x%2Cy%29%5D%7D%5Ceta_%7Bij%7Dy_%7Bij%7D%5E%7Bt%7D%5Cleft%28I_%7Bi%2Cj%7D%5E%7Bt%7D-I_%7Bx%2Cy%7D%5E%7Bt%7D%5Cright%29%7D%7B%5CSigma_%7B%28i%2Cj%29%5Cin+N_%7Bxy%7D%281%29%2F%5B%28x%2Cy%29%5C%7D%7D%5Ceta_%7Bij%7D%5Cgamma_%7Bij%7D%5E%7Bt%7D%7D%5Clabel%7Beq%3A-7%7D%0D%0A%5Cend%7Bequation%7D)

here note that alpha is a parameter to be set:

 ![img](http://latex.codecogs.com/svg.latex?%5Cbegin%7Bequation%7D%0D%0A%5Cbegin%7Barray%7D%7Bl%7D%0D%0A%5Ceta_%7Bij%7D%3D%5Cexp%5Cleft%28-%5Calpha%5Cnot%5Cnabla%5Cleft%28%5Ctilde%7B%5Csigma%7D_%7Bxy%7D%5E%7B2%7D%28R%29%2C%5Ctheta_%7B%5Csigma%7D%5Cright%29%5Cright%29%5C%5C%0D%0A%5Cgamma_%7Bij%7D%5E%7Bt%7D%3D%5Cexp%5Cleft%28-E_%7Bij%7D%5E%7Bt%7D%2FS%5Cright%29%0D%0A%5Cend%7Barray%7D%5Clabel%7Beq%3A-8%7D%0D%0A%5Cend%7Bequation%7D)
 
 The main goal of smoothing is to alleviate the complexity for subsequent
processes in early vision. With this pre- processing, the results
of our MRI image are shown in figure below:

![GitHub Logo](/Report_files/original.PNG)

and here is the image after adaptive smoothing:

![GitHub Logo](/Report_files/AdaptiveSmoothing.PNG)

We can clearly notice that the algorithm
has blurred the details of object but takes care of the edges. This
will help us in getting great accuracy for segmentation.


## K-Means Clustering

The smoothed images were then clustered using $k$-means algorithm
proposed by Duda and Hart.
This algorithm has four steps as shown in figure
to search for the image clusters.

![GitHub Logo](/Report_files/flowchartforkmeans.PNG)
 The algorithm is quite simple and
is widely used in Machine learning, Econmics, Data science and many
other fields.
The key idea of the K-means algorithm is to divide M points
in N dimensions into K clusters, such that the within-cluster
sum of squares is minimized.K-means
Clustering is categorized as unsupervised learning, which means that
it does not need any intervention by human and leads
way to automatic segmentation of Left Ventricle. The figure
shows results after applying k-means clustering.


![GitHub Logo](/Report_files/clustering.PNG)


## Detection of Region of Interest (ROI)

We know that the left ventricle can thought of as an approximation
of circle. Hough transform is used to detect circular features in
an image. We applied hough transform and detected ventricle. With
the centre of ventricle detected as centre of circle, we declared
the reasonable area around centre of circle as region of interest.
However this approach was not a great idea because:

* Left ventricle is the only circular shape object in image, Many slices
had more than one circular object other than left ventricle which
allowed it hough transform to detect false left ventricle.
* In some images / slices, left ventricle becomes too dark to be detected
as an object.
* In some images / slices, the left ventricle is not near to circular
shape. so hough transform fails

## Segmentation of Left Ventricle
A border following algorithm inspired by 
was used to segment Left Ventricle. Border following is one of the
most important and popular technique in segmentation of binary images.
. It derives a sequence of the coordinates or the chain codes from
the border between a connected component of l-pixels
(l-component) and a connected component of O-pixels
(background or hole).


The basic idea of border following algorithm is simple. It works on
binary image and we already produced binary image by k=2 (2 clusters)
with k-means clustering. The border following algorithm as illustrated
in figure sees th component as 1 and background
as 0.

![GitHub Logo](/Report_files/borderfollowingAlgorithm.PNG)

The figure demonstrates
the border following algorithm. The yellow pixels are some object
border. The algorithm moves through the pixel grid looking for the
jump in pixel intensities. It memorizes that jump and categorizes
them to respective objects according to their spacial location.

When it moves through the pixel grid passing each pixel watching
out their intensity (0 or 1). As soon as it observes a jump from O-Pixel
to 1-Pixel, it memorizes the pixel location and value. After it memorizes
all the jumps i.e switching from O-Pixel to 1-Pixel and vice versa,
It categorizes the the border in number of objects depending whether
the pixel locations are connected to each other or they are sparsely
located.


The resulting segmented image is shown in figure

![GitHub Logo](/Report_files/segmented.PNG)

## Conclusion
During this project, a combination of
smoothing algorithm, K-means algorithm, border
following algorithm is implemented. The accuracy, as
discussed in the previous section, is not very impressive
relative to the state of the art Deep Learning technique. In
the future, further works need to be done such as improving
the accuracy by changing the method to automatically localize
the left ventricle, adding more function to the graphical user
interface that allows to perform segmentation on every images
of one slice at a time, etc. Via this project, we have discovered
new image processing techniques like the smoothing and the
border following algorithm. They are pretty useful techniques
that we will apply them in our next project. This hybrid
approach of using multiple algorithm helped us achieve better
results.



