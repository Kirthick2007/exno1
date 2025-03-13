# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
import pandas as pd
exp=pd.read_csv("/content/SAMPLEIDS.csv")
exp
```
![image](https://github.com/user-attachments/assets/6a45caaf-89bf-43e2-9429-8757d957ca11)
```
exp.isnull().sum()
```
![image](https://github.com/user-attachments/assets/e92266a3-6ab2-42a2-8ebb-e2f17984e78c)
```
exp.isnull().any()
```
![image](https://github.com/user-attachments/assets/35674a13-2e23-4330-9f59-235a7aff6bbf)
```
exp.dropna()
```
![image](https://github.com/user-attachments/assets/64b50042-1b6c-4b00-94ea-35513678991b)
```
exp.fillna(0)
```
![image](https://github.com/user-attachments/assets/db1ef3e8-bd30-4b19-a711-778f99481363)
```
exp.fillna(method="ffill")
```
![image](https://github.com/user-attachments/assets/cea4e9cf-6336-4f62-8589-a86159d51c14)
```
exp.fillna(method="bfill")
```
![image](https://github.com/user-attachments/assets/406f10fc-d4d3-4ce4-9d3d-aa4f29bc9ce1)
```
exp_dropped=exp.dropna()
exp_dropped
```
![image](https://github.com/user-attachments/assets/0937088c-9a5c-4684-b8fe-a91e320cdd07)
```
exp.fillna({'NAME':'MOHAN','GENDER':'MALE','ADDRESS':'THIRUVOTTIYUR','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![image](https://github.com/user-attachments/assets/1eabfd91-316e-434a-8365-e39c37e91d01)

# IQR(Inter Quartile Range)
```
import pandas as pd
ir=pd.read_csv("/content/iris.csv")
ir
```
![image](https://github.com/user-attachments/assets/3dde0b40-79b9-4a84-9257-8222815c8288)
```
ir.describe()
```

![image](https://github.com/user-attachments/assets/7828e348-1feb-4bb7-96aa-5107bc9be6b9)
```
import seaborn as sns
sns.boxplot(x='sepal_width',data=ir)
```
![image](https://github.com/user-attachments/assets/3b7cc419-c8e9-4a20-adad-1aa71b439125)
```
q1=ir.sepal_width.quantile(0.25)
q3=ir.sepal_width.quantile(0.75)
iqr=q3-q1
print(iqr)
```
![image](https://github.com/user-attachments/assets/d01b412e-3d2b-4c33-b210-39cc7c130fb2)
```
outlier=ir[((ir.sepal_width<(q1-1.5*iqr))|(ir.sepal_width>(q3+1.5*iqr)))]
outlier['sepal_width']
```
![image](https://github.com/user-attachments/assets/490a0207-63a6-418d-8fd9-e5f7eff1f992)
```
o=ir[~((ir.sepal_width<(q1-1.5*iqr))|(ir.sepal_width>(q3+1.5*iqr)))]
print(o)
```
![image](https://github.com/user-attachments/assets/91ecbab0-0115-4f97-9f76-f4b2f8224ed2)
```
sns.boxplot(x='sepal_width',data=o)
```
![image](https://github.com/user-attachments/assets/8edaf76d-82ca-4818-b0a5-c75c6d5f4d4f)
# Z-Score
```

import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
data_set=pd.read_csv("/content/heights.csv")
data_set
```

![image](https://github.com/user-attachments/assets/33060559-fa13-41b7-ad77-c0d1617725b1)
```
z=pd.read_csv("/content/heights.csv")
q1=z['height'].quantile(0.25)
q2=z['height'].quantile(0.50)
q3=z['height'].quantile(0.75)
iqr=q3-q1
print(iqr)
```

![image](https://github.com/user-attachments/assets/c456ffbd-fd97-4bbe-b539-8e87b98a338e)
```
low = q1-1.5*iqr
print(low)
```


![image](https://github.com/user-attachments/assets/c80261f1-4826-4cf1-91bd-d821f5a73aae)
```
high = q3+1.5*iqr
print(high)
```

![image](https://github.com/user-attachments/assets/da52f71b-8dc0-4c9f-86dc-6cccf2e8ee7b)
```
z1=z[((z['height']>=low)&(z['height']<=high))]
z1
```

![image](https://github.com/user-attachments/assets/48c4836c-9ed5-4c51-bc38-24092eb18355)
```
z=np.abs(stats.zscore(z['height']))
z
```

![image](https://github.com/user-attachments/assets/20c09da2-5f38-4d72-9977-e0bef6042675)
```
z1=z[z<3]
z1
```

![image](https://github.com/user-attachments/assets/32123761-9a0f-4d8b-82e7-77af96513024)



# Result
        Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
