# require vs include
- include 문에 파일이 포함되어 있는데 PHP가 찾을 수 없어도 스크립트는 계속 실행됨

## require
- 치명적인 오류(E_COMPILE_ERROR)가 발생할 경우 스크립트가 중지됨

## include
- 오류 발생시 경고(E_WARNING)만 발생하고 스크립트는 실행됨

### require_once
- 이미 포함된 함수에 대해선 다시 포함시키지 않음

### include_once
- 이미 포함된 파일에 대해선 다시 포함시키지 않음
- 지정한 파일이 없을 경우 warning 표시

---
## 참고링크
* [PHP_INCLUDES](https://www.w3schools.com/php/php_includes.asp)
