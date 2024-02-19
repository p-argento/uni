
1. Use Modules and Packages
	1. what makes a folder a package is the `__init__.py` file inside it
		1. in this file, the functions from the modules can be imported with `from .<module_name> import <function_name>` 
		2. then, in the main just import 
	2. use `import <module_name>` to import all the code of a module
		1. if there are functions or classes, they can be used with `<module_name>.<function_name>`
		2. everything else will be run
	3. use `from <package_name> import <module_name>`

2. (controversial) Place a single class in a single file.
	1. use PascalCase for ClassNames
	2. use snake_case for file_names

3. Group Related Functionalities together
	1. for example, divide code in
		1. api
		2. docs
		3. tests
		4. utils

4. Place Utilities in a single place (file or package)
	1. don't know where to put them, random helper functions
	2. dump all non-related function in a non-related file

5. organize imports (suggestion)
	1. he suggests this order
		1. third-party
		2. built-ins
		3. my modules
	2. PEP8 suggests
		1. standard library imports
		2. related third party imports
		3. local application/library specific imports .

 5 Tips To Organize Python Code - YouTube
https://www.youtube.com/watch?v=e9yMYdnSlUA



# Modules


(18) Why `__init__.py` File is Used in Python Projects | 2MinutesPy - YouTube
https://www.youtube.com/watch?v=mWaMSGwiSB0

Transcript:
(00:05) Hey folks, welcome to 2MinutesPy. Today, we're unraveling the mystery of init.py in Python, a little file that does big things. Let's get straight to it without any tech jargon. What is init.py? Let's say you have a directory with a bunch of Python files and you want to treat it as a package. Just drop an init.py file inside and boom.
(00:26) Python recognizes that directory as a package. It's like a secret handshake between your code and Python. Now, what's inside this init.py file? It can be as simple as an empty file or you can include some initialization code if you have special setup needs, but most of the time an empty init.py is just fine.
(00:45) Think of init.py as the package's way of saying "I'm ready to be used". When someone else wants to use your package, they import it in their code and Python knows to look for that magical init.py. Without init.py. Python wouldn't recognize your directory as a package and you wouldn't be able to import modules from it using the standard "import" statement.
(01:08) How does init.py help in creating packages? init.py allows you to organize your code into modular chunks, making it easier to manage and reuse. Think of it as a blueprint for your package, you can define common functions, variables or even import other modules within init.py, setting up the foundation for your packages functionality.
(01:32) Let's create a simple package called my_package to illustrate how init.py works inside the my_package directory. Create an empty file called __init__.py. Now create another file called greetings.py and write a function called say_hello() that prints "Hello, World!". Now from any file outside the my_package directory, you can import the greetings module and use the say_hello() function.
(02:04) This will print "Hello, World!" because init.py makes the greetings module accessible from within the my_package namespace init.py is a fundamental building block for creating structured and organized Python packages. It's like the invisible glue that holds your code together, making it easier to manage reuse and share.
(02:29) So in simple terms init.py is like the starting line for your Python project. Thanks for tuning in. That's all for now. And as always, Keep Coding.
