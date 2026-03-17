# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:

```
import pandas as pd
df=pd.read_csv("/content/Encoding Data.csv")
df
```
# OUTPUT:
<img width="802" height="556" alt="image" src="https://github.com/user-attachments/assets/885a7dc1-cf11-4cf1-a70e-0f63f288a332" />




```
# ORDINAL ENCODING
 from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
 pm=['Hot','Warm','Cold']
 e1=OrdinalEncoder(categories=[pm])
 e1.fit_transform(df[["ord_2"]])
```

# OUTPUT:
<img width="787" height="362" alt="image" src="https://github.com/user-attachments/assets/ad932621-9433-480d-9586-d57bb7b44d6a" />


```
 df['bo2']=e1.fit_transform(df[["ord_2"]])
 df
```

# OUTPUT:
<img width="904" height="528" alt="image" src="https://github.com/user-attachments/assets/580160fc-5289-4e97-8dc9-d24fdeb00016" />


```
 # Label Encoder ( orders in alphabetical order)
 le=LabelEncoder()
 dfc=df.copy()
 dfc['ord_2']=le.fit_transform(dfc['ord_2'])
 dfc
```

# OUTPUT:
<img width="946" height="573" alt="image" src="https://github.com/user-attachments/assets/8cb8c627-29b5-426b-a2ff-c630b53e538d" />


```
# ONE HOT ENCODING
 from sklearn.preprocessing import OneHotEncoder
 ohe=OneHotEncoder(sparse_output=False)
 df2=df.copy()
 enc=pd.DataFrame(ohe.fit_transform(df2[["nom_0"]])) # Orders in Alphabetical Order Blue , Green, Red
 df2=pd.concat([df2,enc],axis=1)
 df2
```

# OUTPUT:
<img width="1255" height="624" alt="image" src="https://github.com/user-attachments/assets/8353251e-f4a7-49be-b40e-89c5c4f10027" />


```
 pd.get_dummies(df2,columns=["nom_0"])
```

# OUTPUT:
<img width="1090" height="502" alt="image" src="https://github.com/user-attachments/assets/fd8a4ae4-6643-4839-a11b-732e6e5e7703" />


```
pip install --upgrade category_encoders
```

# OUTPUT:
<img width="1697" height="508" alt="image" src="https://github.com/user-attachments/assets/79491713-3e6d-4205-818e-575f3fa134b2" />


```
from category_encoders import BinaryEncoder
df=pd.read_csv("/content/data.csv")
df
```

# OUTPUT:
<img width="1064" height="555" alt="image" src="https://github.com/user-attachments/assets/ff1ad31c-be5c-440d-8987-640ee4ebfd47" />


```
 be=BinaryEncoder()
 nd=be.fit_transform(df['Ord_2'])
 dfb=pd.concat([df,nd],axis=1)
 dfb
```

# OUTPUT:
<img width="1270" height="579" alt="image" src="https://github.com/user-attachments/assets/00a3a8ec-a682-4b4f-b1a1-c54a5a44f884" />


```
 from category_encoders import TargetEncoder
 te=TargetEncoder()
 CC=df.copy()
 new=te.fit_transform(X=CC["City"],y=CC["Target"])
 CC=pd.concat([CC,new],axis=1)
 CC
```

# OUTPUT:
<img width="1112" height="624" alt="image" src="https://github.com/user-attachments/assets/e65cbb4c-c228-4bd7-8919-58ead44d5e80" />


```
 import pandas as pd
 from scipy import stats
 import numpy as np
 df=pd.read_csv("/content/Data_to_Transform.csv")
 df
```

# OUTPUT:
<img width="1343" height="675" alt="image" src="https://github.com/user-attachments/assets/b6a23179-1306-414e-b964-4fa2ade81f39" />


```
df.skew()
```

# OUTPUT:
<img width="677" height="308" alt="image" src="https://github.com/user-attachments/assets/7522123c-cea2-4d13-96c5-df0e6cb51469" />



```
np.log(df["Highly Positive Skew"])
```

# OUTPUT:
<img width="1168" height="623" alt="image" src="https://github.com/user-attachments/assets/fef7bc98-5a98-46c3-980c-4a209239dd81" />


```
 np.reciprocal(df["Moderate Positive Skew"])
```

# OUTPUT:
<img width="1098" height="633" alt="image" src="https://github.com/user-attachments/assets/ebbec92d-29b6-44e3-98d0-4383912cd930" />


```
 np.sqrt(df["Highly Positive Skew"])
```

# OUTPUT:
<img width="673" height="625" alt="image" src="https://github.com/user-attachments/assets/d7baca7a-3723-4512-829c-a291bce70113" />


```
 np.square(df["Highly Positive Skew"])
```

# OUTPUT:
<img width="953" height="626" alt="image" src="https://github.com/user-attachments/assets/6a2426d6-f25b-4592-a77a-e4ca6651f559" />


```
 df["Highly Positive Skew_boxcox"], parameters=stats.boxcox(df["Highly Positive Skew"])
 df
```

# OUTPUT:
<img width="1571" height="611" alt="image" src="https://github.com/user-attachments/assets/50115fdb-1863-4de8-9c5c-4e9160ef70c0" />


```
 df.skew()
```

# OUTPUT:
<img width="854" height="356" alt="image" src="https://github.com/user-attachments/assets/9b297f4e-ddbf-49b3-be76-cc56f72aacfb" />


```
  df["Highly Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Highly Negative Skew"])
  df.skew()
```

# OUTPUT:
<img width="1262" height="415" alt="image" src="https://github.com/user-attachments/assets/bf1af561-4a0e-408d-addc-8804c93874bd" />


```
 from sklearn.preprocessing import QuantileTransformer
 qt=QuantileTransformer(output_distribution='normal')
 df["Moderate Negative Skew_1"]=qt.fit_transform(df[["Moderate Negative Skew"]])
 df
```

# OUTPUT:
<img width="1743" height="677" alt="image" src="https://github.com/user-attachments/assets/3d5d267f-2a72-435a-9d61-c3c7845ef19d" />


```
  import seaborn as sns
  import statsmodels.api as sm # STATS MODEL- STATISTICAL MODEL TO VISUALIZE DISTRIBUTION
  import matplotlib.pyplot as plt
  sm.qqplot(df["Moderate Negative Skew"],line='45') # QQ - QUANTILE QUANTILE PLOT
  plt.show()
```

# OUTPUT:
<img width="1276" height="705" alt="image" src="https://github.com/user-attachments/assets/a82fa208-d1c5-4804-8381-38b71e06308f" />


```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45') # RECIPROCAL
plt.show()
```

# OUTPUT:
<img width="1059" height="637" alt="image" src="https://github.com/user-attachments/assets/18487fba-9cb4-4964-a6f8-431e4c4c0a89" />


```
 from sklearn.preprocessing import QuantileTransformer
 qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
 df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])
 sm.qqplot(df["Moderate Negative Skew"],line='45')
 plt.show()
```

# OUTPUT:
<img width="1235" height="708" alt="image" src="https://github.com/user-attachments/assets/721f3346-883a-4099-810b-2490f4697fd1" />

# RESULT:
Thus,the program is executed successfully.

       
