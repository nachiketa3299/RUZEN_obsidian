> `__getitem__()` 특수 메서드를 통해 정수 인덱스를 사용한 빠른 요소 액세스를 지원하고, 시퀀스의 길이를 돌려주는 `__len__()`메서드를 정의하는 [[Iterable|이터러블]].

- 내장 시퀀스의 예에는 다음과 같은 것들이 있다.
	- `list`
	- `str`
	- `tuple`
	- `bytes`
	- ~~`dict`~~ ^[`__getitem__()`과 `__len__()`을 지원하지만, 조회에 정수 대신에 임의의 불변 키를 사용하기 때문에 시퀀스가 아니라 매핑으로 취급된다.]