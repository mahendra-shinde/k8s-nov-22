# Comment

1. Basic YAML file with built in types:

	```yaml
	# String type value
	name: Mahendra Shinde
	# Numeric type
	number: 100
	# Boolean value
	isAlive: true 
	isActive: yes
	# Number interpreted as String
	contact: '25765635763'
	```

1. List type values


	```yaml
	# Using indents
	languages:
	  - Java
	  - C#
	  - JavaScript
	```

	```yaml
	# Not Using indents
	languages:
	- Java
	- C#
	- JavaScript
	```

1.	Map / Dictionary Type

	```yaml
	person: 
	  firstName: Mahendra
	  lastName: Shinde
	```

1.	Complex Type (Mix of List/Map and Strings)

	```yaml
	team:
	- firstName: mahendra
	  lastName: shinde
	- firstName: Rajiv
	  lastName: Bhatia
	```

	> team[0].firstName = Mahendra

NOTE:	
1. File extension could be either .yaml or .yml
1. YAML uses "spaces" for indent, do not use "TAB"
1. Smart Text Editors like VSCode can "Convert" Tab into spaces.	