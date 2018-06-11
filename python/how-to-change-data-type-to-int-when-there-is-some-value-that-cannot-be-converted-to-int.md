## How to change data type to int when there is some value that cannot be converted to int

I'm trying to do

```python
df['column'] = df['column'].astype(int)
```

but I got
```
ValueError: invalid literal for long() with base 10: ''
```

I found out there were some values, which cannot be converted to int. And the solution I found was
```python
# pd is Pandas
df['Num_Detections'] = pd.to_numeric(df['Num_Detections'], errors='coerce')
```
