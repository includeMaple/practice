# 题

## 题目

```python
def w1():
  print('one')
  def inner():
    print('two')
  return inner()

w1()
```

## 答案

注意：不要看着像就想当然以为这是返回一个函数的引用，这里return的时候直接调用了

答案：

```
one
two
```
