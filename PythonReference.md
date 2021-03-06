# Python Reference



### Numpy

##### 针对不同的列应用多种不同的统计方法

```python
In [15]: df.groupby('A').agg({'B':[np.mean, 'sum'], 'C':['count',np.std]})

Out[15]: 
          B         C          
       mean sum count       std
A                              
X  2.250000   9     4  3.403430
Y  2.000000   6     3  1.000000
Z  1.333333   4     3  2.081666
```

### Pandas

##### Join 两个 Dataframe 但是列名不同

```python
pd.merge(frame_1, frame_2, left_on='county_ID', right_on='countyid')
```



#### 参考

[Pandas 100 题](https://blog.csdn.net/AvalancheM/article/details/81293149)

[Pandas Exercises](https://github.com/guipsamora/pandas_exercises)



### Sklearn

##### 模型评价Metrics

from sklearn.metrics import 评价指标函数名称 

### Seaborn

##### 数据分布

```python
sns.distplot(df['Pressure'], color="g", bins=len(set(floor)), rug=True)
```

##### 控制 Figure 大小

```python
plt.figure(figsize=(col,row))
## sns.plot ...
plt.show()
```



### Json

python 对象 -> json 对象

`json.loads()`

json 对象 -> python 对象

`json.dumps()`