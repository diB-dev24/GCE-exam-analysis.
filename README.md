# GCE-exam-analysis.
a project exploring the final exams in England in the academic year 2024/2025 based on a dataset collected from the UK government website. The link to the dataset is https://api.education.gov.uk/statistics/v1/data-sets/019c2960-df54-772f-8ad4-a2bc3d3b134f/csv?dataSetVersion=1.0.1

The dataset contains the results of various cohorts of different exam bodies and levels, from various schools.

The dataset contains subsets of data from different schools. 
These subsets have details on the number of entries for each grade, for each subject; this explains the 0 entries in some 'entries_count' column.

The 'Total exam entries' rows capture the sum of grade entries for each item in the 'subject' column.

The 'All subjects' rows captures the sum of grade entries for each grade for all subjects in the school.

# in this project, we will be analysing the exam entries in the GCE exams.
After some data wrangling, we can create a dataset focusing on the results of the GCE alone- looking at the grades distributions of the entries.
<img width="1023" height="545" alt="image" src="https://github.com/user-attachments/assets/7cb72a83-2103-4a1d-b211-c921b654b2ec" />

The GCE dataset also focused on the 10 most popular subjects (those with more than 2000 entries) in its analysis. This was primarily done to sample the data but also because there was not enough space to run all the 75 subjects in the dataset. These include: Mathematics, Psychology, Biology, Chemistry, Sociology, Business Studies, Economics, History, Physics, English Literature and Geography.

After identifying the columns of interest, standardizing and clustering the data using KMeans. The choice of the K value was based on looking at the silhouette scores and elbow plot, and visualizing the clusters using either TSNE or PCA. A code from 'The scikit-learn developers' licence: SPDX-License-Identifier: BSD-3-Clause was also used to consider the best value to cluster the data. after all considerations, a cluster value of 5 was selected as it clusters the data better compared to looking at the best silhouette score or elbow plot, and groups the outliers.

From the distribution of the clusters, we can see that cluster 0 has the highest number of entries, followed by cluster 3, 1, 4 and 2.

### Cluster 0
- Has the highest number of entries, and the highest number of entries for each subject.
- Entries counts lie between 1800 and 1100.
- Has all 11 popular subjects.
- History has the highest entries count.

### Cluster 3
- Has the second highest number of entries, and the second highest number of entries for each subject.
- Entries counts lie between 700 and 50.
- Has all 11 popular subjects.
- Mathematics has the highest entries count.

### Cluster 1
- Has the third highest number of entries, and the third highest in each subject.
- Entries counts lie between 70 and 0.
- Has all 11 popular subjects.
- Psychology has the highest entries count. 

### Cluster 4
- Has the forth highest number of entries.
- Entries counts lie between 100 and 0
- Has all 11 popular subjects.
- Mathematics has the highest entries count. Huge gap between it and the next subject, Biology.

### Cluster 2
- Has the least number of entries.
- Entries counts lie between 5 and 0.
- Has 10 of the 11 popular subjects. Missing subject: Mathematics.
- Psychology has the highest entries count.

Looking at the boxplots from the analysis, here are some of the findings noted;
### What it shows
- Each box represents the distribution of total exam entries for each subject.
- The center line is the median number of entries.
- The top and bottom of the box are the 75th and 25th percentiles (the interquartile range).
- The whiskers extend to the typical range of values, and any points outside are likely outliers.
- This is comparing subject popularity and variability, not individual grades.

### What you can learn from it
- Subjects with a higher median box are the ones with more exam entries overall.
- A taller box means more variability in how many students took that subject across different schools/observations.
- Subjects with short boxes and short whiskers have more consistent entry counts.
- Outliers show subjects where some schools had unusually high or low entry counts compared to most schools.

This analysis clusters the data on the GCE results based on the exam entries from each school. The analysis also clusters the performances in each subject looking at the popularity of each subject in each cluster. 

### Why this is useful
- It helps identify which subjects have the largest and most variable exam participation.
- You can spot popular subjects and those with more uneven school-level coverage basing on the clusters.
- This is a good first step before focusing on specific popular subjects or clustering schools by subject performance.


# Recommendations
- To improve on this analysis, we can categorise the 'grade' column in the gce_analysis_df dataframe into heirachical categories (excluding the 'Total exam entries). This would be insturmental in clustering the schools by performance.

- The analysis is also limited in the scope of view as it only analyses the 10 most popular subjects only. There are 65 more subjects to observe.

- Some of the clusters overlap. This suggests that the clustering is not as accurate as it should be. Using a different classification model such as Hierachical Methods.
