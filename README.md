# Indented <--> Associative
Analysis of various ways to represent multilevel indented data

## Abstract
There are several common ways to represent hierarchical data:
* As indented text:
```
animals
	dog
	cat
fruits
	spherical
		orange
	other
		banana
leaf

```
* As an associative array:
```
'dog' => 'apple',
'cat' => array(
	'fruit' => 'banana',
	'third-level' => array(
		'red' => 'blue',
		'green' => 'red',
	),
	1 => 'hello',
)
```

