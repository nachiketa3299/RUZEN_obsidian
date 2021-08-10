# Terminal Guide

## `ls`

## `cd`

## `man`
- [리눅스 도움말 명령어 man 사용법, 섹션](https://www.leafcats.com/117)
## 찾기 관련 명령어
### `find`

- [# [맥 터미널 / Unix] find 커맨드로 파일 검색하기](https://macinjune.com/all-posts/mac/terminal/맥-터미널-unix-find-command로-파일-검색하기/)
#### 기본 문법
```
$find [directory] [flag] [expression]
```
##### Examples
```
$find . -name "*.txt*"
```
- 현재 디렉토리(`.`)내 `.txt`를 포함한 모든(`*`)파일을 검색한다.
```
$find / -name "*.txt"
```
- 루트 디렉토리(`/`)내의 `.txt`를 포함한 모든(`*`)파일을 검색한다.
```
$find $HOME -name "*.txt"
```
#### 파일 타입으로 구분하여 검색하기
- `-type`옵션을 통해 파일 타입을 `d`(directory) 혹은 `f`(file)로 구분하여 검색이 가능하다.
##### 파일만 검색하기
```
$find . -name "exam*" -type f
```
##### 디렉토리만 검색하기
```
$find . -name "exam*" -type d
```
##### 파일과 디렉토리 모두 검색
```
$find . -name "exam*"
```

- 홈 디렉토리(`~`)내 `.txt`를 포함한 모든(`*`)파일을 검색한다.
### `locate`
> `locate`는 미리 빌트된 데이터베이스에서 빠른 검색을 지원한다.

### `grep`
> `grep`은 파일 내의 문장들에서 문자열 패턴을 검색한다.

### `mdfind`
> `mdfind`는 파일의 메타데이터를 검색한다.