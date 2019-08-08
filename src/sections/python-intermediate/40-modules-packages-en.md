# Modules and packages

## Modules and packages

- Module = Python file from which objects can be imported
- Package = directory that includes Python modules

## Example imports

- `urllib` = package
- `urllib.request` = module
- `urllib.request.urlopen` = function

<!-- list separator -->

- `sys` = module
- `sys.path` = object

## Example imports

Typical imports:

```py
import module1
import module2
from package3 import module3a, module3b
from module4 import object4a, object4b
from package5.module5 import object5a, object5b
```

Specific examples:

```py
import os
import sys
from urllib import request, response
from math import sqrt, pi
from http.client import HTTPConnection, HTTPSConnection
```

## Shorter names for imports

Typically used in an interactive console to save keystrokes:

Short names:

```py
import numpy as np
import matplotlib.pyplot as plt
import tkinter as tk
```

Importing everything from a module (usually not recommended):

```py
from math import *
```

## Conventions for imports

- all imports in a Python file _should_ be at the start of the file
- imports _should_ be split into three groups:
  - imports from the standard library
  - imports from other libraries
  - imports within the project

## Resolving imports

Search order:

- directory of the Python script that was executed
- standard library
- external libraries

Avoid name clashes with existing modules / packages!

## Resolving imports

To see all search paths for imports:

```py
import sys
print(sys.path)
```

## Compilation of modules

Imported modules will be saved in a compiled form, making subsequent loading of the modules faster.

Compiled versions will be saved in the folder `__pycache__`

## Be careful: avoid circular imports