# 常用公式

## 1. tf.keras.losses.mse 均方差

$MSE=\frac{1}{N}\sum(\hat{y_i}-y_i)^2$  

```python
out = tf.random.uniform([4, 2])
y = tf.range(4)
y = tf.one_hot(y, depth=2)
loss = tf.keras.losses.mse(y, out)
out, y, loss
# (<tf.Tensor: shape=(4, 2), dtype=float32, numpy=
#  array([[0.5126084 , 0.81131065],
#         [0.02727783, 0.8493366 ],
#         [0.8134357 , 0.6964725 ],
#         [0.10443616, 0.40264058]], dtype=float32)>,
#  <tf.Tensor: shape=(4, 2), dtype=float32, numpy=
#  array([[1., 0.],
#         [0., 1.],
#         [0., 0.],
#         [0., 0.]], dtype=float32)>,
#  <tf.Tensor: shape=(4,), dtype=float32, numpy=array([0.44788775, 0.01172177, 0.5733758 , 0.08651317], dtype=float32)>)
```

## 2. tf.reduce_mean 平均

$mean=\frac{1}{N}\sum\limits_{i=1}^{n} x_i$  

```python
a = tf.range(5)
a, tf.reduce_mean(a)
# (<tf.Tensor: shape=(5,), dtype=int32, numpy=array([0, 1, 2, 3, 4])>,
#  <tf.Tensor: shape=(), dtype=int32, numpy=2>)
```
