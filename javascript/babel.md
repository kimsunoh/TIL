# Babel
- javascript transfiler
    - 서로 다른 언어간의 변환을 지원
    - ES6+ code를 ES5 code로 변환해준다
- 모던 JS 구문을 널리 지원되는 ES5 문법의 JS로 변환 할 수 있다

## 설정 파일 형태
- package.json
```json
{
  "babel": {
    "presets": ["es2015", "stage-0"]
  }
}
```
-babelrc
```json
{
  "plugins": ["transform-class-properties"]
}
```

## 

---
## 참고링크
- [(번역)(Fullstack React) What are babel "plugins" and "presets"? (And how to use them)](https://gompro.postype.com/post/1696324)