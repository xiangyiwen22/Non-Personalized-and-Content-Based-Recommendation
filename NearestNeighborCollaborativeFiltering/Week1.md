# User-User Collaborative Filtering
To predict how much a target user will like an target item, the system first generates a neighborhood of other users who have agreed with that user on other items in the past. Then the system computes a weighted, normalized average of what those other users rated the target item. <br> 

Given a set of items *I*, and a set of users *U*, and a sparse matrix of ratings *R*

Equation 1 - Predictive Score for ith item and uth user <br>
![equation](http://latex.codecogs.com/gif.latex?S_%7Bu%2C%20i%7D%20%3D%20%5Cfrac%7B%5Csum_%7Bv%5Cepsilon%20u%7Dr_%7Bvi%7D%7D%7B%5Cleft%20%7C%20U%20%5Cright%20%7C%7D) <br>
denominator- number of users <br>

Equation 2 - Normalize it due to high-biased and low-biased users! <br>
![equation](http://latex.codecogs.com/gif.latex?S_%7Bv%2C%20i%7D%20%3D%20%5Cbar%7Br_%7Bv%7D%7D&plus;%20%5Cfrac%7B%5Csum_%7Bv%5Cepsilon%20u%7D%28r_%7Bvi%7D-%5Cbar%7Br_%7Bv%7D%7D%29%7D%7B%5Cleft%20%7C%20U%20%5Cright%20%7C%7D)

Equation 3 - Predictive Score weighted by user similarity between user u and user v <br>
![equation](http://latex.codecogs.com/gif.latex?S_%7Bu%2C%20i%7D%20%3D%20%5Cfrac%7B%5Csum_%7Bv%5Cepsilon%20u%7Dr_%7Bvi%7D%5Ccdot%20w_%7Buv%7D%7D%7B%5Csum_%7Bv%5Cepsilon%20u%7Dw_%7Buv%7D%7D)

#### Final Equation<br>
![equation](http://latex.codecogs.com/gif.latex?S_%7Bv%2C%20i%7D%20%3D%20%5Cbar%7Br_%7Bv%7D%7D&plus;%20%5Cfrac%7B%5Csum_%7Bv%5Cepsilon%20u%7D%28r_%7Bvi%7D-%5Cbar%7Br_%7Bv%7D%7D%29%5Ccdot%20w_%7Buv%7D%7D%7B%5Csum_%7Bv%5Cepsilon%20u%7Dw_%7Buv%7D%7D) <br>
By combining equation 1, 2 and 3 ... 
- v not equal to U
- limit size of neighborhood to top-*k* neighbors
- limit similarity of neighborhood to sim > sim_threshold
- negative correlation - disagree between 2 users, may user *|sim|* or *sim* 
- Small overlap (only 2 items in common)
<br>

How to compute weight? How to describe the 2 users are similar? --> similarity metric by Pearson Correlation <br>
![equation](http://latex.codecogs.com/gif.latex?w_%7Buv%7D%20%3D%20%5Cfrac%7B%5Csum_%7Bi%5Cepsilon%20I%7D%28r_%7Bvi%7D-%5Cbar%7Br_%7Bv%7D%7D%29%7D%7B%5Csigma%20_%7Bu%7D%5Csigma%20_%7Bv%7D%7D) <br>
denominator - product std of 2 users ratings <br>

#### Implementation Issues
Given *m=|U|* users and *n=|I|* items:
- Computation can be a bottleneck 
  - Correlation bt 2 users is *O(n)*
  - All correlations for a user is *O(mn)*
  - All pairwise correlations is *O(m^2n)*
  - Recommendations at least *O(mn)*
- Make it more practical 
  - More persistent neighborhoods (m->k)
  - Cached or incremental correlations

#### Assumptions: our past agreement predicts our future agreement
- Our tastes are either individually stable or move in sync with each other
- Our system is scoped within a domain of agreement
 