# 关于tensor的一些操作

## 1 tf.random.shuffle 打乱 洗牌

```python
a = tf.range(10)
tf.random.shuffle(a)
# <tf.Tensor: shape=(10,), dtype=int32, numpy=array([7, 0, 3, 9, 4, 2, 1, 5, 6, 8])>
```

## 2 tf.gather

打散idx，利用打散后的idx tf.gather 索引x,y，达到打散x,y 而不改变原有的对应关系

```python
x = tf.range(10)
y = tf.range(10)
idx = tf.range(x.shape[0])
idx = tf.random.shuffle(idx)
x = tf.gather(a, idx)
y = tf.gather(b, idx)
x, y
# (<tf.Tensor: shape=(10,), dtype=int32, numpy=array([5, 6, 9, 3, 7, 0, 1, 2, 8, 4])>,
#  <tf.Tensor: shape=(10,), dtype=int32, numpy=array([5, 6, 9, 3, 7, 0, 1, 2, 8, 4])>)
```
