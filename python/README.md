# Core.Today Python Style Guide

## 프로젝트 구성
뼈대는 다음의 가이드라인을 따릅니다

https://python-guide-kr.readthedocs.io/ko/latest/writing/structure.html

- [Skeleton](https://github.com/navdeep-G/samplemod)


## 기본 원칙
1. 하나의 함수는 하나의 일만 하도록 하자
2. 밑줄이 앞에 붙은 함수 이름은 패키지 내부에서만 사용되는 함수이다
3. 메인 코드가 실행되기 전에 의존성 버전 차이를 처리한다
4. Spinx 자동 문서화 확장을 사용하자
5. Autoformatter로 [`black`](https://github.com/CoreDotToday/styleguide/issues/2)을 사용하자
6. [PEP8](https://www.python.org/dev/peps/pep-0008/)을 준수한다


## 환경
1. Python 3.6 이상을 사용한다
2. 마이너 업데이트가 있을 시 첫 패치 업데이트 이후 사용한다
   * 예) 3.9 버전은 3.9.1 이후로 사용


## 독스트링 (Docstrings)
- Numpy 스타일 독스트링을 기준으로 한다
  - [Numpy-style.py](https://github.com/CoreDotToday/styleguide/blob/main/python/docstring/Numpy-style.py)

## 세부논의

#### 코드 레이아웃
- 들여쓰기는 공백 4칸을 권장
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

#### .gitignore
- 다음 파일을 참고하여 불필요한 파일은 Git에 올리지 말 것   
https://raw.githubusercontent.com/CoreDotToday/styleguide/main/python/.gitignore


## 각주
<strong><a name="footnote1">1.</a></strong> 제안자 <a class="user-mention" data-hovercard-type="user" data-hovercard-url="/users/jourmooney/hovercard" data-octo-click="hovercard-link-click" data-octo-dimensions="link_type:self" href="https://github.com/jourmooney">@jourmooney</a> 생일이 89년생

## 참고 문헌
- [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)
- [Python Coding Convention](https://spoqa.github.io/2012/08/03/about-python-coding-convention.html)
