# Core.Today Python Style Guide

## 프로젝트 구성
뼈대는 다음의 가이드라인을 따릅니다
- [Structure](https://python-guide-kr.readthedocs.io/ko/latest/writing/structure.html)
- [Skeleton](https://github.com/navdeep-G/samplemod)


## 기본 원칙
1. 하나의 함수는 하나의 일만 하도록 한다
2. 밑줄이 앞에 붙은 함수 이름은 패키지 내부에서만 사용되는 함수이다
3. 메인 코드가 실행되기 전에 의존성 버전 차이를 처리한다
4. Spinx 자동 문서화 확장을 사용한다
5. Autoformatter로 [`black`](https://github.com/CoreDotToday/styleguide/issues/2)을 사용한다
6. 환경변수는 `.env` 파일에 저장하고, 라이브러리 [`environs`](https://github.com/sloria/environs) 로 불러온다
7. [PEP8](https://www.python.org/dev/peps/pep-0008/)을 준수한다


## 환경
1. Python 3.6 이상을 사용한다
2. 마이너 업데이트가 있을 시 첫 패치 업데이트 이후 사용한다
   * 예) 3.9 버전은 3.9.1 이후로 사용
3. `import` 목록을 정리할 때는 [isort](https://github.com/PyCQA/isort)를 사용한다
   - `black`과 [호환되지 않으므로](https://pysanity.netlify.app/#auto-formatters) `isort`를 먼저 실행하고 `black`을 사용하는 것이 낫다



## 독스트링 (Docstrings)
- Numpy 스타일 독스트링을 기준으로 한다
  - 가독성을 극대화하기 위해 추가 세로 공간을 사용하는 좋은 형식
  - [Numpy-style.py](https://github.com/CoreDotToday/styleguide/blob/main/python/docstring/Numpy-style.py)
- 예(example)는 REPL 스타일로 제공되어야 한다
```python
"""
Examples
--------
>>> dumb_add(1, 2, 3, 4, 5)
15

Comment explaining the second example

>>> dumb_add(6, 7, 8, 9, 10)
40
"""
```
- 한 줄 독 스트링
```python
def dumb_sub(num1, num0):
    """Subtracting num0 from num1."""
```
- 인라인 주석은 소문자로 시작해야 한다
```python
# going through the student list
for idx, student in enumerate(students_list):
    ...
```
- 클래스를 문서화하는 경우 메서드와 속성을 언급해야 한다
  - 메서드는 함수처럼 문서화되어야 한다
```python
class Dummy(ndarray):
    """
    Dummy classes for demonstration.

    Attributes
    ----------
    attribute_1 : float
        Set up your goal.

    Methods
    -------
    method_1(c=2)
        Runs a self-referential loop n times.
    method_2(n=1.0)
        Prints Nietzsche's n times.
    """
```


## 세부논의

### 코드 레이아웃
- 들여쓰기는 소프트탭(space character)을 이용해 공백 4칸을 사용
- 한 줄은 최대 89자까지 <sup>[[1]](#footnote1)</sup>   
  - 긴 문자열은 경우에 따라 다음과 같이 끊어서 입력한다.
    ```python
    token = (
      "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9."
      + "eyJzdWIiOiJ1YnVudHUiLCJleHAiOjY4NDg3NDI1MDl9."
      + "varo-uXei0kmGkejkfzCtOkWvW6y7ewzaKBj4qZZHWQ"
    )

    headers = {
        "accept": "application/json",
        "Authorization": f"Bearer {token}",
    }
    ```
- 최상위(top-level) 함수와 클래스 정의는 2줄씩 띄어 씀
- 클래스 내의 메서드 정의는 1줄씩 띄어 씀


### Single quote, double quote

- 둘 중 무엇이든 한 프로젝트에선 하나의 스타일로 통일성을 유지하게끔 사용함

* `docstrings`에는 triple double quotes를 사용한다
* `\\` 이스케이프를 피하고자 둘을 잠시 혼용하는 걸 허용한다


### 코멘트
- 코드와 모순되는 주석은 없느니만 못함. 항상 코드에 따라 갱신할 것
- 불필요한 주석은 달지 말 것
- 한 줄 주석은 신중히 달 것

### 명명 규칙
- 변수, 함수, 인스턴스의 이름을 지을 때, 스네이크 케이스(snake_case)를 사용한다
- `import`에도 사용되므로 파일 이름(file name)에도 스네이크 케이스(snake_case)를 사용한다
```python
# don't
import myMod

anOBJEct = {}
thisIsAnObject = {}
def ThisisAFunction():
    ...

# do
import my_mod

anobject = {}
this_is_an_object = {}
def this_is_a_function():
    ...
```
- 일반적으로 모듈 수준에서 정의되는 전역상수(Global constants)는 단어를 구분하는 밑줄과 함께 모두 대문자로 이름을 지정한다
```python
# don't
global_constant = 50

# do
GLOBAL_CONSTANT = 50
```
- 클래스 이름을 지정할 때만 파스칼케이스(PascalCase)를 사용한다
```python
# don't
class exampleDummyFactory():
    # ...

fact = exampleDummyFactory()


# do
class ExampleDummyFactory():
    # ...

fact = ExampleDummyFactory()
```
- 프라이빗 `속성`, `메서드`, `변수` 및 `함수` 앞에는 밑줄을 사용한다
```python
# private methods and attributes demo


class SomeThing:
    """A class for demonstration."""

    def __init__(self):
        # private attribute
        self._private_att = 10

    def _private_method(self):
        """This is a private method."""
        pass

    def method_x(self):
        # using the private attribute
        res_private_att = self._private_att
        # calling the private method
        res_private_method = self._private_method()
```
```python
# private function demo


def _private_function():
    pass


def public_function():
    # calling the private function
    res_private_function = _private_function()
```
- 단일 문자 이름을 사용하지 않는다. 설명적(descriptive)이고 의미있는(meaningful) 이름을 사용한다
  - 함수의 기능 또는 개체의 데이터 유형을 알려주자. object_description 대신에 description_object을 쓴다
```python
# don't
def a():
    # ...


# do
def analogy():
    # ...

# don't - no convention to know what data type it's
df_raw_data = pd.DataFrame(raw_data)
id_dct_num = {"a": 1, "b": 2}

# do - convention to tell data type by the last term
raw_data_df = pd.DataFrame(raw_data)
id_num_dct = {"a": 1, "b": 2}

# don't - meaningless names, lost context
list_1 = ["Jack", "Alice", "Emily"]
# ... many lines of code later
for item in list_1:
    add_person(item)

# do
name_list = ["Jack", "Alice", "Emily"]
# ... many lines of code later
for name in name_list:
    add_person(name)
```
- 이름 지정에 단수 또는 기본 단어를 사용한다
  - 복수를 사용하지 말고 대신 데이터 유형과 함께 단수를 추가한다
```python
# don't
def moves_object(x, y):
    # ...


# do
def move_object(x, y):
    # ...

# don't - inconsistent naming for same data type and usage
teacher = ["Michael"]
students = ["Jack", "Alice", "Emily"]
books = pd.DataFrame({"title": ["lorem", "ipsum"]})

for t in teacher:
    add_human(t)

for student in students:
    add_human(student)

for book in books:
    add_item(book) # wrong; iterate column name instead of book

# do
teacher_list = ["Michael"]
student_list = ["Jack", "Alice", "Emily"]
book_df = pd.DataFrame({"title": ["lorem", "ipsum"]})

for teacher in teacher_list:
    add_human(teacher)

for student in student_list:
    add_human(student)

# naming as df suggests it'll be treated as a dataframe
for idx, book in book_df.iterrow():
    add_item(book)
```

### .gitignore
- 다음 파일을 참고하여 불필요한 파일은 Git에 올리지 말 것   
https://raw.githubusercontent.com/CoreDotToday/styleguide/main/python/.gitignore



## 코딩 지침

### 변수
- 전역 범위(global scope)에서 변경 가능한(mutable) 변수는 피한다
  - `list`, `set`, `dict`은 변경 가능(mutable) 합니다
  - `int`, `float`, `bool`, `str`, `tuple`, `unicode`은 변경불가능(immutable) 합니다
  - Why?
    - 그들은 함수와 클래스 간의 종속성을 숨기고 코드의 다른 부분이 서로 어떻게 관련되어 있는지 확인하기가 정말 어렵습니다. 코드를 성공적으로 실행하기 위해 전역 변수가 어떤 상태여야 하는지 알지 못하기 때문에 사용, 리팩토링 및 테스트가 어렵습니다.
    - 테스트를 병렬로 실행하면 테스트가 전역 상태를 엉망으로 만듭니다.
    - 함수들의 깊은 연결 관계를 디버깅하는 경우 모니터링해야하는 모든 변수를 선택하는 것은 쉽지 않습니다.
    - 그들은 병합 충돌의 형태로 개발자 시간을 낭비하는 경향이 있습니다.

### 함수
- 기본 함수/메서드 인수로 변경 가능한(mutable) 데이터 유형을 피한다
```python
# don't
def make_list(val, lst=[]):
    lst.append(val)
    return lst

make_list(1)
# => [1]
make_list(2)
# => [1, 2], instead of the new init [2]


# do
def make_list(val, lst=None):
    if lst is None:
        lst = []
    lst.append(val)
    return lst

init_list(1)
# >> [1]

init_list(2)
# >> [2]
```
- Robert C. Martin의 [단일 책임 원칙](https://en.wikipedia.org/wiki/Single-responsibility_principle) 은 기능이 단일 책임만 갖도록 권장한다. 즉, 한 가지 일만 수행해야 한다. 이는 리팩토링 가능성(refactorability)을 크게 향상시킨다
  - 기능을 변경해야 하는 이유는 단 하나뿐입니다. 기능을 수행하는 방식이 변경되어야 하는 경우.
  - 함수를 삭제할 수 있는 시기도 명확해 집니다. 다른 곳에서 변경할 때 함수의 단일 책임이 더 이상 필요하지 않음이 분명해지면 간단히 제거하십시오.
```python
# don't
# this function calculates multiple things and print them out at the same time
# ideally these two responsibilities can be split into two functions


def calculate_and_print_stats(list_of_numbers):
    total = sum(list_of_numbers)
    mean = statistics.mean(list_of_numbers)
    median = statistics.median(list_of_numbers)
    mode = statistics.mode(list_of_numbers)

    print("-----------------Stats-----------------")
    print(f"SUM: {total}")
    print(f"MEAN: {mean}")
    print(f"MEDIAN: {median}")
    print(f"MODE: {mode}")
```
```python
# do
# these two functions do the same things but each of them
# only has a single responsibility


def calculate_statistics(list_of_numbers):
    """Calculates arithmatic sum, mean, median and mode."""

    total = sum(list_of_numbers)
    mean = statistics.mean(list_of_numbers)
    median = statistics.median(list_of_numbers)
    mode = statistics.mode(list_of_numbers)

    return total, mean, median, mode


def print_statistics(total, mean, median, mode):
    """Prints statistics on the console."""

    print("-----------------Stats-----------------")
    print(f"SUM: {total}")
    print(f"MEAN: {mean}")
    print(f"MEDIAN: {median}")
    print(f"MODE: {mode}")
```
- 가능한 순수(pure)하거나 최소한 멱등(idempotent) 함수를 작성하도록 노력한다
  - 멱등 함수는 호출 횟수에 관계없이 항상 동일한 인수 집합이 주어지면 동일한 값을 반환합니다. 결과는 로컬이 아닌 변수, 인수의 가변성 또는 I/O 스트림의 데이터에 의존하지 않습니다.
  - 다음 함수는 멱등입니다. `square_num(5)`의 결과는 호출 횟수에 관계없이 항상을 `25`를 반환합니다.
    ```python
    def square_num(number):
        """This is an idempotent function."""
    
        return number ** 2
    ```
  - 다음 함수는 멱등이 아닙니다.
    ```python
    def square_num():
        """Return number_entered_by_user ** 2."""
    
        number = int(input("Enter a number: "))
        return number ** 2
    ```
  - Why?
    - 멱등 함수는 동일한 인수로 호출될 때 항상 동일한 결과를 반환하므로 테스트하기 쉽습니다. 
      테스트는 단순히 함수에 대한 다양한 호출에 의해 반환된 값이 예상 값을 반환하는지 확인하는 것입니다.
      
  - 함수는 멱등성이고 관찰 가능한 부작용이 없는 경우 순수(pure)하다고 간주됩니다. 예를 들어 위의 `square_func(number)`의 멱등 버전이 결과를 반환하기 전에 프린트(print)를 했거나 함수 범위 외부의 변수를 변경한 경우 I/O 스트림에 액세스하는 동안 여전히 멱등으로 간주됩니다. 그러나 더 이상 순수한 기능으로 남아 있지 않습니다.
    ```python
    a_variable = 0
    
    
    def square_num(number):
    """Idempotent but not pure."""
    
        sq_num = number ** 2
        a_variable += sq_num
    
        return sq_num
    ```
  - Why?
    - 순수 함수는 멱등 함수보다 테스트하기가 훨씬 쉽습니다. 함수 범위 바깥에 footprint를 유지하지 않습니다. 또한 순수하지 않은 함수를 호출하지 않습니다. 기본적으로 data-in-data-out 파이프 라인입니다.
### 모듈 불러오기 (import)
- 와일드 카드 가져 오기를 사용하지 않는다
```python
# don't
from mod import *
from package.mod import *

# do
from mod import func_0
from package.mod import func_1
```
- 사용하지 않는 모듈을 가져 오지 않는다
- [Flake8](https://itholic.github.io/python-flake8-list/) 은 사용되지 않은 `import`를 지적하므로 커밋하기 전에 제거해야 합니다
- `import`를 `from B import A`와 같이 사용하고 알파벳순으로 정렬하자
```python
# don't
from a_mod import foo
import e_mod
import b_mod
from z_mod import bar, baz

# do
import b_mod
import e_mod
from a_mod import foo
from z_mod import bar, baz
```
- 프로덕션 코드에서는 절대경로(absolute) `import`를 사용한다
- 상대경로 `import`는 특히 디렉토리 구조가 변경될 가능성이 있는 공유 프로젝트의 경우 지저분해질 수 있습니다.
```
└── project
└── package1
    ├── module1.py
    └── module2.py
```
```python
# package1/module1

# don't
from .module2 import func

# do
from package1.module2 import func
```

### 예외처리 
- bare except 블록을 작성하지 말자
  - except 부분에 특정 에러를 명시하는 것을 권고
```python
# don't
try:
    do_something()
except:
    pass

# don't
try:
    do_something()
except Exception:
    pass
```
- 대부분의 경우 포착된 예외 유형은 가능한 구체적이어야 합니다. `KeyError`, `ConnectionTimeout` 등
```python
# do
try:
    do_something()
# catch some very specific exception - KeyError, ValueError, etc.
except ValueError:
    pass
```
- 일부 코드 경로가 모든 예외를 광범위하게 포착해야하는 경우 이러한 포착된 각 예외는 타임 스탬프와 함께 전체 스택 추적을 로그 또는 파일에 기록해야 한다
  - 예를 들어, 장기 실행 지속 프로세스에 대한 최상위 루프
  - 예외 유형 및 메시지 뿐만 아니라 전체 스택 추적할 수 있어야 합니다.
```python
# do
def get_number():
    return int("foo")

try:
    x = get_number()
except ValueError:
    pass
except Exception:
    logging.exception("Caught an error", exec_info=True)
```

### 함수형 패러다임
Python은 다중 패러다임 언어로 간주되지만 정확히 함수형 언어로 설계되지는 않았으며 단순히 map, filter 및 reduce 함수가 있다고 해서 하나가 되지는 않았습니다.   
그러나 실제로 Python은 함수형 코딩이 가능합니다. 인수로 전달할 수 있으며 다른 함수에서 반환 할 수도 있습니다.   
이러한 함수형 프로그래밍을 남용하지 못하도록 하는 몇 가지 지침을 제안합니다.
- 익명화된(anonymized) `lambda` 함수의 사용을 최소한으로 제한하자
  - Why?
    - `lambda` 표현식 에서 오류가 발생하면 Python은 트레이스백에 함수 이름을 제공하지 않습니다. 또한 표현이 복잡해지면 읽기가 더 어려워집니다.
    ```python
    # don't
    div_zero = lambda x: x / 0
    div_zero(2)
    ```
    - 이 경우 추적은 다음과 같습니다.
    ```python
    Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
        File "<stdin>", line 1, in <lambda>
    ZeroDivisionError: division by zero
    ```
    
  - `lambda` 표현식을 할당하지 말자 (그렇게하면 `flake8`이 불평할 겁니다)
    - 만약 필요한 경우 일반적인 함수로 정의하십시오
  ```python
  # don't
  divider = lambda some_list: list(map(lambda n: n // 2, some_list))

  divider([1, 2, 3])
  # >> [0, 1, 1]

  
  # do
  def divider(some_list):
      return [x // 2 for x in some_list]

  divider([1, 2, 3])
  # >> [0, 1, 1]
  ```

- `map`, `filter`, `reduce`는 꼭 써야할 때만 쓰자
  - Why?
    - 거의 모든 경우 list comprehension 함수로 대체되고 내장될 수 있습니다
  - `Map`의 대안
    ```python
    # don't
    customers = ["Alice", "Bob", "Frank", "Ann"]
    result = map(lambda x: x[0], customers)
    
    print(list(result))
    # >> ['A', 'B', 'F', 'A']
    
    # do
    customers = ["Alice", "Bob", "Frank", "Ann"]
    result = [x[0] for x in customers]
    
    print(result)
    # >> ['A', 'B', 'F', 'A']
    ```
  - `Filter`의 대안
    ```python
    # don't
    customers = ["Alice", "Bob", "Frank", "Ann"]
    result = filter(lambda x: x[0] == "A", customers)
    
    print(list(result))
    # >> ['Alice', 'Ann']
    
    # do
    customers = ["Alice", "Bob", "Frank", "Ann"]
    result = [x for x in customers if x[0] == "A"]
    
    print(result)
    # >> ['Alice', 'Ann']
    ```
  - `Reduce`의 대안
    ```python
    # don't
    from functools import reduce
    
    print(reduce(lambda x, y: x + y, range(1, 6)))
    # >> 15
    
    # do
    print(sum(range(1, 6)))
    # >> 15
    ```


### Logging
패키지 `__init__.py` 모듈에서 로거를 인스턴스화 하자   
예시로 라이브러리 [requests](https://github.com/psf/requests/blob/master/requests/__init__.py) 를 참고하자

- 기본 로깅 클래스를 정의하세요
```python
# __init__.py
# demo of a global logger that can be called and used anywhere in your package

import logging

logging.getLogger(__name__)

logging.basicConfig(
    level=logging.INFO,
    format="\n(asctime)s [%(levelname)s] %(message)s",
    handlers=[logging.FileHandler("packg/debug.log"), logging.StreamHandler()],
)
```
- 다음과 같이 `import`해서 사용하세요
```python
# mod.py
# using the logging class defined in __init__.py

from . import logging


def dumb_div(a):
    try:
        res = a // 0
    except ValueError:
        res = a // 1
    except Exception:
        logging.exception("Exception Occured")
        res = None

    return res

dumb_div(5)
```
- 프로덕션 레벨에서는 `sentry` 등을 이용한 logging도 고려해 보세요
```python
# __init__.py

import logging
import sentry_sdk
from sentry_sdk.integrations.logging import LoggingIntegration

sentry_logging = LoggingIntegration(
    level=logging.INFO,  # Capture info and above as breadcrumbs
    event_level=logging.ERROR,  # Send errors as events
)
sentry_sdk.init(
    dsn="<sign-up-for-sentry-and-you-will-get-your-dsn>",
    integrations=[sentry_logging],
)
```
```python
# mod.py
# using the sentry logging class defined in __init__.py

from . import logging


def dumb_div(a):
        try:
            res = a // 0
        except ValueError:
            res = a // 1
        except Exception:
            logging.exception("Exception Occured")
            res = None

        return res

    dumb_div(5)
```
- 경우에 따라 핵심 로직에서 예외 처리 및 로거 로직을 분리해야합니다. 이를 위해 Python의 컨텍스트 관리자 데코레이터를 사용할 수 있습니다.
```python
from . import logging
from contextlib import contextmanager


class Calculation:
    """Dummy class for demonstrating exception decoupling with contextmanager."""

    def __init__(self, a, b):
        self.a = a
        self.b = b

    @contextmanager
    def errorhandler(self):
        try:
            yield
        except ZeroDivisionError:
            print(
                f"Custom handling of Zero Division Error! Printing "
                "only 2 levels of traceback.."
            )
            logging.exception("ZeroDivisionError")

    def main_func(self):
        """Function that we want to save from nasty error handling logic."""

        with self.errorhandler():
            return self.a / self.b
```
```
# folder structure of the logging demo package
packg
├── debug.log
├── __init__.py
└── mod.py
```

### 코드 패턴
#### Null 비교
PEP8에서 알 수 있듯이, 같은 단일 항목(singleton)에 대한 `None` 같은 비교는 항상 `is` 나 `is not`을 써야 합니다.
- `=`나 `!=`는 절대 쓰지 마세요!
- Why?
  - 연산자 `==`는 두 피연산자의 값을 비교하고 값이 같은지 확인합니다.
  - 연산자 `is`는 두 피연산자가 동일한 개체를 참조하는지 여부를 확인합니다.
```python
# don't
if val == None:
    # ...

if val != None:
    # ...
```
```python
# do
if val is None:
    # ...

if val is not None:
    # ...
```


#### 데코레이터(decorator)
가능한 경우 소스 코드를 직접 변경하는 대신 데코레이터를 사용하여 함수/메서드를 변경하거나 모니터링하자.   
다음과 같은 패턴을 추천한다.
```python
from functools import partial, wraps


def decorator(func=None, foo="spam"):
    if func is None:
        return partial(decorator, foo=foo)

    @wraps(func)
    def wrapper(*args, **kwargs):
        # do something with `func` and `foo`, if you're so inclined
        pass

    return wrapper
```
매개 변수를 포함하거나 포함하지 않고 사용할 수 있다.
```python
# applying decorator without any parameter
@decorator
def f(*args, **kwargs):
    pass


# applying decorator with extra parameter
@decorator(foo="buzz")
def f(*args, **kwargs):
    pass
```
또 다른 예제로써 `retry` 데코레이터를 참조하자.
- 미리 지정된 예외가 발생하는 경우 여러 번 호출을 실행하는 데코레이터
```python
import logging
import time
from functools import partial, wraps


def retry(func=None, exception=Exception, n_tries=5, delay=5, backoff=1, logger=False):
    """Retry decorator with exponential backoff.

    Parameters
    ----------
    func : typing.Callable, optional
        Callable on which the decorator is applied, by default None
    exception : Exception or tuple of Exceptions, optional
        Exception(s) that invoke retry, by default Exception
    n_tries : int, optional
        Number of tries before giving up, by default 5
    delay : int, optional
        Initial delay between retries in seconds, by default 5
    backoff : int, optional
        Backoff multiplier e.g. value of 2 will double the delay, by default 1
    logger : bool, optional
        Option to log or print, by default False
    Returns
    -------
    typing.Callable
        Decorated callable that calls itself when exception(s) occur.
    Examples
    --------
    >>> import random
    >>> @retry(exception=Exception, n_tries=4)
    ... def test_random(text):
    ...    x = random.random()
    ...    if x < 0.5:
    ...        raise Exception("Fail")
    ...    else:
    ...        print("Success: ", text)
    >>> test_random("It works!")
    """

    if func is None:
        return partial(
            retry,
            exception=exception,
            n_tries=n_tries,
            delay=delay,
            backoff=backoff,
            logger=logger,
        )

    @wraps(func)
    def wrapper(*args, **kwargs):
        ntries, ndelay = n_tries, delay

        while ntries > 1:
            try:
                return func(*args, **kwargs)
            except exception as e:
                msg = f"{str(e)}, Retrying in {ndelay} seconds..."
                if logger:
                    logging.warning(msg)
                else:
                    print(msg)
                time.sleep(ndelay)
                ntries -= 1
                ndelay *= backoff

        return func(*args, **kwargs)

    return wrapper
```

### 테스팅
- [pytest](https://docs.pytest.org/en/latest/) 를 사용하여 테스트 작성하자
- 테스트 파일의 이름은 `test_`로 시작해야 하며, 마찬가지로 테스트 함수도 `test_`로 시작되어야 한다
- 많은 작은 순수(pure) 함수 및 멱등(idempotent) 함수를 작성하고, 변형(mutations)이 발생하는 것을 최소화하자
- 버그를 수정할 때마다 [회귀 테스트](https://docs.python.org/3.8/library/test.html) 를 작성하자
  - 회귀(regression)<sup>[[2]](#footnote2)</sup> 테스트 없이 수정된 버그는 거의 확실하게 향후 다시 중단될 것이다
  - 모든 유닛 테스트 빌드는 기존 코드에 회귀되지 않는다는 것을 보장하도록 실행된다
- 직접 주장(direct assertions)과 명시적 비교(explicit comparisons)를 사용하자
  - 부정(negations)을 피하자
  ```python
  # don't - other values can be falsy too: `[], 0, '', None`
  assert not result
  assert result_list

  # do
  assert result == False
  assert len(result_list) > 0
  ```


## 주피터 노트북
### 매직 커맨드
- `%pylab inline`를 쓰지 말고 `%matplotlib inline`를 쓰자<sup>[[3]](#footnote1)</sup>   


## 각주
<strong><a name="footnote1">1.</a></strong> 제안자 <a class="user-mention" data-hovercard-type="user" data-hovercard-url="/users/jourmooney/hovercard" data-octo-click="hovercard-link-click" data-octo-dimensions="link_type:self" href="https://github.com/jourmooney">@jourmooney</a>가 89년생   
<strong><a name="footnote2">2.</a></strong> 새로운 변경사항은 기존 코드의 동작에 영향을 주지 않는다   
<strong><a name="footnote2">3.</a></strong> Jupyter의 코어 개발자 <a href="https://github.com/ipython/ipython/issues/8315">Carreau</a>가 격하게 반대.. <a href="https://carreau.github.io/posts/10-No-PyLab-Thanks/#Please-Stop-using-Pylab">[Blog]</a>

## 참고 문헌
- [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)
- [Python Coding Convention](https://spoqa.github.io/2012/08/03/about-python-coding-convention.html)
