# Class Development Toolkit

Notes from talk by Raymond Hettinger about python class architecture

http://pyvideo.org/video/1779/pythons-class-development-toolkit


Product class:
```circle.py
# circle.py
import math

class Circle(object):
    """An advanced circle analytic toolkit"""

    version = '0.1' # class variable, always use strings or integers for versions

    def __init__(self, radius):
        self.radius = radius

    def area(self):
        'Perform quadrature on a shape of uniform radius'
        return math.pi * self.radius ** 2.0

    def perimeter(self):
        return 2.0 * math.pi * self.radius

    @classmethod # alternative constructor
    def from_bbd(cls, bbd):
        'Construct a circle from a bounding box diagonal'
        radius = bbd / 2.0 / math.sqrt(2.0)
        return cls(radius)   # calls clc => so the function works for subclasses

```

Customer usage:
```tire.py
# tire.py
class Tire(Circle):
    'Tires are circles with a corrected perimeter'

    def perimeter(self):
        'Circumfrence corrected for the rubber'
        return Circle.perimeter(self) * 1.25
```


Protect parent object methods from being overwritten.
``` circle.py
# circle.py
...
    def area(self):
        p = self.__perimeter()
    ...

    # when invoked, this will results as: _Klass_perimeter, protects original
    # on being overwritten
    __perimeter = perimeter

```


Getters and setters in python:
``` circle.py
# circle.py

    @property # converts dotted access to method calls
    def radius(self):
        'Radius of a circle'
        return self.diameter / 2.0

    @radius.setter
    def radius(self, radius):
        self.diameter = radius * 2.0

```


When scaling to avoid new isntances object (saves tons of memory):
DO THIS LAST

```
class Circle(object):

    # flyweight design pattern suppresses the instance dictionary
    #   removes ability to add own attributes on this class.

    __slots__ = ['diameter']  # does not inherit on to subclasses
    ...
```
