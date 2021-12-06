# Unsupervised Learning: Customer Segmentation

## Summary

In this Jupyter notebook, we used unsupervised learning to cluster the customer base of a bank into different profile groups. First, we undertook Exploratory Data Analysis to get an overview of our data to make sure it is appropriate for modeling. We then used the K-Means, Gaussian Mixture, and K-Medoids algorithms to build our clustering models and then we compared their performances by observing different metrics such as how well the models account for outliers. 

## The Data

Data is of various customers of a bank with their credit limit, the total number of credit cards the customer has, and different channels through which customer has contacted the bank for any queries, different channels include visiting the bank, online and through a call centre.

- **Sl_no** - Customer Serial Number
- **Customer Key** - Customer identification
- **Avg_Credit_Limit**	- Average credit limit (currency is not specified, you can make an assumption around this)
- **Total_Credit_Cards**	- Total number of credit cards 
- **Total_visits_bank**	- Total bank visits
- **Total_visits_online** -	 Total online visits
- **Total_calls_made** - Total calls made

## Technologies Used

* Numpy
* Pandas
* Matplotlib
* Seaborn
* Sklearn
* KMeans
* GaussianMixture
* KMedoids

## Data Preprocessing and Exploratory Data Analysis

In this section we dealt with duplicate values and dropped unecessary columns that we don't need for modeling such as customer keys. We then examined the distributions and summary statistics of the variables. The distribution and box plot for average credit limit produced by our function is displayed below as an example

![Screen Shot 2021-12-02 at 4 06 41 PM](https://user-images.githubusercontent.com/88220704/144510816-04ad2a37-17f6-428d-b6e6-aaeea487d46c.png)

We also looked for correlations among the different variables using a heatmap: 

![Screen Shot 2021-12-02 at 4 08 12 PM](https://user-images.githubusercontent.com/88220704/144511020-ab3fc316-93ec-4a6a-a466-61aa82591175.png)

Finally, we scaled the data to make it optimal for our clustering models. 

## Models 

### K-Means

The first algorithm we used was K-Means. The intuition behind this algorithm involves grouping data points together into clusters based on certain similarities. This algorithm works by identifying *k* number of centroids, and then allocating every data point to the nearest cluster while keeping centroids as small as possible. The algorithm then stops creating and optimizing clusters when either the centroids have stabilized meaning there is no change in their values because the clustering has been successful, or the defined number of iterations has been achieved. 

But how do we know what value of *k*(number of clusters to use) to use? 

One way is to use the elbow method which is one of the most popular methods to determine the optimal value of *k*. It works by calculating the sum of squared distances of samples to their closest cluster, also known as **inertia**. We then plot the SSE vs. k  (as shown below) and choose the "elbow" point to obtain our optimal *k* value which is where we see the "kink" in the graph. 

![Screen Shot 2021-12-02 at 4 22 05 PM](https://user-images.githubusercontent.com/88220704/144512693-d71c6af5-067d-4840-b481-a26ed9d85919.png)

As we can see, the elbow point is 3. 

After obtaining our optimal *k* value, we then created the cluster profiles using the algorithm and created summary statistics and box plots for each label as shown below, and then observed the differences between the clusters. For example, cluster 2 clearly has considerably higher averge credit limit, posesses more credit cards, and don't visit the bank as much as other clusters. 

![Screen Shot 2021-12-02 at 4 25 01 PM](https://user-images.githubusercontent.com/88220704/144513048-b7c619f7-a33b-44f8-a0a8-a3d94eefb3a8.png)

![Screen Shot 2021-12-02 at 4 25 20 PM](https://user-images.githubusercontent.com/88220704/144513081-d0b94f3f-ed61-44ac-933e-937c6abdf2e0.png)


## Gaussian Mixture

One drawback of the K-means algorithm is that it is not great at identifying cluster when the data distribution of points is not in a circular form. Gaussian Mixture models on the other hand, work a different way and can overcome this problem. GMMs assume that thetre are a certain number of Gaussian distributions and that each of these distributions represents a cluster. Thus, a GMM groups the data points belonging to a single distribution together. As a result, GMMS are probabilistic models that use the soft clustering approach for distributing the points in different clusters. 

After applying this algorithm to our data, we saw the following results. 

![Screen Shot 2021-12-02 at 4 31 45 PM](https://user-images.githubusercontent.com/88220704/144513797-2e830040-d021-4556-8b20-08a19145c5d1.png)

![Screen Shot 2021-12-02 at 4 31 59 PM](https://user-images.githubusercontent.com/88220704/144513822-ddbf3cc8-bdb0-4aa6-b538-694a2bc8381f.png)

As we can see, the clusters ended up being very similar to that of K-Means and the distributions of both the number of observations in each cluster as well as the boxplots show identical results. 

## K-Medoids

Finally, we used the K-Medoids algorithm to see how well it can segment our customer base into appropriate clusters. The difference between K-Medoids and K-Means is that K-Medoids actually makes the final centroids actual datapoints which in turn makes the centroids interpretable. For K-Means, we were obtaining the mean of all points present in the cluster whereas for K-Medoids uses a cost function to compute the new centroid point. 

After applying the algorithm, we obtained the following results. 

![Screen Shot 2021-12-03 at 2 17 47 PM](https://user-images.githubusercontent.com/88220704/144667421-a803e10c-f36d-48bd-ae6b-4b15468403c4.png)

![Screen Shot 2021-12-03 at 2 18 02 PM](https://user-images.githubusercontent.com/88220704/144667446-0599ac5b-e492-4f38-9519-8ef026c460fd.png)

We can observe that K-Medoids is better at detecting outliers because the boxplots display more of them compared to K-Means, and we can also see that there is a more even split of the three clusters compared to K-Means. 



