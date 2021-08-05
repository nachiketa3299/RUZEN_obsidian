> 멤버들을 한 번에 하나씩 돌려줄 수 있는 파이썬 객체이다.

- 이터러블의 예로는 모든 시퀀스(`list`, `str`, `tuple`과 같은) 형들, `dict`와 같은 몇몇 비 시퀀스 형들, 파일 객체들, `__iter__()`나 시퀀스 개념을 구현하는 `__getitem__()` 메서드를 써서 정의한 모든 클래스의 객체들이 있다.
- 이터러블을 `for`루프에 사용될 수 있고, 시퀀스를 필요로 하는 다른 많은 곳 (`zip()`, `map()` 등)에 사용될 수 있다.
- 이터러블 객체가 내장 함수 `itre()`에 인자로 전달되면, 그 객체의 [[iterator|이터레이터]]를 돌려준다.
- 이 [[iterator|이터레이터]]는 값들의 집합을 한 번 거치는 동안 유효하다.
- 이터러블을 사용할 때, 보통은 `iter()`를 호출하거나, [[iterator|이터레이터]] 객체를 직접 다룰 필요가 없다. `for`문은 이것을 우리를 대신해서 자동으로 해주며, 루프를 도는 동안 [[iterator|이터레이터]]를 잡아둘 이름 없는 변수를 만든다.