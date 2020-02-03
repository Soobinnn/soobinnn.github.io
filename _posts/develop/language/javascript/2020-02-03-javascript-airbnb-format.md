---
title: '[JavaScript] Formatting'
date: 2020-02-03 10:49:00 -0400
categories: devlog
tags: javascript devlog format
---

본 설정은 **VS Code** 에서 실행함.

# ESLint / Prettier 적용

## 1. VS Code 플러그인 설치

## 2. 프로젝트 적용

### 1) ESLint, Prettier 라이브러리 프로젝트에 설치

```
npm install -D eslint prettier
```

### 2) Airbnb 설정 설치

```
npx install-peerdeps --dev eslint-config-airbnb
```

### 3) ESLint-Prettier 연동 plugin

```
npm install -D eslint-config-prettier eslint-plugin-prettier
```

- eslint-plugin-prettier

  Prettier를 ESLint 플러그인으로 추가한다. 즉, Prettier에서 인식하는 코드상의 포맷 오류를 ESLint 오류로 출력해준다.

- eslint-config-prettier

  ESLint의 formatting관련 설정 중 Prettier와 충돌하는 부분을 비활성화 한다.

eslint-config-prettier은 prettier 에서 관리 해 줄 수 있는 코드 스타일의 ESLint 규칙을 비활성화 시켜줍니다. 이것을 사용하게 된다면 ESLint 는 자바스크립트 문법 관련된 것들만 관리하게 되고, 코드스타일 관련 작업은 prettier 가 담당하게 됩니다.

이 라이브러리 말고도 prettier-eslint 라는 도구도 있습니다. 이 도구는 prettier 에서 ESLint 설정을 연동해서 사용하게 해주는데요, .prettierrc 같은 파일을 생성하지 않고 온전히 ESLint 설정으로만 관리합니다.

사용률만 따지면 eslint-config-prettier 가 6배정도 더 많이 사용됩니다. 저는 둘 다 사용해봤는데 eslint-config-prettier 를 더 선호합니다

### 4) .eslintrc. 설정 (root directory)

```
{
  "extends": [ "airbnb", "prettier"],
  "plugins": [ "prettier"],
  "rules": {
    "prettier / prettier": [ "error"]
  },
}
```

### 5) .prettierrc 설정 (root directory)

```
{ "printWidth": 200, "semi": true, "singleQuote": true, "useTabs": false, "tabWidth": 2, "trailingComma": "all"
}
```

자세한 설정 참고 [https://prettier.io/docs/en/options.html](https://prettier.io/docs/en/options.html)

- singleQuote

  boolean 문자열을 사용할 때 '를 사용

- semi

  boolean 코드는 ;로 끝나야함.

- useTabs

  boolean 탭 대신에 스페이스를 사용함.

- tabWidth

  int 들여쓰기 크기

- trailingComma

  all 객체나 배열을 작성 할 때, 원소 혹은 key-value의 맨 뒤에있는 것에도 쉼표를 붙인다.

- printWidth

  int 한줄 길이

### ESLint 검사 무시하기

```

고칠 필요가 없는 경우, 파일 최상단에 주석 추가

/_ eslint-disable _/

```

# 참고 문서

https://velog.io/@velopert/eslint-and-prettier-in-react

```

```
