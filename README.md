# zeecode
# Data Normalization vs Standardization
# Normalization: Normalization is the method used to arrange the data in a database. It is a scaling method that reduces duplication in which the numbers are scaled and moved between 0 and 1. Formula : 𝑁=  (𝑥′ −𝑥(𝑚𝑖𝑛))/(𝑥(𝑚𝑎𝑥)−𝑥(𝑚𝑖𝑛))
# Standardization: referred to as z-score Normalization, occasionally is a method for rescaling the values that meet the characteristics of the standard normal distribution while being similar to normalizing. Formula: 𝑆=  (𝑥′− 𝜇)/𝜎
# Lets see how we perform Normalization and standardization on data sets.
import pandas as pd
import numpy as np
from scipy import stats
from math import comb, factorial
from scipy.stats import skewnorm
import seaborn as sns
import matplotlib.pyplot as plt

n1000 = np.random.normal(loc = 20, scale = 10, size = 1000)
u1000 = np.random.uniform(low = 10, high = 20, size = 1000)
sp1000 = skewnorm.rvs(10, scale = 10, size = 1000)
sn1000 = skewnorm.rvs(-10, scale = 10, size = 1000)

norm_stand = pd.DataFrame(n1000)

norm_stand['Uniform_Dist'] = u1000
norm_stand['Positive_skewed_Dist'] = sp1000
norm_stand['Negative_skewed_Dist'] = sn1000

norm_stand.rename(columns = {0:'Normal_dist'}, inplace = True)

norm_stand

norm_stand.describe()

## Normalization

norm_stand['Normalization_of_Normal_Dist'] = (norm_stand['Normal_Dist']-norm_stand['Normal_Dist'].min())/(norm_stand['Normal_Dist'].max()-norm_stand['Normal_Dist'].min())
norm_stand['Normalization_of_Uniform_Dist'] = (norm_stand['Uniform_Dist']-norm_stand['Uniform_Dist'].min())/(norm_stand['Uniform_Dist'].max()-norm_stand['Uniform_Dist'].min())
norm_stand['Normalization_of_P_Skew_Dist'] = (norm_stand['Positive_skewed_Dist']-norm_stand['Positive_skewed_Dist'].min())/(norm_stand['Positive_skewed_Dist'].max()-norm_stand['Positive_skewed_Dist'].min())
norm_stand['Normalization_of_N_Skew_Dist'] = (norm_stand['Negative_skewed_Dist']-norm_stand['Negative_skewed_Dist'].min())/(norm_stand['Negative_skewed_Dist'].max()-norm_stand['Negative_skewed_Dist'].min())

## Standardization

norm_stand['Standardization_of_Normal_dist'] = (norm_stand['Normal_Dist'] - norm_stand['Normal_Dist'].mean())/norm_stand['Normal_Dist'].std()
norm_stand['Standardization_of_Uniform_dist'] = (norm_stand['Uniform_Dist'] - norm_stand['Uniform_Dist'].mean())/norm_stand['Uniform_Dist'].std()
norm_stand['Standardization_of_P_Skew_dist'] = (norm_stand['Positive_skewed_Dist'] - norm_stand['Positive_skewed_Dist'].mean())/norm_stand['Positive_skewed_Dist'].std()
norm_stand['Standardization_of_N_Skew_dist'] = (norm_stand['Negative_skewed_Dist'] - norm_stand['Negative_skewed_Dist'].mean())/norm_stand['Negative_skewed_Dist'].std()

## Plots

fig, axs = plt.subplots(figsize=(15, 6),ncols=4)

sns.distplot(norm_stand['Normal_Dist'],ax=axs[0])
sns.distplot(norm_standt['Uniform_Dist'],ax=axs[1])
sns.distplot(norm_stand['Positive_skewed_Dist'],ax=axs[2])
sns.distplot(norm_stand['Negative_skewed_Dist'],ax=axs[3])

fig, axs = plt.subplots(figsize=(15, 6),ncols=3)

sns.distplot(norm_stand['Normal_Dist'],ax=axs[0])
sns.distplot(norm_stand['Normalization_of_Normal_Dist'],ax=axs[1])
sns.distplot(norm_stand['Standardization_of_Normal_dist'],ax=axs[2])

fig, axs = plt.subplots(figsize=(15, 6),ncols=3)

sns.distplot(norm_stand['Uniform_Dist'],ax=axs[0])
sns.distplot(norm_stand['Normalization_of_Uniform_Dist'],ax=axs[1])
sns.distplot(norm_stand['Standardization_of_Uniform_dist'],ax=axs[2])

fig, axs = plt.subplots(figsize=(15, 6),ncols=3)

sns.distplot(norm_stand['Positive_skewed_Dist'],ax=axs[0])
sns.distplot(norm_stand['Normalization_of_P_Skew_Dist'],ax=axs[1])
sns.distplot(norm_stand['Standardization_of_P_Skew_dist'],ax=axs[2])

fig, axs = plt.subplots(figsize=(15, 6),ncols=3)

sns.distplot(norm_stand['Negative_skewed_Dist'],ax=axs[0])
sns.distplot(norm_stand['Normalization_of_N_Skew_Dist'],ax=axs[1])
sns.distplot(norm_stand['Standardization_of_N_Skew_dist'],ax=axs[2])

![image](https://github.com/ShaikZeeshanRaheem/zeecode/assets/129654237/8e24cdeb-035c-415f-8567-efc6fcc0886d) # Normal Distribution Plot
![image](https://github.com/ShaikZeeshanRaheem/zeecode/assets/129654237/8f2b8e12-cfc2-4f30-8db5-6adb2dec2f5a) # Uniform Distribution Plot
![image](https://github.com/ShaikZeeshanRaheem/zeecode/assets/129654237/8a76765c-4e94-4e8c-90a2-e97dcf71217b) # Positive Skew Plot
![image](https://github.com/ShaikZeeshanRaheem/zeecode/assets/129654237/b0872c8a-0c19-4525-b693-f4368701dc40) # Negetive Skew Plot

![image](https://github.com/ShaikZeeshanRaheem/zeecode/assets/129654237/e6de0636-4e8c-4af0-9d8d-b22856536b2d) # Normal Distribution plot + Normalization plot + Standardization plot.
![image](https://github.com/ShaikZeeshanRaheem/zeecode/assets/129654237/af1b1b6d-5b5d-4411-872f-6ef43cdb4c3c) # Uniform Distribution plot + Normalization plot + Standardization plot.
![image](https://github.com/ShaikZeeshanRaheem/zeecode/assets/129654237/ae2223dc-423a-4e55-8bca-65054d642cf9) # Positive Skew plot + Normalization plot + Standardization plot.
![image](https://github.com/ShaikZeeshanRaheem/zeecode/assets/129654237/54480802-6e84-4fd9-aad8-d130a81f43d1) # Negetive Skew plot + Normalization plot + Standardization plot.








