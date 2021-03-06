# Read and write

## Read text file

Get a single `str`.
```python
with open(path) as f_in:
    text = f_in.read()
```

Get a `list` of `str` objects.

```python
with open(path) as f_in:
    text = f_in.read()
    lines = text.splitlines()
```

Note `list.splitlines` will remove newlines by default and something similar could be achived with `list.split("\n")`

Use `f.seek(0)` to reset if you need to read the entire file multiple times.

Read line by line. This is more memory efficient.

```python
with open(path) as f_in:
    for line in f_in:
        print(line)
```

## Write text file

```python
with open(path, 'w') as f_out:
    f_out.write('foo\n')
    f_out.write('bar\n')
```

```python
my_list = ["foo", "bar"]
with open(path, 'w') as f_out:
    f_out.writelines(my_list)
```

Example path values:

- `text.txt`
- `foo/bar.txt`
- An absolute path


## Write JSON file

```python
with open(path, 'w') as f_out:
    json.dump(data, f_out)
```

## Write CSV file

```python
header = ["Foo", "Bar"]
rows = [["foo", "bar"], ["fizz", "buzz"]]
with open(path, 'w') as f_out:
    writer = csv.writer(f_out)
    write.writerow(header)
    write.writerows(rows)
```


```python
header = ["Foo", "Bar"]
rows = [
    {"Foo": "a", "Bar" 1},
    {"Foo": "b", "Bar": 2}
}
with open(path, 'w') as f_out:
    writer = csv.DictWriter(f_out, fieldnames=header)
    write.writeheader()
    write.writerows(rows)
```
