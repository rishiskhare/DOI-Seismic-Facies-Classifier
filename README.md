# DOI-Seismic-Facies-Classifier
By Jongho Choi, Litzy Cerezo, Rishi Khare

With special thanks to Kimberly Baldwin (BOEM) and Kevin Smith (BOEM)

## Bureau of Ocean and Energy Management (BOEM)
- BOEM is a federal agency within the United States Department of the Interior (DOI). BOEM, along with its sister agency, Bureau of Safety and Environmental Enforcement promotes energy independence, environmental protection, and economic development.
- BOEM focuses in particular on offshore energy resources, with the mission “to manage development of U.S. Outer Continental Shelf energy and mineral resources in an environmentally and economically responsible way.” 

## What are Seismic Facies?
<img width="1407" alt="Screenshot 2023-12-21 at 6 03 12 PM" src="https://github.com/rishiskhare/DOI-Seismic-Facies-Classifier/assets/30673002/70efbfa8-f9f1-4017-9e54-7239dd77c6eb">

## Training Data
- Training data from Seismic Facies Identification Challenge hosted by AIcrowd [(link to dataset)](https://www.aicrowd.com/challenges/seismic-facies-identification-challenge )
- The data consists of a 3D block of seismic readings. For our purposes, we divided the block into slices along the x and y axes to create 2D facies
<img width="785" alt="Screenshot 2023-12-21 at 6 04 02 PM" src="https://github.com/rishiskhare/DOI-Seismic-Facies-Classifier/assets/30673002/2e6ee974-cc05-47cf-a65f-b3a9b92e74e5">

## U-Net: Image Segmentation Technique
- The contracting path (left) performs repeated downsampling operations, each of which apply a convolution, followed by a Rectified Linear Unit (ReLU) activation, and finally a max pool.
- The expanding path (right) performs repeated upsampling operations, each of which involve up-convolutions and concatenations.
- The intuition driving this is that during the contracting path, feature information is condensed by reducing spatial information. The expansive path takes this increased feature information and concatenates them back with the spatial information to retrieve the features in context. 
- Developed for biomedical image segmentation at the Computer Science Department of the University of Freidberg. 
- The architecture gets its name from the contracting/expanding paths of the net, which form a ‘U’ shape. 
- Source: Ronneberger, Olaf, et al. “U-Net: Convolutional Networks for Biomedical Image Segmentation.” Lecture Notes in Computer Science, 2015, pp. 234–241., https://doi.org/10.1007/978-3-319-24574-4_28. 

<img width="731" alt="Screenshot 2023-12-21 at 6 06 25 PM" src="https://github.com/rishiskhare/DOI-Seismic-Facies-Classifier/assets/30673002/7cf7caef-ac5f-46a9-b797-664cc18b21b7">
<img width="1345" alt="Screenshot 2023-12-21 at 6 08 35 PM" src="https://github.com/rishiskhare/DOI-Seismic-Facies-Classifier/assets/30673002/3de6186f-c17e-45f2-9143-18879c7d5bf3">


## Further Analysis
- W-Net - neural net architecture which in essence concatenates two U-Nets together for fully unsupervised image segmentation
- Classifier - takes the segmented images and classifies the relevant seismic formations
- Feature Augmentation - augment data with additional seismic attributes
<img width="1333" alt="Screenshot 2023-12-21 at 6 09 39 PM" src="https://github.com/rishiskhare/DOI-Seismic-Facies-Classifier/assets/30673002/ad287721-b75a-48c9-99ee-a5f644c35e89">

## K-Means Clustering
- Idea: Clusters a large data set into “k” clusters
- Initially, arbitrarily assign cluster centers randomly, and assign each training points to a cluster
- At each epoch, calculate the arithmetic mean of all points in each cluster (center), and assign each data point to its nearest cluster center
- Source: https://www.nvidia.com/en-us/glossary/data-science/k-means/
<img width="1313" alt="Screenshot 2023-12-21 at 6 12 38 PM" src="https://github.com/rishiskhare/DOI-Seismic-Facies-Classifier/assets/30673002/0afe6150-31ae-442a-8b7f-79e8d7b9cd0f">

## How to determine K?
- When running K-Means, number of clusters (K) is a hyperparameter of the model
Needs to be chosen using validation
- A common loss function to evaluate the quality of K-means output: inertia
- Inertia: the sum of squared distances from each sample point to its centroid
- Elbow plot: shows the marginal benefit of increasing K to decrease inertia
- Diminishing marginal returns
- Elbow plot can smooth for large, complex data

## K-Means Clustering on Seismic Data
- X-axis: Number of Traces (Proxy for Distance)
- Y-axis: Number of Time Samples (Proxy for Depth)
- 3 features used for K-means clustering: 
- RMS_amplitude, generalized_spectral_decomposition', first_derivative
- Showed to contain the most variance in Principal Component Analysis
- Below is an elbow plot for our data:
<img width="599" alt="Screenshot 2023-12-21 at 6 14 05 PM" src="https://github.com/rishiskhare/DOI-Seismic-Facies-Classifier/assets/30673002/919e1a3e-87db-4148-b28d-1f236e5d19f2">

## K-Means on Seismic Data (K = 3 clusters)
<img width="1358" alt="Screenshot 2023-12-21 at 6 14 31 PM" src="https://github.com/rishiskhare/DOI-Seismic-Facies-Classifier/assets/30673002/dd430420-0cf1-4379-9da1-a2af51eaa9da">

## K-Means on Seismic Data (K = 2 clusters)
<img width="1426" alt="Screenshot 2023-12-21 at 6 15 27 PM" src="https://github.com/rishiskhare/DOI-Seismic-Facies-Classifier/assets/30673002/11acfc3a-b6c8-4f32-8e9c-1132c55e8117">

## K-Means on Seismic Data (K = 4 clusters)
<img width="1298" alt="Screenshot 2023-12-21 at 6 15 44 PM" src="https://github.com/rishiskhare/DOI-Seismic-Facies-Classifier/assets/30673002/a75520f4-bc43-43fa-aef0-55e7583f4be6">




