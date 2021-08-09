- 참고: [파이썬 공식 자습서: 내장형](https://docs.python.org/ko/3/library/stdtypes.html#set-types-set-frozenset)
### 요소 변경
```python
sequence[offset] = x
```
- 여러 개의 요소를 한꺼번에 변경하려면 아래를 이용한다.

```python
sequence[start:end[:step]] = t
```

### 요소 삭제
#### 인덱스를 이용하여 삭제
```python
del sequence[start:end[:step]]
sequence[i:j] = []
```
#### 값을 이용하여 삭제
```python
sequence.remove(x)
```
- `sequence.remove(x)`에서 `x`가 `s`에서 발견되지 않으면 `remove()`는 `ValueError`를 일으킨다.
### 요소 추가
```python
sequence.append(x)
sequence[len(sequence):len(sequence)] = [x]
```

### 시퀀스 비우기
```python
s.clear()
del s[:]
```

### 시퀀스 복사(Shallow Copy)
```python
sequence.copy()
s[:]
```

### 시퀀스 확장
```python
sequence.extend(t)
sequence += t
sequence[len(sequence):len(sequence)] = t
```

### 기타 연산
```python
sequence *= n
```
- `sequence *= n`에서 `n`이 $<=0$이면 해당 시퀀스를 지운다.

### 가변 시퀀스 관련 메소드
```python
sequence.insert(i, x)
sequence.pop()
sequence.pop(i)
sequence.remove(x)
sequence.reverse()
```

