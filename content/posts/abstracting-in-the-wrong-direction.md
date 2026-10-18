+++
title = "Abstracting in the wrong direction"
date = 2026-06-12
extra.katex = false
extra.toc = true
[taxonomies]
tags = ["programming"]
+++

I'm tired of endless OOP and inheritance-based frameworks.
All I want is just some simple form of language with basic *Algebraic Data Type (ADT)* and simple *functions* with fine *generics*.
If possible, the language should also be equiped with *Typeclass*.

Most OOP based languages, for example Python and Java, like to build softwares from classes and inheritance which I found is quite complex and confusing. In most of development situations, one don't need complete subtyping and inheritance. For example, people like to use the example of animals to demonstrate the OOP way of abstraction:

```python
class Animal:
    def sound(self):
        print("Animal sound")

@dataclass
class Dog(Animal):
    color: str
    age: int

    def sound(self):
        print("Bark")

d = Dog()
d.sound()

def some_logic(x: Animal):
    s.sound()
```

In the above code, data and behavior are tightly packed together.
For instance, one can see that the behavior `sound` depends on the actual implementation or overriding of `Animal.sound`. It seems that this kind of code is fine, but when it comes to adding or mixing more behaviors, it quickly becomes chaotic. Now suppose the animal can run, drink water and eat food, we have to extend our `Animal` class and implement this method for every subclass.

What about we want to make `Dog` serializable? How about implementing `Read` or even more interfaces?
You may argue that we can just add more superclasses but it's quite messy! Every time you add one more inheritance relation, you're making your code harder to refactor. The author the class `Dog` should not care any other behaviors be used later. Instead, the author should only focus on the data and basic aspects of dogs. It's the later user who want extend dog to some other interfaces to make it compatible to other APIs.

## Just functions
To get better abstraction of our `Dog`, one can just write:
```python
# in module 'dog.py'

@dataclass
class Dog:
    color: str
    age: int

def bark(d: Dog):
    print("Bark!")
```

No animals, no methods, and no inheritance.
When you want to write more logics on `Dog`, just **def** new functions by composing existing functions.
If, finally, you need to build polymorphism on this `Dog`, you can write:
```python
class Sounding(Protocol):
    def sound(self) -> None: ...

def logic_on_sound(d: Sounding):
    d.sound()
```

How about more behaviors?
```python
class Encode(Protocol):
    def encode(self) -> str: ...

@dataclass
class MyDog:
    inner: Dog

    def sound(self):
        dog.bark(self.inner)

    def encode(self) -> str:
        return repr(self.inner)
```

You just pack behaviors and data together with no subtyping at all!
You can even completely separate data and behaviors as different arguments on function input like
```python
def encode_me[A](a: A, encoder: Encode[A]):
    encoder.encode(a)
```

Therefore, you can just build any kinds of abstraction you want by utilizing plain functions and data.
As a final example:

```python
# only composition alias
class Animal(Sounding, Encode, Protocol):
    pass

def logics(a: Animal) -> str:
    a.sound()
    s = a.encode()
    return s

d = MyDog(Dog(color='dark', age=1))
logics(d)
```


### Default behaviors
Sometimes, one want to have default implementation of protocol behaviors:
```python
class Iterator[T](Protocol):
    def next(self) -> Optional[T]: ...

    def skip_one(self) -> Optional[T]:
        self.next()
        return self.next()
```

However, how do we implement these default methods like `skip_one`?
Should we fall back to inheritance again?

No! We can just use simple functions
```python
class Iterator[T](Protocol):
    def next(self) -> Optional[T]: ...

def skip_one(it: Iterator) -> Optional[T]:
    it.next()
    return it.next()
```

