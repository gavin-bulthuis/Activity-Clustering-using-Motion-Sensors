# Activity Clustering using Motion Sensors 

## Authors

- [@gavin-bulthuis](https://www.github.com/gavin-bulthuis)
- [@kevint4890](https://www.github.com/kevint4890)
- [@ivanfierros](https://github.com/ivanfierros)

## Data source

- [UCI Machine Learning Repository - Daily and Sports Activities](https://archive.ics.uci.edu/dataset/256/daily+and+sports+activities)
  * 8 subjects (4 male and 4 female)
  * 19 activities
    * Playing Basketball
    * Running on Treadmill
    * Jumping
    * Biking in Horizontal Position
    * Biking in Vertical Position
    * Moving in Elevator
    * Standing in Elevator
    * Exercising on Stairmaster
    * Exercising on Elliptical
    * Rowing
    * Walking on Inclined Treadmill
    * Walking on Treadmill
    * Walking in Parking Lot
    * Ascending Stairs
    * Descending Stairs
    * Lying on Side
    * Lying on Back
    * Standing
    * Sitting
  * 5 minutes performing an activity per person
    * Divided into 60 segments or a sensor reading every 5 seconds
  * 5 Sensor Units
    * Torso, Right Arm, Left Arm, Right Leg, Left Leg
    * 9 sensors per sensor unit
      

## Overview

The goal of this project was to determine if raw sensor data could be used to cluster activities based on biomechanical similarities. A successful outcome could lead towards improvements in areas like fitness trackers and rehabilitation tools.

To accomplish this goal, we used the following process:

  - **Dimensionality Reduction**
     - Principal Component Analysis: Utilized to reduce the dimensionality of the data from 45 to 20 features per person in each activity. Over half of the features were removed while still keeping roughly 80% of the variance per activity.

  - **Feature Extraction**
     - Summary Statistics: Features that were extracted from each sensor in each activity such as the mean, median, standard deviation, and more. These were added as features to the already reduced raw data to provide a comprehensive representation of motion dynamics.
 
  - **Clustering Methods**
      - K-Means Clustering: Partitions data into k clusters by minimizing the variance within each cluster using centroid-based assignments.
      - Spectral Clustering: Uses the eigenvalues of a similarity matrix to transform data into a lower-dimensional space, then applies clustering in that space.
      - Hierarchical Clustering: Builds a tree-like structure of nested clusters by either merging (agglomerative) or splitting (divisive) data based on a distance metric.
 
  - **Cluster Validation**
    - Silhouette Score: Measures how well-separated the clusters are by comparing intra-cluster cohesion with inter-cluster separation.
    - Dunn Index: Evaluates compactness and separation of clustersby considering the ratio between the smallest and inter-cluster distance and largest intra-cluster distance.
  

## Cluster Performance Summary

We determined that the activities best fit into 3 large branches in high, medium, and low intensity activities. Based on these 3 main branches, we decided that our activites would optimally fall into the following 9 clusters.

* Low Intensity:
  * Stationary Movements:
    * Lying on Side, Lying on Back, Standing, Sitting, Standing in Elevator
* Medium Intensity:
  * Biking Movements: 
    * Stationary Bike in Horizontal/Vertical Position
  * Rowing Movements: 
    * Rowing
  * Flat Walking Movements: 
    * Walking on a Treadmill, Walking in a Parking Lot
  * Incline/Decline Movements: 
    * Ascending Stairs, Descending Stairs, Walking on Incline Treadmill
  * Other Machine-Based Movements: 
    * Exercising on an Elliptical, Moving in an Elevator, Walking on Stairmaster
* High Intensity:
    * Playing Basketball
    * Running on a Treadmill
    * Jumping

Using 9 clusters gave us the following results for Silhoutte Score and Dunn Index. 

- **K-Means Performance:**
  - Average Silhouette Score: 0.2057
  - Average Dunn Index Score: 0.6864

- **Spectral Performance:**
  - Average Silhouette Score: 0.1132
  - Average Dunn Index Score: 0.2508

- **Hierarchical Performance:**
  - Average Silhouette Score: **0.2086**
  - Average Dunn Index Score: **0.7064**
 
Our research paper goes more in-depth on the specific clustering results using the Hierarchical method and outputs a dendrogram for all 8 subjects.

## Conclusion
The results from our cluster validation indicates that Hierarchical Clustering clusters specific activities the best. Simply visualizing the dendograms supports this claim as well. 
The benefits of using this method also include for the user to specify the number of clusters and distance measure depending on the subject. Hierarchical Clustering not only had the best performance in terms of Silhoutte Score and Dunn Index, but also placed activities in the correct branch of high, medium, and low intensity over 90% of the time.
