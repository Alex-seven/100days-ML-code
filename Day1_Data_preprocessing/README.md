# Data Preprocessing
![](https://github.com/LiuChuang0059/100days-ML-code/blob/master/Day1_Data_preprocessing/Day%201.jpg)


## Step 1: Importing the libraries
* [numpy]() :  包含 数学函数
* [pandas]():  导入和管理 数据集

```python
import numpy as np
import pandas as pd
```

## Step 2: Importing dataset

* 数据集通常在.csv 文件中
* csv文件储存 表格式数据
* 用 pandas 库里面的read_csv 读取本地csv文件 作为 [数据桢（dataframe）](http://wiki.jikexueyuan.com/project/start-learning-python/311.html)
* 从数据帧中创建独立的矩阵和独立变量和因变量

```python
dataset = pd.read_csv('Data.csv')
X = dataset.iloc[ : , :-1].values   ## 选取前三列
Y = dataset.iloc[ : , 3].values     ## 选取最后一列    返回值的类型仍为 dataframe
```
ps : [iloc 选取特定的列](https://blog.csdn.net/chenKFKevin/article/details/62049060)
![](https://github.com/LiuChuang0059/100days-ML-code/blob/master/Day1_Data_preprocessing/%E6%95%B0%E6%8D%AE.png)


## Step 3: Handling the missing data
* 为了不影响机器学习模型效果，需要处理缺失的数据
* 使用整列的中位数或者平均值表示缺失值
* 使用[sklearn.preprocessing 中的 Imputer类](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.Imputer.html)

```python
from sklearn.preprocessing import Imputer
imputer = Imputer(missing_values = "NaN", strategy = "mean", axis = 0)
imputer = imputer.fit(X[ : , 1:3])
X[ : , 1:3] = imputer.transform(X[ : , 1:3])
```

## Step 4: Encoding categorical data
* 分类数据：有标签值 而不是数字值
* 分类数据具有有限的可能值
* 编码这些变量 为数字
* 需要sklearn.preprocessing 中的 LabelEncoder类, OneHotEncoder

```python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder_X = LabelEncoder()
X[ : , 0] = labelencoder_X.fit_transform(X[ : , 0])

onehotencoder = OneHotEncoder(categorical_features = [0])
X = onehotencoder.fit_transform(X).toarray()
labelencoder_Y = LabelEncoder()
Y =  labelencoder_Y.fit_transform(Y)
```

## Step 5: Splitting the datasets into training sets and Test sets

* 数据集分成训练集和测试集
* 分的比例通常 8:2
* 使用sklearn.cross_validation 中 train_test_split 类

```python
from sklearn.cross_validation import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split( X , Y , test_size = 0.2, random_state = 0)
```
## Step 6: Feature Scaling---特征缩放
* 使用欧几里得距离
* 特征与 标度有关
* 使用标准特征标度

```python
from sklearn.preprocessing import StandardScaler
sc_X = StandardScaler()
X_train = sc_X.fit_transform(X_train)
X_test = sc_X.fit_transform(X_test)

```











