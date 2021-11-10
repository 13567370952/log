
## 21-11-10
### str转datetime.date
```python
   t = '2021-11-10'
   year, month, day = time.strptime(t, "%Y-%m-%d")[:3]
   t1 = datetime.date(year, month, day)
   print(t1)

##  2021-11-10

```
