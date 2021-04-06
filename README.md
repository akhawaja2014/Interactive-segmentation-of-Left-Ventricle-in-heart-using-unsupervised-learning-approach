# Automatic segmentation of Left Ventricle in heart using hybrid approach

## Executable File
Link to executable file (for Ubuntu) can be found in repository as well as in this link: https://drive.google.com/file/d/1QV_SJl5ikvbxa1Ck75qKnBAoV_62Aivq/view?usp=sharing

## What this Project is about?
Left Ventricle is an integral part of the heart. It pumps blood into the body. Cardiovascular diseases are quite common in modern world. The health of the heart can be studied using left ventricle. Most of the heart diseases can be diagnosed by retrieving important information from systole and diastole operations of heart via effective medical imaging analysis of Left Ventricle (LV). The segmentation of Left Ventricle plays an important role in retrieving the ejection fraction (a parameter which indicates the heart’s health). Since Magnetic Resonance Images (MRI) are noisy and not really perfect, scientific community is always curious to find more efficient, reliable, robust and more accurate segmentation methods to calculate ejection fraction.
 In this project, a combination of smoothing algorithm, K-means algorithm and border following algorithm is implemented.
 

### Index Terms
K-means, Python, Border Following Algorithm, Left Ventricle, Adaptive Smoothing, Clustering, Hough Transform.

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


