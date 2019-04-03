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

## Possible Array Representations
1: everything is stored as keys, and everything has a child array. this method is susceptible to key overwriting if the source data has duplicate entries at the same level
	array(
		'basic' => array(),
		'animals' => array(
			'dogs' => array(),
			'cats' => array(),
		),
		'fruits' => array(
			'spherical' => array(
				'oranges' => array(),
			),
			'other' => array(
				'bananas' => array(),
			),
		),
		'nothing' => array(),
	)
2: nodes with children are stored as keys, leaf nodes are stored as elements. this method is susceptible to key overwriting if numbers are involved - not a good solution
	array(
		0 => 'basic',
		'animals' => array(
			0 => 'dogs',
			1 => 'cats',
		),
		'fruits' => array(
			'spherical' => array(
				0 => 'oranges',
			),
			'other' => array(
				0 => 'bananas',
			),
		),
		1 => 'nothing',
	)
3: everything is stored as elements (values). all nodes are arrays. leaves have no 'children' array row. this is the most verbose and most foolproof
	a node with one leaf looks like this:
		0 => array(
			'value' => 'fruit',
		),
	a grandparent node looks like this:
		0 => array(
			'value' => 'fruit',
			'children' => array(
				0 => 'banana',
				1 => 'apple',
			),
		),
4: everything is stored as elements (values). leaves are stored more simply than parent nodes. this is the second most verbose method
	a node with one leaf looks like this:
		0 => 'fruit',
	a grandparent node looks like this:
		0 => array(
			'value' => 'fruit',
			'children' => array(
				0 => 'banana',
				1 => 'apple',
			),
		),
	a full example looks like this:
		array(
			0 => 'basic',
			1 => array(
				'value' => 'animals',
				'children' => array(
					0 => 'dogs',
					1 => 'cats',
				),
			),
			2 => array(
				'value' => 'fruits',
				'children' => array(
					0 => array(
						'value' => 'spherical'
						'children' => array(
							0 => 'oranges',
						),
					),
					1 => array(
						'value' => 'other',
						'children' => array(
							0 => 'bananas',
						),
					),
				),
			),
			3 => 'nothing',
		)
