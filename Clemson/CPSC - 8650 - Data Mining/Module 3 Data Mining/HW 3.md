1. Discuss the role of data transformation. Explain with examples how normalization and discretization can improve the efficiency of mining algorithms - Completed 

2. Given the following data (in increasing order) for the attribute age: 13, 15, 16, 16, 19, 20, 20, 21, 22, 22, 25, 25, 25, 25, 30, 33, 33, 35, 35, 35, 35, 36, 40, 45, 46, 52, 70.

- Use smoothing by bin means to smooth these data, using a bin depth of 3. Illustrate your steps. Comment on the effect of this technique for the given data.
    
- How might you determine outliers in the data?
    
- What other methods are there for data smoothing?

 3. Differentiate between supervised and unsupervised discretization. Provide one method for each and discuss how they are applied in practice
 4.  Suppose that a hospital tested the age and body fat data for 18 randomly selected adults with the following results:

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/_a39dd92d1fde429aa6bc79ca39d3cfc5_image.jpeg?expiry=1769105096281&hmac=PtqZjvy6EdFn_tHgN8EVL9sFMuAjRfWY6MLCeoH08Xw)

- Normalize the two attributes based on z-score normalization.
    
- Calculate the correlation coefficient (Pearson’s product-moment coefficient). Are these two attributes positively or negatively correlated? Compute their covariance.

5. Use a flowchart to summarize the following procedures for attribute subset selection:

- stepwise forward selection
    
- stepwise backward elimination
    
- a combination of forward selection and backward elimination

6. Describe the three main methods of normalization and explain their differences. Provide one example each using the values: 12000, 24000, 36000, and 48000.

7. Compare and contrast attribute subset selection and principal component analysis (PCA). When would you prefer one method over the other in dimensionality reduction?

8. Why is dimensionality reduction important in high-dimensional datasets? Define the "curse of dimensionality" and how PCA or nonlinear methods like t-SNE can address it.

9. What is concept hierarchy generation, and how does it support data mining tasks?Create a simple example of a concept hierarchy using geographic location data (e.g., Street → City → State → Country).

10. Suppose you are given a dataset with several redundant attributes. How would you identify and eliminate such redundancies using correlation or covariance analysis?
 11. Suppose a group of 12 sales price records have been sorted as follows:

**5, 10, 11, 13, 15, 35, 50, 55, 72, 92, 204, 215**

Partition them into three bins by each of the following methods:

- equal-frequency (equal-depth) partitioning
    
- equal-width partitioning
    
- clustering
    

12. Robust data loading poses a challenge in database systems because the input data are often dirty. In many cases, an input record may miss multiple values; some records could be contaminated, with some data values out of range or of a different data type than expected. Work out an automated data cleaning and loading algorithm so that the erroneous data will be marked and contaminated data will not be mistakenly inserted into the database during data loading. What are the major challenges of mining a huge amount of data (e.g., billions of tuples) in comparison with mining a small amount of data (e.g., data set of a few hundred tuples)?