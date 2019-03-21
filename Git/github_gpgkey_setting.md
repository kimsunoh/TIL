# GPG
- GPG : GNU Privacy Guard
- pair key(private key & public key)를 생성해, 이 key pair를 가지고 암호화&복호화를 해서 데이터를 안전하게 보호하는 방법

## GPG 키 생성
- gpg 설치 : [설치 파일](https://gpgtools.org) 다운받은 후 설치
```
// osX 환경에서 설정함
$ gpg --full-generate-key

// terminel output question
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
Your selection? 

RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048)

Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for?

Is this correct? (y/N) 

GnuPG needs to construct a user ID to identify your key.

Real name: 
Email address: 
Comment:
You selected this USER-ID:
    "myName <Email Address>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? 

// then create gpg key, output message like this
gpg: key {gpg private key code} marked as ultimately trusted

// gpg key 확인 명령어
$ gpg --list-secret-keys --keyid-format LONG

> sec   rsaNNNN/{gpg private key code} 2019-03-21 [SC] [expires: 2020-03-20]
        
// git config 에 GPG key를 사용 설정
$ git config --global user.signingkey {gpg private key code}
//항상 commit에 sign을 하겠다는 명령어
$ git config --global commit.gpgsigntrue 

// github에 등록하기 위한 GPG pair key 생성
$ gpg --armor --export {gpg private key code}

// 출력으로 나온 GPG pair  Key를 복사해서 등록하기
// Personal settings > SSH and GPG keys > GPG keys > "New GPG key" 버튼 클릭후 복사내용 붙여넣기

// 커밋 후 sign 이 됬는지 확인하는 명령어
$ git log --pretty="format: %h %G? %aN %s"

> 
```

---
## 참고 링크
- [Git 도구 내 작업에 서명하기](https://git-scm.com/book/ko/v2/Git-도구-내-작업에-서명하기)
- [help github : generating a new gpg key](https://help.github.com/en/articles/generating-a-new-gpg-key)
- [시리즈:암호의 암도 몰라도 쉽게 하는 GPG](https://librewiki.net/wiki/시리즈:암호의_암도_몰라도_쉽게_하는_GPG)