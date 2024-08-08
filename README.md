# Dart 시작하기

- [Dart 시작하기](#dart-----)
- [0. Introduction](#0-introduction)
  - [0.1 Why `dart`](#01-why--dart-)
  - [0.2 How To Learn](#02-how-to-learn)
- [1. VARIABLES](#1-variables)
  - [1.0 Hello World](#10-hello-world)
  - [1.1 The Var Keyword](#11-the-var-keyword)
  - [1.2 Dynamic Type](#12-dynamic-type)
  - [1.3 Nullable Variables](#13-nullable-variables)
  - [1.4 Final Variables](#14-final-variables)
  - [1.5 Late Variables](#15-late-variables)
  - [1.6 Constant Variables](#16-constant-variables)
  - [1.7 Recap](#17-recap)
- [2. DATA TYPES](#2-data-types)
  - [2.0 Basic Data Types](#20-basic-data-types)
  - [2.1 Lists](#21-lists)
  - [2.2 String Interpolation](#22-string-interpolation)
  - [2.3 Collection For](#23-collection-for)
  - [2.4 Maps](#24-maps)
  - [2.5 Sets](#25-sets)
- [3. FUNCTIONS](#3-functions)
  - [3.0 Defining a Function](#30-defining-a-function)
  - [3.1 Named Parameters](#31-named-parameters)
  - [3.3 Optional Positional Parameters](#33-optional-positional-parameters)
  - [3.4 QQ Operator](#34-qq-operator)
  - [3.5 Typedef](#35-typedef)
- [4. CLASSES](#4-classes)
  - [4.0 Your First Dart Class](#40-your-first-dart-class)
  - [4.1 Constructors](#41-constructors)
  - [4.2 Named Constructor Parameters](#42-named-constructor-parameters)
  - [4.3 **Named Constructors**](#43---named-constructors--)
  - [4.4 Recap](#44-recap)
  - [4.5 Cascade Notaion](#45-cascade-notaion)
  - [4.6 Enums](#46-enums)
  - [4.7 Abstract Classes](#47-abstract-classes)
  - [4.8 Inheritance](#48-inheritance)
  - [4.9 Mixins](#49-mixins)

# 0. Introduction

## 0.1 Why `dart`

- `dart`의 컴파일러 기술을 사용해 다양한 방식으로 코드를 실행할 수 있다.
  - 기본 플랫폼
    - 모바일 및 데스크톱 장치를 대상으로 하는 앱의 경우
      -> JIT(Just-In-Time) 컴파일 기능이 있는 `dart` VM과 기계 코드 생성을 위한 AOT(Ahead-Of-Time) 컴파일러가 모두 포함되어 있다.
  - 웹 플랫폼
    - 웹을 대상으로 하는 앱의 경우
      -> 개발 또는 프로덕션 목적으로 컴파일할 수 있다.
      웹 컴파일러는 `dart`를 JavaScript로 변환한다.

## 0.2 How To Learn

- [`dart`pad](https://www.notion.so/Dart-7a122ff1f76549b89b32e84f9392430d?pvs=21)

# 1. VARIABLES

## 1.0 Hello World

- `main` 함수는 모든 `dart` 프로그램의 `Entry Point`이다.
- `main` 함수에서 작성한 코드가 호출되는 방식.

> [!NOTE]
> dart는 자동으로 세미콜론을 붙여주지 않기 때문에 직접 붙여주어야 한다.
> (일부러 세미콜론을 쓰지 않는 경우가 있기 때문)

## 1.1 The Var Keyword

- `dart`에서 변수를 어떻게 만드는가?

1. 관습적으로 함수나 메서드 내부에 `지역 변수`를 선언할 때는 `var`를 사용한다.

   ```dart
   void main() {
   	var name = '니꼬';
   	name = 'nico';
   }

   ```

2. `class`에서 변수나 `property`를 선언할 때에는 `타입`을 지정해준다.

   ```dart
   void main() {
   	String name = '니꼬';
   	name = 'nico';
   }

   ```

## 1.2 Dynamic Type

- `Dynamic`: 여러가지 타입을 가질 수 있는 변수에 쓰는 키워드
  - 왜 사용하는가?
    : 변수가 어떤 타입일지 알기 어려운 경우가 존재함
  ```dart
  void main() {
  	dynamic name;
  	name = 'nico';
  	name = 12;
  	name = true;
  	...
  }
  ```
  ```dart
  void main() {
  	dynamic name;
  	if (name is String) {
  		...
  	}
  	if (name is int) {
  		...
  	}
  }
  ```
- 조건문을 통해 `name`이 `String`/`int`, ...임을 알 수 있다.

## 1.3 Nullable Variables

- `null safety`
  - 개발자가 `null` 값을 참조할 수 없도록 하는 것
  - 어떤 변수, 혹은 데이터가 `null`이 될 수 있음을 명시하는 것

```dart
// Without null safety:
bool isEmpty(String string) => string.length == 0;

main() {
	isEmpty(null);
}
```

- `null safety` 가 없는 버전에서 이 코드를 실행하면 런타임 에러가 발생함
  > null에는 length 메서드가 없기 때문에 NoSuchMethodError가 발생함

```dart
void main() {
	String nico = 'nico';
	// nico = null; (x)

	String? jeongmok = 'jeongmok';
	jeongmok = null; (o)

	jeongmok?.isNotEmpty;
	if (jeongmok != null) {
		jeongmok.isEmpty;
	}
```

- 변수명 뒤에 `?`를 붙임으로써 `dart`에게 그 변수가 `null`이 될 수도 있음을 알려줄 수 있다.

## 1.4 Final Variables

- `JavaScript`의 `const`와 비슷하게 수정할 수 없는 변수를 만들 수 있다.
  ```dart
  void main() {
  	final name = 'nico';
  	// name = 'jeongmok' (x)
  }
  ```

## 1.5 Late Variables

- `late`는 `var` 앞에 붙일 수 있는 수식어다.
  - `late`를 붙이면 초기 데이터 없이 변수를 선언할 수 있게 해준다.
    ```dart
    void main() {
    	late final name;
    	// do something, go to api, ...
    	name = 'nico';
    }
    ```
    > 필요한 데이터가 어떤 데이터인지 모르는 경우 사용하기 좋다.

## 1.6 Constant Variables

- `JavaScript`나 `TypeScript`의 `const`는 `dart`의 `final`과 비슷하다.
  - `dart`의 `const`는 `compile-time constant`를 만들어준다.
    > compile-time constant: 컴파일이 되는 시점에 그 값을 알 수 있는 상수
  - `const`는 `final`과 같이 수정이 불가능하다.
  - `const`에서 가장 중요한 것은, `compile-time`에 알고 있는 값이어야 한다.
    ```dart
    void main() {
    	const API_KEY = 123456;
    	// API_KEY = 987654; (x)
    }
    ```
    - `API_KEY`는 바뀌지 않을 것이고, **컴파일이 될 때 그 값을 알고 있을 것**이다.
    ```dart
    void main() {
    	// const API_KEY = fetchAPI(); (x)
    	final API_KEY = fetchAPI();
    }
    ```
    - **`API`로부터 데이터를 받아와 변수에 저장**하는 것과 같은 경우에는, 컴파일하는 시점에 `API_KEY` 변수의 값을 모르기 때문에 `const`로 선언하면 안되고 `final`로 선언해야 한다.
      - 또한 **사용자가 화면에서 입력해야 하는 값**과 같은 경우에도 `const`가 아닌 `final`이나 `var`을 사용해야 한다.

## 1.7 Recap

- 변수 선언 방법들

  ```dart
  void main() {

  	// Type을 지키는 선에서 수정이 가능한 변수
  	// var을 가능한 한 많이 사용하는 것을 권장함(어차피 컴파일러가 Type을 추론)
  	int i = 1;
  	var name = 'nico';

  	// 수정이 불가능한 변수
  	final name = 'jeongmok';

  	// 여러 Type을 가질 수 있는 변수
  	dynamic name;

  	// 컴파일할 때 알고 있는 변수
  	const max_allowed_width = '100';

  	// null 값을 참조하지 못하게 하는 변수
  	// (변수가 null일 수도 있다고 알려주는 방법)
  	String? name = 'jeongmok2';

  	// 데이터를 나중에 넣을 수 있는 변수
  	// flutter로 API에서 데이터를 가져오는 작업에 합리적이다.
  	late final String name;
  }
  ```

# 2. DATA TYPES

## 2.0 Basic Data Types

```dart
void main() {
	String name = 'nico';
	bool alive = true;
	int age = 12;
	double money = 100;

	// num 은 int일 수도 있고, double일 수도 있다.
	// int와 double의 부모 class
	num x = 20;
	x = 1.1;
}
```

> 위의 기본 자료형을 포함한 대부분의 자료형은 object, class로 이루어져 있기 때문에 실제 자료형 안에 어떤 게 들어있는지 볼 수 있다.
> (함수도 객체임)

## 2.1 Lists

```dart
void main() {
	// 리스트 선언 방법
	var list1 = [
		1,
		2,
		3,
	];
	List<int> list2 = [
		1,
		2,
		3,
	];
	// numbers.add('a'); (x)
}
```

- `dart`는 `collection if`와 `collection for`을 지원한다.
  ```dart
  void main() {
  	var giveMeFive = true;
  	var numbers = [
  		1,
  		2,
  		3,
  		4,
  		if (giveMeFive) 5,
  	];
  	print(numbers);
  }
  ```
  ```
  [1, 2, 3, 4, 5]
  ```

## 2.2 String Interpolation

- `String interpolation`
  - `text`에 변수를 추가하는 방법
    ```dart
    void main() {
    	var name = 'nico';
    	var greeting = 'Hello everyone, my name is $name, nice to meet you!';
    	print(greeting);
    }
    ```
    ```
    Hello everyone, my name is nico, nice to meet you!
    ```
    - 원하는 부분에 `$`와 변수 이름을 적어주면 된다.
      (변수가 이미 존재하는 경우 사용)
  - 계산을 할 때의 문법
    ```dart
    void main() {
    	var name = 'nico';
    	var age = 10;
    	var greeting = 'Hello everyone, my name is $nico and I\\'m ${age + 2}';
    	print(greeting);
    }
    ```
    ```
    Hello everyone, my name is nico and I'm 12
    ```

## 2.3 Collection For

```dart
void main() {
	var oldFriends = ['nico', 'lynn'];
	var newFriends = [
		'lewis',
		'ralph',
		'darren',
		for(var friend in oldFriends) "❤️ $friend"
	];
	print(newFriends);
}
```

```
[lewis, ralph, darren, ❤️ nico, ❤️ lynn]
```

## 2.4 Maps

```dart
void main() {
	var player1 = {
		'name': 'nico',
		'xp': 19.99,
		'superpower': false',
	};

	// key값과 value값의 Type을 지정할 수 있다.
	Map<int, bool> player2 = {
		1: true,
		2: false,
		3: true,
	};

	// 복잡한 Map 생성
	Map<List<int>, bool> player3 = {
		[1, 3, 5]: true,
		[2, 4, 6]: false,
	};

	// Map List(차라리 class를 사용하는게 나음)
	List<Map<String, Object>> player4 = [
		{
			{'name': 'nico', 'xp': 199.99},
		},
	];
}
```

```dart
// Map 생성자를 사용해 동일한 객체를 만들 수 있음
void main() {
	var fruits = Map();
	fruits['first'] = 'apple';
	fruits['second'] = 'banana';
	fruits['third'] = 'orange';
	print(fruits);
}
```

```
{first: apple, second: banana, third: orange}
```

## 2.5 Sets

```dart
void main() {
	var numbers = {1, 2, 3, 4};
	numbers.add(1);
	numbers.add(1);
	numbers.add(1);
	numbers.add(1);
	print(numbers);
}
```

```dart
{1, 2, 3, 4}
```

- `List`와 유사하지만, 그 안에 있는 요소가 `unique`해야 한다.

# 3. FUNCTIONS

## 3.0 Defining a Function

```dart
// void는 아무것도 return하지 않음, parameter의 Type은 String, 이름은 name
void sayHello1(String name) {
	print("Hello $name nice to meet you!");
}

// return시킬 Type을 정해주고, return을 해주면 된다.
String sayHello2(String name) {
	return "Hello $name nice to meet you!";
}

// fat arrow syntax로 곧바로 return 시키는 방법(한 줄짜리를 return할 때)
String sayHello3(String name) => "Hello $name nice to meet you!";

void main() {
	print(sayHello2('nico'));
}

```

```
Hello nico nice to meet you!

```

## 3.1 Named Parameters

```dart
// 별로 좋지 않은 방법
String sayHello(String name, int age, String country) {
	return "Hello $name, you are $age and you come from $country";
}

void main() {
	print(sayHello('nico', 19, 'cuba'));
}
```

```dart
// named argument 활용하기(중괄호 추가)
String sayHello({
	String name,
	int age,
	String country,
}) {
	return "Hello $name, you are $age and you come from $country";
}

// 순서에 상관없이 argument의 요소들을 적어주면 된다.
void main() {
	print(sayHello(
		age: 19,
		country: 'cuba',
		name: 'nico'
	));
}
```

- 하지만 아래의 경우와 같이 `say Hello function` 안에 있는 모든 요소를 적지 않을 수 있다.

  ```dart
  void main() {
  	print(sayHello(
  		age: 12,
  	));
  }

  void main() {
  	sayHello();
  }
  ```

1. `named argument`에 `default value` 정하기

   ```dart
   String sayHello({
   	String name = 'anon',
   	int age = 99,
   	String country = 'wakanda',
   }) {
   	return "Hello $name, you are $age and you come from $country";
   }
   ```

2. 유저에게 실제 `data`를 받아야 할 때, `required`를 붙이기

   ```dart
   String sayHello({
   	requried String name,
   	requried int age,
   	requried String country,
   }) {
   	return "Hello $name, you are $age and you come from $country";
   }
   ```

## 3.3 Optional Positional Parameters

```dart
String sayHello(
	String name,
	int age,
	String country,
	) =>
		'Hello $name, you are $age years old from $country';

void main() {
	sayHello('nico', 12, 'cuba');
}
```

- 현재 `sayHello function`을 호출하려면 `name, age, country` 순으로 `parameter`들을 전달해야 한다.

  - 여기서 `named argument`를 적용하지 않고 `country`는 `required`하지 않게 하려면 어떻게 해야 할까?

    ```dart
    String sayHello(
    	String name,
    	int age,
    	[String? country = 'cuba'],
    	) =>
    		'Hello $name, you are $age years old from $country';

    void main() {
    	sayHello('nico', 12);
    }
    ```

    - `country` 필드에 대괄호를 씌운 뒤, `?`를 통해 `null`값일 수도 있음을 알리고 `default value`를 넣어주면 된다.

## 3.4 QQ Operator

```dart
String capitalizeName(String name) => name.toUpperCase();

void main() {
	capitalizeName('nico');
}
```

- `name`을 받으면 이를 대문자로 바꿔주는 함수를 만들어보자.

  - 이때, `null`값도 넣을 수 있게 하고 싶다.

  ```dart
  String capitalizeName(String? name) => name.toUpperCase();

  void main() {
  	capitalizeName('nico');
  	capitalizeName(null);
  }
  ```

  - 단순히 `String?`을 적용하게 되면, `null`이 될 수도 있는 값에 메서드를 적용할 수 없기 때문에 불가능하다. 이를 해결하는 방안들이 있다.

    ```dart
    // 긴 버전
    String capitalizeName(String? name) {
    	if (name != null) {
    		return name.toUpperCase();
    	}
    	return "ANON";
    }

    // fat arrow syntax 활용 버전
    String capitalizeName(String? name) =>
    	 name != null ? name.toUpperCase() : "ANON";

    // QQ Operator 활용 버전
    String capitalizeName(String? name) =>
    	name?.toUpperCase() ?? "ANON";
    ```

    - `QQ Operator`는 좌항이 `null`이면 `"ANON"`을 `return`하고, 좌항이 `null`이 아니면 그대로 좌항을 `return`한다.
    - 이때 `name` 자체가 `null`인 경우에는 메서드 호출이 불가능하기 때문에 `name?`으로 적어준다.

- `QQ equals`/`QQ assignment operator`
  ```dart
  void main() {
  	String? name;
  	name ??= 'nico';
  	// name ??= 'another'; (이미 name='nico' 이므로 오류 발생)
  }
  ```
  - `name`이 `null`이라면 할당할 값을 적어주면 된다.

## 3.5 Typedef

```dart
List<int> reverseListOfNumbers(List<int> list){
	var reversed = list.reversed;
	return reversed.toList();
}

void main() {
	...
}
```

- `typedef`를 활용해 자료형에 원하는 `alias`를 붙일 수 있다.(자료형 이름의 별명을 만듦)

  ```dart
  typeofdef ListOfInts = List<int>;

  ListOfInts reverseListOfNumbers(ListOfInts list) {
  	var reversed = list.reversed;
  	return reversed.toList();
  }
  ```

# 4. CLASSES

## 4.0 Your First Dart Class

```dart
// Player1 class 선언(Type 명시를 반드시 해주어야 함)
class Player1 {
	String name = 'nico';
	int xp = 1500;

	void sayHello() {
		// class method 내에서의 this는 사용하지 않는 것이 권고됨
		print("Hi my name is $name");
	}
}

// Player2 class 선언
class Player2 {
	final country = 'korea';
	final age = 20;
}

void main() {
	// Player instance 생성
	var player1 = Player1();
	var player2 = Player2();

	// class 내의 property 변경 가능
	player1.name = 'jeongmok';

	// final으로 선언 시 변경 불가
	// player2.country = 'Japan'; (x)

	player1.sayHello();
}
```

```
"Hi my name is nico"
```

## 4.1 Constructors

```dart
class Player {
	late final String name;
	late int xp;

	Player(String name, int xp) {
		this.name = name;
		this.xp = xp;
	}

	void sayHello() {
		print("Hi my name is $name");
	}
}

void main() {
	var player = Player("nico", 1500);
	player.sayHello();
	var player2 = Player("jeongmok", 1000);
	player2.sayHello();
}
```

- 위 코드를 줄여서 작성할 수 있다.

  ```dart
  class Player {
  	final String name;
  	int xp;

  	Player(this.name, this.xp);

  	void sayHello() {
  		print("Hi my name is $name");
  	}
  }
  void main() {
  	var player = Player("nico", 1500);
  	player.sayHello();
  	var player2 = Player("jeongmok", 1000);
  	player2.sayHello();
  }
  ```

## 4.2 Named Constructor Parameters

```dart
class Player {
	final String name;
	int xp;
	String team;
	int age;

	Player(this.name, this.xp, this.team, this.age);

	void sayHello() {
		print("Hi my name is $name");
	}
}

void main() {
	var player = Player("nico", 1500, 'red', 12);
	player.sayHello();
	var player2 = Player("jeongmok", 1000, 'blue', 12);
	player2.sayHello();
}
```

- 너무 많은 `positinal argument`가 서로 붙어있으면 헷갈리게 된다.

  ```dart
  class Player {
  	final String name;
  	int xp;
  	String team;
  	int age;

  	Player({
  		required this.name,
  		required this.xp,
  		required this.team,
  		required this.age,
  	 });

  	void sayHello() {
  		print("Hi my name is $name");
  	}
  }

  void main() {
  	var player = Player(
  		name: "nico",
  		xp: 1500,
  		team: 'red',
  		age: 12,
  	);
  	player.sayHello();
  	var player2 = Player(
  		name: "jeongmok",
  		xp: 1000,
  		team: 'blue',
  		age: 12,
  	);
  	player2.sayHello();
  }
  ```

## 4.3 **Named Constructors**

```dart
class Player {
	final String name;
	int xp, age;
	String team;

	Player({
		required this.name,
		required this.xp,
		required this.team,
		required this.age,
	 });

	// Player를 초기화하는 메서드 선언
	Player.createBluePlayer({
		required String name,
		required int age,
		)}  : this.age = age,
					this.name = name,
				  this.team = 'blue',
				  this.xp = 0;

	Player.createRedPlayer({
		String name,
		int age,
		)}  : this.age = age,
					this.name = name,
					this.team = 'red,
					this.ep = 0;

	void sayHello() {
		print("Hi my name is $name");
	}
}

void main() {
	var player = Player.createBluePlayer(
		name: "nico",
		age: 12,
	);
	player.sayHello();

	// named syntax를 사용하지 않고 positional syntax를 사용
	var player2 = Player.createRedPlayer(
		"jeongmok",
		12,
	);
	player2.sayHello();
}
```

- `createBluePlayer` 메서드는 `name`과 `age` 의 `named` 된 파라미터를 받고 있다.

  - 그리고 `:` 는 `Player` 클래스를 초기화해준다.
    <aside>
    💡 https://dart.dev/tools/linter-rules/prefer_initializing_formals

    </aside>

    - `Named Constructor`에서의 `syntactic sugar`(편의 문법)

      ```dart
      // Named parameters
      // 일반적인 방법
      Player.createBlue({
      	required String name,
      	required int xp
      })  : this.name = name,
      			this.xp = xp,
      			this.team = 'blue';

      // 간소화된 방법(dart는 간소화된 방법을 추천)
      Player.createRed({
      	required this.name,
      	required this.xp,
      	this.tem = 'red',
      });
      ```

    - `Positional parameters`에서의 `syntactic sugar`(편의 문법)

      ```dart
      // Positional parameters
      // 일반적인 방법
      Player.createRed(String name, int xp)
      	: this.name = name,
      		this.xp = xp,
      		this.team = 'red';

      // 간소화된 방법
      Player.createRed(
      	this.name,
      	this.xp,
      	[this.team = 'red']
      );
      ```

## 4.4 Recap

- API로부터 여러 Player가 들어있는 목록(`List`)을 받는다고 가정해보자.

  ```dart
  class Player {
    final String name;
    int xp;
    String team;

    Player.fromJson(Map<String, dynamic> playerJson)
        : name = playerJson['name'],
          xp = playerJson['xp'],
          team = playerJson['team'];

    void sayHello() {
      print("Hi my name is $name");
    }
  }

  void main() {
    var apiData = [
      {
        "name": "nico",
        "team": "red",
        "xp": 0,
      },
      {
        "name": "lynn",
        "team": "red",
        "xp": 0,
      },
      {
        "name": "dal",
        "team": "red",
        "xp": 0,
      },
    ];

    apiData.forEach((playerJson) {
      var player = Player.fromJson(playerJson);
      player.sayHello();
    });
  }
  ```

## 4.5 Cascade Notaion

```dart
class Player {
  String name;
  int xp;
  String team;

	Player({
		required this.name,
		required this.xp,
		required this.team,
	});

  void sayHello() {
    print("Hi my name is $name");
  }
}

void main() {
	var nico = Player(name: 'nico', xp: 1200, team: 'red');
	nico.name = 'las';
	nico.xp = 120000;
	nico.team = 'blue';
}
```

- 위의 코드처럼 `nico`라는 변수의 필드를 `변수명.필드명`처럼 바꾸려면 매우 귀찮다.
  ```dart
  void main() {
  	var nico = Player(name: 'nico', xp: 1200, team: 'red');
  		..name = 'las'
  		..xp = 120000
  		..team = 'blue'
  }
  ```
  - `..name`에서 첫 번째 `.`은 `nico`를 가리킨다.

## 4.6 Enums

```dart
enum Team { red, blue }
enum XPLevel { low, mid, high }

class Player {
	String name;
	XPLevel xp;
	Team team;

	Player({
		required this.name,
		required this.xp,
		required this.team,
	});

	void sayHello() {
    print("Hi my name is $name");
  }
}

void main() {
	var nico = Player(
		name: 'nico',
		xp: XPLevel.low,
		team: Team.red
	);

	var lynn = Player(
		name: 'lynn',
		xp: XPLevel.high,
		team: Team.blue
	);
}
```

- `enum` 타입을 만들어 코드를 작성할 때 실수를 줄일 수 있다.

## 4.7 Abstract Classes

- `Abstract Class`(추상화 클래스)는 다른 클래스들이 직접 구현해야 하는 메서드들을 모아놓은 일종의 청사진이다.

  ```dart
  // 추상화 클래스 선언
  abstract class Human {
  	// walk라는 메서드 선언(기능 구현 x)
  	void walk();
  }

  enum Team { red, blue }
  enum XPLevel { low, mid, high }

  // 추상화 클래스 상속/확장
  class Player extends Human {
  	String name;
  	XPLevel xp;
  	Team team;

  	Player({
  		required this.name,
  		required this.xp,
  		required this.team,
  	});

  	// 추상화 클래스 메서드의 기능 구현
  	@override
  	void walk() {
  		print("Player is walking");
  	}

  	void sayHello() {
  		print("Hi my name is $name");
  	}
  }

  // 추상화 클래스 상속/확장
  class Coach extends Human {
  	// 추상화 클래스 메서드의 기능 구현
  	@override
  	void walk() {
  		print("Coach is walking");
  	}
  }

  void main() {
  	var nico = Player(
  		name: 'nico',
  		xp: XPLevel.low,
  		team: Team.red,
  	);

  	var lynn = Player(
  		name: 'lynn',
  		xp: XPLevel.high,
  		team: Team.blue,
  	);

  	// sayHello 메서드 호출
  	nico.sayHello();
  	lynn.sayHello();
  }

  ```

  - 추상화 클래스를 선언할 때에는 기능을 따로 구현하지 않는다.

    - 대신 어떤 클래스에서 추상화 클래스를 확장해준다.

      - 그리고 메서드의 기능을 구현해준다.
        <aside>
        💡 상속/확장을 하는 이유는 상속/확장한 메서드가 클래스에 존재해야만 한다는 것이고, 이 메서드의 기능을 클래스마다 원하는 대로 구현할 수 있다.

        </aside>

## 4.8 Inheritance

```dart
class Human {
  String name;

	// 생성자
  Human(this.name);
  void sayHello() {
    print("Hi my name is $name");
  }
}

enum Team { red, blue }

class Player extends Human {
  final Team team;

  Player({
    required this.team,
    required String name,
  }) : super(name);

  @override
  void sayHello() {
    super.sayHello();
    print('and I play for ${team.name}');
  }
}

void main() {
  var player = Player(team: Team.red, name: 'nico');
  player.sayHello();
}
```

- 부모 클래스(`Human`)가 생성자를 포함하고 있을 때, 이 클래스를 사용하기 위해서는 필요한 값을 전달하고 그 부모 클래스의 생성자를 `super`로 호출해야 한다.

## 4.9 Mixins

- `Mixins`는 다른 클래스의 메서드와 속성을 포함하여 새로운 클래스를 정의할 수 있는 방법이다.

  - 자바의 **다중 속성**과 유사한 기능을 제공할 수 있다.
  - `with` 키워드를 사용해 클래스 정의에 추가할 수 있다.

    ```dart
    class Strong {
      final double strengthLevel = 1500.99;
    }

    class QuickRunner {
      void runQuick() {
        print("ruuuuuuuuuuun!");
      }
    }

    class Tall {
      final double height = 1.99;
    }

    enum Team { red, blue }

    class Player with Strong, QuickRunner, Tall {
      final Team team;

      Player({
        required this.team,
      });
    }

    void main() {
      var player = Player(
        team: Team.red,
      );
      player.runQuick(); // mixin으로 추가된 메서드 호출
      print("Player strength: ${player.strengthLevel}");
      print("Player height: ${player.height}");
    }
    ```
