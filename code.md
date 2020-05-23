### Preparation

Import some libraries.

```python
import numpy as np
import matplotlib.pyplot as plt
```

### Lagrange Function

```python
#Lagrange Interpolation

def lagrange(x,y,order):

  y_interpolate = []
  Denum= []
  Num = []

  def search_data(x_i, x, order):
    pseudo_vector = x_i - x
    for i in range(np.size(x)):
      if np.sign(pseudo_vector[i]) != np.sign(pseudo_vector[i+1]):
        return np.array(x[i:i+order+1]), i

  def Numerator(x_i, i):
    return np.prod(x_i - np.delete(dummy_vector_x, i))

  def Denumerator(i):
    return np.prod(dummy_vector_x[i] - np.delete(dummy_vector_x, i))

  for i in range (np.size(x_interpolate)):
    simpan = 0
    dummy_vector_x, index = search_data(x_interpolate[i], x, order)
    dummy_vector_y = y[index:index+order+1]
    for j in range (np.size(dummy_vector_x)):
      simpan = simpan + y[index+j] * Numerator(x_interpolate[i], j) / Denumerator(j)
    y_interpolate.append(simpan)

  return y_interpolate
```

### Test the Function

Initialize the data.

```python
x = np.array([0, 0.560, 0.805, 1.01, 1.16, 1.36, 1.50, 1.66, 1.88])
y = np.array([0, 10, 60, 30, 40, 30, 60, 70, 80])

plt.scatter(x,y)
plt.xlabel('x')
plt.ylabel('y')
plt.savefig('scatterInterpol.png')
```
Here is the data

![Data](https://github.com/Prakhosha/Lagrange-Interpolation/blob/master/demo1.png)

Let's interpolate the data with second order lagrange.

```python
y_interpolate = lagrange(x,y,2) # order value

plt.figure(1)
plt.plot(x_interpolate, y_interpolate, label='Interpolasi')
plt.plot(x, y, 'o', label='Data')
plt.xlabel('x')
plt.ylabel('y')
plt.legend()

plt.savefig('Lagrange2.png')
```

Here what its looks like.

![Interpolated Data](https://github.com/Prakhosha/Lagrange-Interpolation/blob/master/demo2.png)
