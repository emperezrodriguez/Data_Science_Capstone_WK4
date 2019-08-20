# Methodology:

As we mentioned in the data description, we will need to obtain a complete dataframe with the following columns in order to apply clustering:

* Neighborhood: Division of Madrid's urban area.
* Top 10 venues per neighborhood: One in each column of the data frame.

After that, we will cluster the neighborhoods using the **k-means** algorithm. This way, we will separate the 131 neighborhoods of Madrid in 10 different clusters by similarity. We will obtained a 'Cluster Label' column with the obtained cluster and plot the neighborhoods cordinates in a map, painting the ones of each cluster in a different color to make the information easily understandable.

As an extra, once we get all the clusters, we will do a **weighted scoring** regarding the most important venues mentioned by Company&Co: Hotels, restaurants and metro stations. We will need a column for each of these venues and an extra one with the obtained score.

This way, in the end, we will obtain the most suitable neighborhoods for the Cohttps://github.com/emperezrodriguez/Data_Science_Capstone_WK4/blob/master/Problem_Description.mdmpany&Co expansion in order of preference, so our client can make a decision easier.
