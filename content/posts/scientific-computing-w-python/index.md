---
title: Python库中一些与科学计算相关的方法
date: 2014-02-10T14:45:17+08:00
categories:
- Python
tags:
- python
- numpy
---

```python
numpy.zeros(shape, dtype=float, order='C')
```
返回1个给定形状和类型的新数组，并用`0`填充；
<!-- more -->
```python
random.random()
```
返回在`[0.0, 1.0)`范围内的下一个随机浮点数；

```python
random.uniform(a, b)
```
返回1个随机浮点数，满足条件`a <= N <= b`（当`a <= b`时）；

```python
random.sample(population, k)
```
返回从序列`population`中1个长度为`k`的取样，序列`population`中的元素不必是不同的值；

```python
numpy.random.randint(low, high=None, size=None)
```
返回1个在`[low, high)`范围内满足离散型均匀分布的随机整数，如果`high`是`None`（默认），结果就在`[0, low)`范围内；

```python
numpy.random.normal(loc=0.0, scale=1.0, size=None)
```
返回1个从正态（高斯）分布中抽样的数组；

```python
numpy.array(object, dtype=None, copy=True, order=None, subok=False, ndmin=0)
```
创建1个数组；

```python
numpy.nonzero(a)
```
返回1个数组的元组，元组的元素数是`a`的维度数，每个元素是所有非0元素在该维度上的索引组成的数组；

```python
numpy.where(condition[, x, y])
```
如果没有给出参数`x`和`y`，返回`condition.nonzero()`，即`condition`是`True`的索引的数组；

如果给出参数`x`和`y`（`x`、`y`中元素的数量必须与`condition`中元素的数量一致），返回一个由`condition`中对应位置元素是`True`还是`False`来决定从`x`还是`y`中取值的结果组成的数组；

```python
numpy.cumsum(a, axis=None, dtype=None, out=None)
```
计算数组元素沿1个特定的轴的累和；

```python
numpy.mean(a, axis=None, dtype=None, out=None)
```
计算数组元素沿1个特定的轴的算术平均值；

```python
numpy.linalg.norm(x, ord=None, axis=None)
```
计算矩阵或向量的范数。如果`x`是矩阵，根据不同的参数`ord`，可以返回7个矩阵范数中的1个；

如果`x`是向量，可以返回无限个向量范数中的1个。
