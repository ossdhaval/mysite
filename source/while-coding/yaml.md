# YAML

YAML: YAML Ain't Markup Language

What It Is:
  YAML is a human-friendly data serialization
  language for all programming languages.

- How is it different from json? Json has elements like `{` and `]` to define elements. This adds additional elements that makes JSON harder to read and understand by humans.
- Yaml replaces additional structural elements with spaces. Spaces are really important in yaml.
- Yaml has following constructs.

## Key value pairs:

```
key:<space>value
```
neither key nor value need to be in quotes. Value should be in double quotes only if there is a special character in it. A space is **not** a special character.



## Arrays

Arrays just have values and sequence is maintained at retrieval

Spacing is not important as long as same spacing is maintained throughout the file.

```
american:
  - Boston Red Sox
  - Detroit Tigers
  - New York Yankees
national:
  - New York Mets
  - Chicago Cubs
  - Atlanta Braves
```

## maps

maps/dictionaries have key and values. But sequence is not important.

Spacing is not important as long as same spacing is maintained throughout the file.

```
burger:
  calories: 12
  price: 15
```

you can mix arrays and maps.

```
drinks:
  - milk:
      calories: 4
      price: 3
  - water:
      calories: 0
      price: 0
```
  


```

