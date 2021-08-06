## 17-2) 포인터의 필요성은 어디에서 찾아야 하는가?
- [[Data Structure|자료 구조]]를 공부하면 포인터의 필요성을 보다 확실히 느낄 수 있다.
- 일단은 포인터에 대해서 열심히 공부하고, 포인터가 가져다 주는 이점은 앞으로 천천히 생각해 보기로 하자.

# 18. 다차원 배열 그리고 포인터
- 포인터의 마지막 난관.

## 18-1) 2차원 배열 이름의 포인터 타입
- 함수로 전달되는 배열의 이름은 포인터로 받을 수 있다고 배웠다.
	- 예를 들어, `int arr[5]`는 `int *`로 받는다.
	- 배열의 이름 자체가 배열의 타입과 동일한 타입의 **포인터 상수**이기 때문에 가능한 일이었다.
- 그러면 *"2차원 배열의 이름은 더블 포인터로 받으면 되겠네"*라고 쉽게 결론 내릴 수도 있지만, 잘못된 생각이다.
	- 2차원 배열 이름의 포인터 타입은 무조건 더블 포인터라고 할 수 없다.
### 1) 2차원 배열의 이름이 가리키는 것은?
- 1차원 배열에서는 배열 이름이 가리키는 요소가 배열 이름의 포인터 타입을 결정짓는 기준이었다.
- 2차원 배열에서도 마찬가지로 배열 이름이 가리키는 요소가 배열 이름의 포인터 타입을 결정짓는 기준의 일부가 된다.
	[[two_array1#Source Code]]
	[[two_array1#Execution Report]]
	- 위 예제에서는 `a[0]`,  `a[1]`, `a[2]`가 나타내는 값을 출력하고 있다. 
		- 여기서, 출력되는 값의 차이가 $8$임을 알 수 있다.
		- 또한, 배열 이름 `a`가 가리키는 곳과 `a[0]`이 가리키는 곳이 같음도 알 수 있다.
	- `a[0]`은 배열 요소 `a[0][0]`을 가리키고, `a[1]`은 배열 요소 `a[1][0]`을 가리키며, 마지막으로 `a[2]`는 배열 요소 `a[2][0]`을 가리킨다.
		- 이를 2차원적인 메모리 구조로 이야기한다면, 각 행의 첫 번째 요소를 가리킨다고 말할 수 있다.
	- 이제 배열 이름 `a`의 포인터 타입에 대해 이야기 해보자.
		- 쉽게 생각해서, a가 가리키는 요소가 배열의 첫 번째 요소 `a[0][0]`이므로, `int`형 포인터라고 결론 내릴 수 있다.
		> 왜? 배열의 첫 번째 요소가 `int`형 변수이기 때문이다.
		- 하지만 이것이 끝이 아니고, 배열 이름 `a`의 포인터 타입은 조금 더 구체화되어야 한다.
			- 배열 이름 `a`가 '`int`형 포인터야'라고 하는 것은, 완벽한 설명이 아니다. 이 정도의 정의로는 하다 못해 배열 이름 `a`를 인자로 받는 함수조차 적절한 형태로 정의하지 못한다.
	- 자세한 내용은 [[배열의 이름과 포인터의 관계에 대해서#결론]]를 참조한다.
### 2) 2차원 배열 이름 + 1: 배열 이름을 이용한 포인터 연산
- 2차원 배열 이름도 배열의 첫 번째 요소를 가리키는 포인터이므로, 배열의 이름이 지니는 값을 하나 증가시키면 어딘가 새로운 곳을 가리키게 될 것이다.
#### `arr2_name.c`
```c
#include <stdio.h>

int main()
{
	int a[3][2] = {1, 2, 3, 4, 5, 6};

	printf("- a    : %p\n", a);
	printf("- a + 1: %p\n", a + 1);
	printf("- a + 2: %p\n", a + 2);

	return 0;
}

```
```
- a    : 0x107aa7740
- a + 1: 0x107aa7748
- a + 2: 0x107aa7750
```
- 2차원 배열 이름은 포인터 연산 시 행 단위로 이동을 한다.

### 3) 포인터의 타입에는 이동에 대한 정보가 들어있다.
- 우리가 흔히 이야기 하는 *포인터 타입*에는 *이동에 대한 정보*가 들어있다.

```c
#include <stdio.h>

int main()
{
	int a[5] = {1, 2, 3, 4, 5};
	double d[5] = {1.1, 2.2, 3.3, 4.4, 5.5};
	
	int * pA = a + 1; // +4 (a is int)
	int * pD = d + 1; // +8 (d is double)
	return 0;
}
```

- `a`에 $1$을 더하면 실제로는 $4$가 증가한다.
	- 피연산자 `a`가 `int *`형이기 때문이다.
- `d`에 $1$을 더하면 실제로는 $8$이 증가한다.
	- 피연산자 `d`가 `double *`형이기 때문이다.
- 실제로는 배열 이름이 해당 타입의 포인터로 [[배열의 이름과 포인터의 관계에 대해서#결론|붕괴]]한 것이다.
> 임의의 두 포인터 타입이 일치한다면, 기본적으로 포인터 연산에 의해 증가 및 감소되는 값의 크기가 일치해야 한다. 위 예제에서 `a`와 `d`는 연산에 의해 증가되는 값이 다르므로 둘은 서로 포인터 타입이 다르다고 말 할 수 있다.
```c
#include <stdio.h>

int main()
{
	int arr1[3][2];
	int arr2[2][3];

	printf("> About arr1[3][2]\n");
	printf("- arr1    : %p\n", arr1);
	printf("- arr1 + 1: %p\n", arr1 + 1);
	printf("- arr1 + 2: %p\n", arr1 + 2);

	printf("> About arr2[2][3]\n");
	printf("- arr2    : %p\n", arr2);
	printf("- arr2 + 1: %p\n", arr2 + 1);
	printf("- arr2 + 2: %p\n", arr2 + 2);

	return 0;
}

```
```
> About arr1[3][2]
- arr1    : 0x111076740
- arr1 + 1: 0x111076748
- arr1 + 2: 0x111076750
> About arr2[2][3]
- arr2    : 0x111076720
- arr2 + 1: 0x11107672c
- arr2 + 2: 0x111076738
```
- 결론적으로 `arr1`과 `arr2`는 배열 요소의 자료형이 같은 2차원 배열임에도 불구하고, 이름 자체가 지니는 포인터 타입은 다르다고 결론 내릴 수 있다. **왜냐하면 포인터 연산 시 증가되는 값이 차이를 보이기 때문이다.**
- `int arr1[3][2]`
	- 배열 이름 `arr1`은 `int`형 포인터이자, 포인터 연산 시 배열 요소를 $2$칸씩 건너 뛰는 포인터이다.
	- 이와 완전히 일치하는 타입의 포인터 변수는 `int (*pArr1)[2];`로 선언할 수 있다.
- `int arr2[2][3]`
	- 배열 이름 `arr2`은 `int`형 포인터이자, 포인터 연산 시 배열 요소를 $3$칸씩 건너 뛰는 포인터이다.
	- 이와 완전히 일치하는 타입의 포인터 변수는 `int (*pArr2)[3];`로 선언할 수 있다.
> 배열을 가리킬 수 있는 포인터를 **배열 포인터**라고 한다.

###### `pnt_arr.c`
```c
#include <stdio.h>

void show_data(int (*ptr)[4], int a);

int main()
{
	int arr1[2][4] = {1, 2, 3, 4, 5, 6, 7, 8};
	int arr2[3][4] = {{1}, {2}, {3}};

	show_data(arr1, 2);
	show_data(arr2, 3);

	return 0;
}

void show_data(int (*ptr)[4], int a)
{
	printf("======Start Printing======\n");
	for(int i = 0; i < a; i++)
	{
		for(int j = 0; j > 4; j++)
			printf("%d ", ptr[i][j]);
		printf("\n");
	}
	return;
}
```
- `arr1`과 `arr2`는 둘 다 `int`형 1차원 포인터이면서 포인터 연산시 $4$칸씩 이동을 한다.
	- 따라서 둘의 포인터 타입은 `int (*ptr)[4]`로 동일하다.
- 함수 `show_data`는 매개 변수로 `int (*ptr)[4]`를 전달받는다.
	- 함수의 매개 변수 선언 시 `int (*ptr)[4]`와 같은 표현 외에도 `int ptr[][4]`와 같은 표현도 사용 가능하다.
	- 이러한 표현은 함수의 매개 변수 선언시에만 가능하다. 외의 경우에 위같은 표현을 사용하면 크기를 생략한 배열 선언으로 인식한다.
#### `int (*pArr)[4]`와 `int * pArr[4]`의 차이점
- `int (*pArr)[4]`는 **포인터 배열**이다.
- `int * pArr[4]`는 **배열 포인터**이다.

## 18-2) 2차원 배열에서의 `arr[i]`와 `*(arr + i)`
- 13장에서 `arr[i] == *(arr + i)`가, `arr`이 **포인터 변수**이거나 **배열의 이름**인 경우에 항상 성립함을 이야기하였다.
- 이것이 2차원 배열에서도 성립하는지 확인해 보자.
###### `two_array2.c`
```c
#include <stdio.h>

int main()
{
	int a[3][2] = {{1, 2}, {3, 4}, {5, 6}};

	for(int i = 0; i < 3; i++)
	{
		printf("- a[%d]      : %p\n", i, a[i]);
		printf("- *(a + %d)  : %p\n", i, *(a + i));
		printf("\n");
	}
	printf("- a[1][0]        : %d\n", a[1][0]);
	printf("- (*(a + 1))[0]  : %d\n", (*(a + 1))[0]);
	printf("\n");
	printf("- a[1][1]        : %d\n", a[1][1]);
	printf("- *(a[1] + 1)    : %d\n", *(a[1] + 1));
	printf("\n");
	printf("- a[2][1]        : %d\n", a[2][1]);
	printf("- *(*(a + 2) + 1): %d\n", *(*(a + 2) + 1));

	return 0;
}
```
- `a`가 2차원 배열의 이름일 때, 다음과 같은 결과를 확인할 수 있다.
	> `a[i]` $=$ `*(a + i)`
	> `a[i][j]` $=$ `(*(a + i))[j]` $=$ `*(a[i] + j)` $=$ `*(*(a + i) + j)` 

# 19. 함수 포인터와 `void`포인터
## 19-1) 함수 포인터
- 다음과 같은 상황을 가정해 보자.
	- `main`, `fct1`, `fct2`, `fct3`의 3개의 함수로 구성이 되어 있는 `test.c`를 컴파일 하여 `test.exe`라는 실행 파일을 생성하였다.
	- `test.exe`파일을 더블 클릭하면 다음과 같은 과정을 거쳐 프로그램이 실행된다.
		1. 프로그램의 실행은 CPU가 담당한다.
		2. CPU는 메인 메모리에 올라와 있는 자료로 일을 하므로, 하드 디스크상에 존재하는 `test.exe`를 구성하는 함수 `main`, `fct1`, `fct2`, `fct3`을 메인 메모리로 옮겨야 한다.
		3. 메인 메모리에 올려 두면 CPU에 의해 실행 가능한 상태가 된다.
	- 함수 포인터란 메인 메모리에 올라와 있는 함수를 가리킬 수 있는 포인터이다.

### 1) 함수 포인터란 무엇인가?
- 프로그래머가 정의한 모든 함수는 실행 시 메인 메모리(Main memory)에 올라가게 된다.
	- 이 때에 **함수의 이름**은 **메모리 상에 존재하는 함수의 위치를 가리키는 주소 값**을 의미한다.
	- 물론 함수의 이름은 배열의 이름과 마찬가지로 **상수 포인터**이다.
- `fct(1, 3)`과 같은 함수 호출문은 다음과 같이 이해할 수 있다.
	- 상수 포인터 `fct`가 가리키는 곳에 존재하는 함수를 호출하면서, 첫 번째 인자로 `1`, 두 번째 인자로 `3`을 전달해라.
> 함수의 이름이 주소값을 지니는 포인터이기 때문에, 함수의 이름과 동일한 타입의 포인터 변수를 선언하여 그 값을 저장할 수도 있으며, 이러한 기능을 가진 포인터를 가리켜 **함수 포인터**라고 한다.

### 2) 함수 포인터의 포인터 타입은 어떻게 되는가?
- 함수 이름의 포인터 타입을 결정짓는 요소는 **반환형**과 **전달인자**이다.
	```c
	int foo(int a)
	{
		a++;
		return a;
	}

	double bar(double a, double b)
	{
		double add = a + b;
		return add;
	}
	```
	- 함수 이름 `foo`은 반환형이 `int`이고 전달 인자가 `int`형 변수 하나인 포인터 타입이다.
	- 함수 이름 `bar`는 반환형이 `double`이고 전달 인자가 `double`형 변수 두개인 포인터 타입이다.

### 3) 적절한 함수 포인터의 선언
```c
int (*fPtr1)(int, double);
```
- 함수 포인터는 위와 같이 선언하면 된다.
- 함수 포인터 `fPtr`은 반환형이 `int`이고 전달 인자가 `int`, `double`형 2개인 **모든** 함수를 가리킬 수 있다.

###### `fct_ptr1.c`
```c
#include <stdio.h>

int add(int, int);
int sub(int, int);
void sPrint(char *);

int main()
{
	int (*p)(int, int);
	void (*s)(char *);

	p = add;
	printf("- add(1, 3): %d\n", add(1, 3));
	printf("- p(1, 3)  : %d\n", p(1, 3));

	p = sub;
	printf("- sub(1, 3): %d\n", sub(1, 3));
	printf("- p(1, 3)  : %d\n", p(1, 3));

	s = sPrint;
	printf("- sPrint(\"123\"):\n");
	sPrint("123");
	printf("- s(\"123\")     :\n");
	s("123");

	return 0;
}

int add(int a, int b)
{
	return a + b;
}

int sub(int a, int b)
{
	return a - b;
}

void sPrint(char * str)
{
	printf(" >> %s\n", str);
}
```
```
- add(1, 3): 4
- p(1, 3)  : 4
- sub(1, 3): -2
- p(1, 3)  : -2
- sPrint("123"):
 >> 123
- s("123")     :
 >> 123
```
- 함수 포인터는 위와 같이 사용될 수 있다.

###### `fct_ptr2.c`
```c
#include <stdio.h>

void select(int);
void add(void);
void min(void);

int main()
{
	int sel;

	while(1)
	{
		printf("===== Menu =====\n");
		printf("\t Add  (1)\n");
		printf("\t Sub  (2)\n");
		printf("\t Quit (3)\n");
		printf("- Your select: ");
		scanf("%d", &sel);
		if(sel == 3)
			break;
		select(sel);
	}

	printf("> Program terminated.\n");

	return 0;
}

void select(int s)
{
	void (*p)(void);
	if(s == 1)
		p = add;
	else
		p = min;
	p();
	return;
}

void add(void)
{
	int a, b;
	printf(">> Add| Input 2 integers:");
	scanf("%d %d", &a, &b);
	printf(">> Add| Result: %d\n", a + b);

	return;
}

void min(void)
{
	int a, b;
	printf(">> Min| Input 2 integers:");
	scanf("%d %d", &a, &b);
	printf(">> Min| Result: %d\n", a - b);

	return;
}
```
```
===== Menu =====
	 Add  (1)
	 Sub  (2)
	 Quit (3)
- Your select: 1
>> Add| Input 2 integers:1 3
>> Add| Result: 4
===== Menu =====
	 Add  (1)
	 Sub  (2)
	 Quit (3)
- Your select: 1
>> Add| Input 2 integers:4 5
>> Add| Result: 9
===== Menu =====
	 Add  (1)
	 Sub  (2)
	 Quit (3)
- Your select: 1
>> Add| Input 2 integers:10 1000
>> Add| Result: 1010
===== Menu =====
	 Add  (1)
	 Sub  (2)
	 Quit (3)
- Your select: 2
>> Min| Input 2 integers:10 1000
>> Min| Result: -990
===== Menu =====
	 Add  (1)
	 Sub  (2)
	 Quit (3)
- Your select: 3
> Program terminated.
```
> 함수 포인터는 우리가 정의한 함수를 운영체제에게 알려 줄 때 유용하게 사용되는 개념이다. 우리가 정의한 함수의 이름을 운영체제에 전달하면 운영체제는 전달된 함수의 이름을 이용해서 우리를 대신해 함수를 호출해 준다.

## 19-2) `void` 형 포인터
- `void` 형 포인터 변수를 선언하게 되면 변수이건, 함수이건, 하다못해 포인터의 주소 값까지도 저장이 가능하다.

```c
char c = `a`;
int n = 10;

void *vp;
vp = &c;
vp = &n;
```
- `void` 형 포인터인 `vp`는 무엇이든 담을 수 있으므로 변수 `n`과 `c`의 타입에 관계없이 주소값 `&n`과 `&c`를 저장할 수 있다.
- *무엇이든 담을 수 있다*는 것은 단점이 되기도 하는데, **`void` 포인터를 가지고는 아무것도 하지 못한다.**
	- 값을 변경하거나, 참조하는 일들, 하다못해 포인터 연산까지도 허용이 되지 않는다.
	- 포인터 자체에 **데이터에 대한 정보**(몇 바이트를 읽어 들여야 하는지)가 없으므로 이는 당연하다.
```c
int n = 10;
void *vp = &n;
*vp = 20;		// Error
vp++;			// Error
```
- `*vp = 20;`과 `vp++;`는 오류를 발생시킨다. `void` 형 포인터는 주소 값을 저장하는 것 외에는 아무 것도 할 수 없기 때문이다.
- 따라서 `void` 형 포인터는 반드시 **명시적 형 변환**을 거쳐서 사용하게 된다.
	- *일단 주소 값을 저장해 두고, 포인터의 타입은 나중에 결정한다!*는 전략을 세울 때 필요한 포인터로서, 25장에서 언급되는 "메모리의 동적 할당"에서 유용하게 사용된다.
	
```c
int n = 10;
void *vp = &n;
*((int *) vp) = 20;
```
- `*((int *) vp) = 20;` 로 `void`형 포인터가 가리키는 변수의 값을 `20`으로 변경하기 위해 `int *`로 명시적으로 형 변환을 해주고 있다.

## 19-3) `main` 함수도 인자를 받을 줄 알아요
### 1) `main`함수를 통한 인자의 전달
- 지금까지 선언한 `main`함수는 인자를 전달받지 못하도록 `void`로 선언되어 있었으나, 프로그램 실행 시 인자를 전달받을 수 있도록 `main`함수를 선언하는 것도 가능하며 인자를 전달하는 것도 가능하다.

###### `main_arg.c`
```c
#include <stdio.h>

int main(int argc, char **argv)
{
	printf("> # of string: %d\n", argc);

	for(int i = 0; i < argc; i++)
		printf("- %d: %s\n", i + 1, argv[i]);

	return 0;
}
```
```
./a.out abcd 1234

> # of string: 3
- 1: ./a.out
- 2: abcd
- 3: 1234
```

### 2) 인자의 형성 과정
- [[💻 Projects/Computer/C/C#main_arg c]]에서, 실행을 위해 `./a.out abcd 1234`라는 명령문을 전달하였다. 
	- `./a.out`는 실행시킬 파일을 특정한다.
	- `abcd`, `1234`는 `main`함수로 전달되는 인자이다.
- 이러한 형태로 `./a.out`을 실행시키면 인자들이 문자열 배성으로 구성되어 `main`함수의 인자로 전달된다.
	- 문자열은 **공백**을 기준으로 나뉘게 되므로, 다음의 총 $3$개의 문자열을 형성한다.
		- `"./a.out"`
		- `"abcd"`
		- `"1234"`
	- 문자열의 개수가 $3$개이므로 문자열을 저장할 배열의 길이는 $3$이 된다.
		- 배열의 각 요소는 문자열을 가리킬 주소 값을 지니게 되고, 최종적으로 **이 배열이 `main`함수의 두 번째 인자로 전달된다.**
		- 문자열을 인자로 전달할 때 큰 따옴표를 사용하면 공백을 포함하고 있는 문자열도 전달할 수 있다.
	- `main`함수의 첫 번째 인자(`argc`)로 전달되는 것은 **문자열의 개수**다.
	
	
###### `private_arg.c`
```c
#include <stdio.h>

int main(int argc, char * argv[])
{
	if(argc != 3)
	{
		printf(">> Input Error! Usage:\n./a.out <name> <private_number>\n");
		return 1;
	}

	printf("> name          : %s\n", argv[1]);
	printf("> private_number: %s\n", argv[2]);

	return 0;
}
```
```
./a.out "Jasmin Song" 940918
> name          : Jasmin Song
> private_number: 940918
```
```
./a.out "Jasmin Song" 9339 39993
>> Input Error! Usage:
./a.out <name> <private_number>
```



