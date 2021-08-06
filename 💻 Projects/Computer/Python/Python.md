# Chapter 3-1. Sequence: 리스트, 튜플, 딕셔너리, 셋
> [[sequence|시퀀스]]들에 공통적으로 적용 가능한 연산은 [[시퀀스 공통 연산]]을 참조한다.

## 가변 [[sequence|시퀀스]] - 리스트, 바이트 배열
> 가변 자료형들에 공통적으로 적용 가능한 연산은 [[가변 [[sequence|시퀀스]] 공통 연산]]을 참조한다.
### 리스트 (Mutable)
- 모든 것의 [[sequence|시퀀스]]이다.
	- 리스트는 리스트를 요소로 가질 수도 있다.
- 데이터를 순차적으로 파악하는데 유용하다.
- 내용의 순서가 바뀔 수 있으며, 동일한 값이 여러 번 나타날 수 있다.
	- 요소들이 순서는 상관 없이 유일한 값으로만 유지될 필요가 있다면, *셋(Set)*을 사용한다.
- 내용을 변경 가능하다. 리스트의 현재 위치에서 새로운 요소를 추가하거나 삭제 혹은 기존 요소를 덮어쓸 수 있다.
#### 리스트 생성
- 리스트의 생성자는 아래와 같이 정의된다.
```python
class list([iterable])
```

##### 생성자로 생성
```python
l = list()
l = list(iterable)
```
- `list()`함수는 다른 데이터 타입(`iterable`)을 리스트로 변환한다.
	- 이 경우 순서가 `itreable`과 같은 리스트를 생성한다.
- `iterable`의 종류는 아래와 같다.
	- [[sequence|시퀀스]]
	- 이터레이션을 지원하는 컨테이너
	- 이터레이터 객체
- 
##### 리스트 리터럴 문법`[]`으로 생성
```python
l = []
```
##### 리스트 컴프리헨션
```python
l = [x for x in iterable]
```

#### 리스트 메소드
```python
list.sort(*, key=None, reverse=False)
```
### 바이트 배열 객체 (Mutable)
- 바이트 배열 객체(`bytearray`)는 바이트열 객체(`bytes`)의 가변형이다.
#### 바이트 배열 객체 생성
- 바이트 배열 객체의 생성자는 아래와 같다.
```python
class bytearray([source[, encoding[, errors]]])
```
- 바이트 배열 객체에 대한 전용 리터럴 문법은 없고, 항상 생성자를 호출하여 만든다.
##### 생성자로 생성
```python
bytearray()
bytearray(n)
bytearray(range(20))
bytearray(b'str')
```
#### 바이트 배열 메소드
```python
bytearray.fromhex(string)
bytearray.hex([sep[,bytes_per_sep]])
```
## 불변 [[sequence|시퀀스]] - 튜플, 바이트열, 문자열, 범위
### 바이트열 객체 (Immutable)
- `bytes`는 `bytesarray`와 함께 바이너리 데이터를 조작하는 데에 쓰인다.
- 바이트열 객체는 단일 바이트들의 불변 [[sequence|시퀀스]]이다.
- 많은 주요 바이너리 프로토콜이 ASCII 텍스트 인코딩을 기반으로 하기 때문에, 바이트열 객체는 ASCII 호환 데이터로 작업할 때만 유효한 여러 가지 메서드를 제공하며, 다양한 다른 방법으로 문자열 객체와 밀접한 관련이 있다.
#### 바이트열 객체 생성
- 바이트열 객체의 생성자는 아래와 같다.
```python
clas bytes([source[, encoding[, errors]]])
```
##### 생성자로 생성
```python
bytes(n)
bytes(range(n))
bytes(obj)
```
##### 바이트 리터럴 문법 `b`로 생성
```python
b'str"inside_str"str'
b"str'inside_str'str"
b'''str'''
b"""str"""
```
- 바이트열 리터럴에는 ASCII 문자만 허용된다.
- 바이트열 리터럴과 그 표현은 ASCII 텍스트를 기반으로 하지만, 바이트열 객체는 실제로는 *정수의 불변 [[sequence|시퀀스]]*처럼 동작하고, [[sequence|시퀀스]]의 각 값은 $0 \leq x < 256$이 되도록 제한된다.
	- 이 제한을 위반하면 `ValueError`를 일으킨다.
#### 바이트열 메소드
```python
bytes.fromhex(string)
bytes.hex([sep[, bytes_per_sep]])
```

### 튜플 (Immutable)
- 불변 [[sequence|시퀀스]]이며, 다음과 같은 상황에서 사용된다.
	- 이질적인 데이터의 모음을 저장할 때
	- 등질적인 데이터의 불변 [[sequence|시퀀스]]가 필요할 때
- 리스트를 대신하여 튜플을 사용할 수 있지만, 튜플은 리스트와 다르게 `append()`, `insert()`등과 같은 클래스 메소드가 없고, 메소드의 수가 매우 적다. 이는 튜플이 불변 [[sequence|시퀀스]]이기 때문이다.
- 일반적으로 튜플 보다는 리스트와 딕셔너리를 더 많이 사용한다.
- 리스트와 비교한 튜플의 특성은 아래와 같다.
	- 튜플은 더 적은 공간을 사용한다.
	- 실수로 튜플의 항목을 손상시킬 염려가 없다.
	- 튜플을 딕셔너리의 키로 사용할 수 있다.
	- 네임드 튜플은 객체의 단순한 대안이 될 수 있다.
	- 함수의 인자들은 튜플로 전달된다.
#### 튜플의 생성
- 튜플의 생성자는 아래와 같이 정의된다.
```python
class tuple([iterable])
```
##### 생성자로 생성
```python
t = tuple()
t = tuple(iterable)
```
##### 튜플 리터럴 문법 `,`으로 생성
```python
t = ()
t = x,
t = (x,)
t = a, b, c
t = (a, b, c)
```
- 튜플을 만드는 것은 실제로는 괄호(`()`)가 아니라 쉼표(`,`)이다.

### 문자열 (Immutable)
- 문자열은 유니코드 코드 포인트의 불변 [[sequence|시퀀스]]이다.
	- [코드 포인트란 무엇입니까?](https://www.netinbag.com/ko/internet/what-is-a-code-point.html)
- 파이썬에는 별도의 '문자(`char`)'형이 없으므로 문자열을 인덱싱 하는 경우 길이가 $1$인 문자열이 생성된다.
	- 다라서, 비어 있지 않은 문자열 `s`에 대해서 `s[0] == s[0:1]`이 성립한다.
#### 문자열의 생성
- 문자열의 생성자는 아래와 같다.
```python
class str(object='')
class str(object=b'', encoding='utf-8', errors='strict')
```
##### 생성자로 생성
```python
str(1)
str([1, 2, 3])
str('str')
str(b'str')
```
##### 문자열 전용 리터럴 문법 `'`, `"`로 생성
```python
'str"inside_str"str'
"str'inside_str'str"
'''str'''
"""str"""
```
- 삼중 인용 부호로 묶인 문자열은 여러 줄에 걸쳐 있을 수 있다. 
	- 이 경우, 연관된 모든 공백이 문자열 리터럴에 포함된다.
#### 문자열 메소드
```python
str.capitalize()
str.casefold()
str.center(width[,fillchar])
str.count(sub[, start[, end]])
str.encode(encoding="utf-8", errors="strict")
str.endswith(suffix[, start[,end]])
str.expandtabs(tabsize=8)
str.find(sub[, start[, end]])
str.format(*arg, **kwargs)
str.format_map(mapping)
str.index(sub[, start[, end]])
str.isalnum()
str.isalpha()
str.isascii()
str.isdecimal()
str.isdigit()
str.isidentifier()
str.islower()
str.isnumeric()
str.isprintable()
str.isspace()
str.istitle()
str.isupper()
str.join(iterable)
str.ljust(width[, fillchar])
str.lower()
str.lstrip([char])
static str.maketrans(x[, y[, z]])
str.partition(sep)
str.removeprefix(prefix, /)
str.removesuffix(suffix, /)
str.replace(old, nes[, count])
str.rfind(sub[, start[, end]])
str.rindex(sub[, start[, end]])
str.rjust(width[, fillchar])
str.rpartition(sep)
str.rsplit(sep=Non, maxplit=-1)
str.rstrip([chars])
str.split(sep=None, maxplit=-1)
str.splitlines([keepends])
str.startswith(prefix[,start[, end]])
str.strip([chars])
str.swapcase()
str.title()
str.translate(table)
str.upper()
str.zfill(width)
```
### 범위 (Immutable)
- `range` 형은 숫자의 불변 [[sequence|시퀀스]]를 나타내며 `for` 루프에서 특정 횟수만큼 반복하는 데 흔히 사용된다.
- `list`나 `tuple`에 비해 `range`가 갖는 장점은 `range`객체는 표현하는 범위의 크기에 무관하게 항상 같은(작은) 양의 메모리를 사용한다는 점이다.
	- `range` 객체는 `start`, `stop`, `step` 값만을 저장하고, 필요에 따라 개별 항목과 하위 범위를 계산한다.

#### 범위의 생성
- 범위 형의 생성자는 아래와 같다.
```python
class range(stop)
class range(start, stop[, step])
```
- 범위 생성자의 인자는 정수여야 한다.
- `step` 인자가 생략되면 기본값 $1$이 사용된다.
- `start` 인자가 생력되면 기본값 $0$이 사용된다.
##### 생성자로 생성
```python
rang = range(10)
rang = range(1, 11)
rang = range(0, 30, 5)
rang = range(0, -10, -1)
```
#### 범위 지원 연산
- 범위는 이어 붙이기와 반복을 제외한 [[시퀀스 공통 연산]]을 모두 구현한다.
	- 범위 객체는 엄격한 패턴을 따르는 [[sequence|시퀀스]]만 나타낼 수 있는데, 반복과 이어 붙이기는 보통 그 패턴을 위반한다는 사실에 기인한다.
- `==`나 `!=`로 범위 객체가 같은지 검사하면 [[sequence|시퀀스]]처럼 비교한다. 두 범위 객체가 같은 시퀀스의 값을 나타낼 때 같다고 취급된다.
	- 같다고 비교되는 두 개의 범위가 서로 다른 `start`, `stop`, `step`을 가질 수 있기에 주의해야 한다.
# Chapter3-2. Collection: 사전, 집합
- [[sequence|시퀀스]]와는 다르게, 컬렉션은 Deterministic Ordering을 갖지 않는다. ^[물리적으로 순서가 있긴 하므로 접근할 때마다 똑같은 순서의 값을 반환받지만, 요소를 추가하거나 삭제한다면 순서에 영향을 미친다.]

## 집합 (Mutable & Immutable)
- 집합 객체는 서로 다른 [[hash|해시]]가능 객체의 순서 없는 컬렉션이다.
- 집합의 일반적 용도는 아래와 같다.
	- 멤버십 검사
	- [[sequence|시퀀스]]에서 중복 제거
	- 교집합, 합집합, 차집합, 대칭 차집합과 같은 수학 연산
### 가변 집합 - `set` & 불변 집합 - `frozenset`
- `set`은 가변이므로 내용을 `add()`나 `remove()`와 같은 메서드를 사용하여 내용을 변경할 수 있다.
- `set`은 가변이기 때문에 [[hash|해시]]값이 없으며 딕셔너리 키 또는 다른 집합의 원소로 사용할 수 없다.
- `frozenset`형은 불변이고 [[hash|해시]]가능하다.
- `frozenset`형은 만들어진 후에는 내용을 바꿀 수 없으며, 따라서 딕셔너리 키 또는 다른 집합의 원소로 사용할 수 있다.
### 집합의 생성
- `set`과 `fozenset`의 생성자는 같게 작동한다.
```python
class set([iterable])
class frozenset([iterable])
```
- 집합의 원소는 반드시 [[hash|해시]] 가능해야 한다.
- 집합의 집합을 표현하려면, 포함되는 집합은 반드시 `frozenset` 객체여야 한다.

#### 생성자로 생성
```python
s = set()
s = set('foobar')
s = set(['a', 'b', 'foo'])
s = frozenset()
s = frozenset('foobar')
s = frozenset(['a', 'b', 'foo'])
```
- 생성자로 전달된 [[iterable|이터레이블]] 객체에 중복된 값이 있다면, 집합 자료형은 이를 모두 무시한다.
#### 집합 전용 리터럴 문법 `{}`사용
```python
s = {}
s = {'a', 'b'}
```

#### 집합 컴프리헨션
```python
s = {x for x in 'abcd' if x is not 'a'}
```

### 집합 제공 연산
```python
len(set)
x in set
x not in set
set.isdisjoint(other)
set.issubset(other)
set <= other
set < other
issuperset(other)
set >= other
set > other
set.union(*others)
set.intersection(*others)
set.difference(*others)
set.symmetric_difference(other)
set.copy()
```
## 사전 (Mutable), 또는 매핑 형
- 사전은 파이썬에서 유일하게 지원하는 하나의 표준 매핑 형이다.
	- 매핑 객체는 [[hash|해시]] 가능 값을 임의의 객체에 대응시킨다.

### 사전의 키(key)
- 사전의 키는 *거의* 임의의 값이다.
- [[hash|해시]] 가능하지 않은 값들, 즉 리스트, 사전, 또는 다른 가변형은 키로 사용할 수 없다.
- 키에 숫자형이 사용될 때, 숫자 비교를 위한 일반적인 규칙을 따른다.
	- 두 숫자가 같다고 비교되는 경우(`1`과 `1.0`처럼) 같은 사전 항목을 인덱싱하는데 서로 교환하여 사용할 수 있다.^[그러나 컴퓨터는 부동 소수점 숫자를 근삿값으로 저장하므로 이것들을 딕셔너리 키로 사용하는 것은 현명하지 않다.]

### 사전의 생성
- 사전 클래스는 다음과 같이 정의된다.
```python
class dict(**kwarg)
class dict(mapping, **kwarg)
class dict(iterable, **kwarg)
```
- 키가 두 번 이상 나타나면, 그 키의 마지막 값이 새 사전의 해당 값이 된다.
- 다음 예제는 모두 `{'a': 1, 'b': 2, 'c': 3}`이라는 *동일한* 사전을 반환한다.
	```python
	dictionary = {'a': 1, 'b': 2, 'c': 3}
	dictionary = dict(a=1, b=2, c=3)
	dictionary = dict(zip(['a', 'b', 'c'], [1, 2, 3]))
	dictionary = dict([('b', 2), ('a', 1), ('c', 3)])
	dictionary = dict({'a': 1, 'c': 3}, b=2)
	dictionary = dict({'c': 3, 'b': 2, 'a': 1})
	```
#### 생성자로 생성
```python
dictionary = dict()
dictionary = dict([('a', 1), ('b', 2)])
dictionary = dict(foo=100, bar=200)
```
#### 사전 전용 리터럴 문법으로 생성
```python
dictionary = {}
dictionary = {1:'a', 2:'b'}
```

#### 사전 컴프리헨션
```python
dictionary = {x: x ** 2 for x in range(10)}
```

### 사전 지원 연산
```python
list(dictionary)
len(dictionary)
dictionary[key]
dictionary[key] = value
del dictionary[key]
key in dictionary
iter(dictionary)
dictionary.clear()
dictionary.copy()
dictionary.fromkeys(iterable[, value])
dictionary.get(key[,default])
dictionary.items()
dictionary.keys()
dictionary.pop(key[,default])
dictionary.popitem()
reversed(dictionary[.keys()])
dictionary.setdefault(key[, default])
dictionary.update([other])
dictionary.values()
dictionary | other
dictionary |= other
```

### 사전 뷰 객체
- `dict.keys()`, `dict.values()`, `dict.itesm()`가 돌려주는 객체는 뷰 객체이다.
- 뷰 객체는 사전의 항목들에 대한 동적인 뷰를 제공한다. 사전이 변경되면 뷰는 이러한 변경 사항을 반영한다.
- 뷰 객체는 이터레이션을 통해 각각의 데이터를 산출할 수 있고, 멤버십 검사를 지원한다.

#### 사전 뷰 지원 연산
```python
len(dictview)
iter(dictview)
x in dictview
reversed(dictview)
```