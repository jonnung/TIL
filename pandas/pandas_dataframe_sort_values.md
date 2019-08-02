
## 축(axis)를 기준으로 DataFrame 정렬하기


```python
import pandas as pd
import numpy as np
```

### 샘플 데이터


```python
df = pd.DataFrame({
    'col1': ['A', 'A', 'B', np.nan, 'C'],
    'col2': [2, 1, 9, 8, 5],
    'col3': [0, 1, 9, 5, 2]
})
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>B</td>
      <td>9</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>8</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>C</td>
      <td>5</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



### ▶︎ 정렬 기준이 되는 열 또는 행 값을 지정해서 정렬
`by` 인자는 `str` 또는 `list(str)` 형태가 될 수 있다.  
`axis` 인자의 값에 따라 기준이 *열(column)* 이 되거나, *행(row)* 이 될 수 있다.


```python
df.sort_values(by=['col1'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>B</td>
      <td>9</td>
      <td>9</td>
    </tr>
    <tr>
      <th>4</th>
      <td>C</td>
      <td>5</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>8</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>


