# Jython 이란 
- Java 플랫폼 용 Python 언어의 구현

## Python의 3 종류
- CPython
	- C로 구현된 Python 정식 구현
	- 일반적으로 말하는 Python은 CPython을 말함
- Jython
	- JVM을 위한 Python
- IronPython
	- .NET 환경을 위한 Python

# Python과 동일한가?
- Jython x.x은 CPython x.x와 동일한 언어를 구현한 구현체 이며, 거의 모든 Core Python 표준 라이브러리 모듈을 구현함
- Jython은 Python을 Java 플랫폼에서 구현한 구현체
	- ex) Jython 2.7은 CPython 2.7과 같은 구현체

## 다른점
- Jython 프로그램은 C로 작성된 CPython 모듈을 사용할 수 없음
- Jython은 Python의 참조 계산 방식을 사용하지 않고, Java의 가비지 수집 방식을 사용함

---
## 참고링크
* Read the Docs - [자이썬(Jython) 완벽 안내서](https://jythonbook-ko.readthedocs.io/en/latest/LangSyntax.html)
* Python WIKI - [Jython General Information](https://wiki.python.org/jython/JythonFaq/GeneralInfo)