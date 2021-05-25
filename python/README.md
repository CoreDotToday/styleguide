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
6. [PEP8](https://www.python.org/dev/peps/pep-0008/)을 준수한다


## 환경
1. Python 3.6 이상을 사용한다
2. 마이너 업데이트가 있을 시 첫 패치 업데이트 이후 사용한다
   * 예) 3.9 버전은 3.9.1 이후로 사용
3. `import` 목록을 정리할 때는 [isort](https://github.com/PyCQA/isort)를 사용한다
   - `black`과 [호환되지 않으므로](https://pysanity.netlify.app/#auto-formatters) `isort`를 먼저 실행하고 `black`을 사용하는 것이 낫다



## 독스트링 (Docstrings)
- Numpy 스타일 독스트링을 기준으로 한다
  - [Numpy-style.py](https://github.com/CoreDotToday/styleguide/blob/main/python/docstring/Numpy-style.py)

## 세부논의

#### 코드 레이아웃
- 들여쓰기는 소프트탭(space character)을 이용해 공백 4칸을 사용
- 한 줄은 최대 89자까지 <sup>[[1]](#footnote1)</sup>
- 최상위(top-level) 함수와 클래스 정의는 2줄씩 띄어 씀
- 클래스 내의 메소드 정의는 1줄씩 띄어 씀


#### Single quote, double quote

- 둘 중 무엇이든 한 프로젝트에선 하나의 스타일로 통일성을 유지하게끔 사용함

* `docstrings`에는 triple double quotes를 사용한다
* `\\` 이스케이프를 피하고자 둘을 잠시 혼용하는 걸 허용한다


#### 코멘트
- 코드와 모순되는 주석은 없느니만 못함. 항상 코드에 따라 갱신할 것
- 불필요한 주석은 달지 말 것
- 한 줄 주석은 신중히 달 것

#### 명명 규칙
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
- 프라이빗 `속성`, `메소드`, `변수` 및 `함수` 앞에는 밑줄을 사용한다
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
LIST_1 = ["Jack", "Alice", "Emily"]
# ... many lines of code later
for item in LIST_1:
    add_person(item)

# do
NAME_LIST = ["Jack", "Alice", "Emily"]
# ... many lines of code later
for name in NAME_LIST:
    add_person(name)
```
- 이름 지정에 단수 또는 기본 단어를 사용한다.
  - 복수를 사용하지 말고 대신 데이터 유형과 함께 단수를 추가한다.
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


#### .gitignore
- 다음 파일을 참고하여 불필요한 파일은 Git에 올리지 말 것   
https://raw.githubusercontent.com/CoreDotToday/styleguide/main/python/.gitignore


## 각주
<strong><a name="footnote1">1.</a></strong> 제안자 <a class="user-mention" data-hovercard-type="user" data-hovercard-url="/users/jourmooney/hovercard" data-octo-click="hovercard-link-click" data-octo-dimensions="link_type:self" href="https://github.com/jourmooney">@jourmooney</a> 생일이 89년생

## 참고 문헌
- [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)
- [Python Coding Convention](https://spoqa.github.io/2012/08/03/about-python-coding-convention.html)
