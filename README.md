# 이대환 (202530119) 
# 2025-11-06 강의
## 자바 모듈과 패키지 개념 및 활용

## 1️⃣ 패키지 개념과 필요성

### ▪ 개념
- **패키지(package)**  
  → 서로 관련된 클래스와 인터페이스를 하나의 디렉터리 구조로 묶어 관리하는 단위  
  → 컴파일된 `.class` 파일들이 같은 패키지 폴더에 저장됨  
- 하나의 응용 프로그램은 **여러 개의 패키지로 구성**될 수 있음  
- 패키지는 `.jar` 파일로 **압축 가능**

### ▪ 필요성
- 서로 다른 개발자가 **동일한 클래스 이름**을 사용할 수 있음  
- 프로젝트를 합칠 때 **이름 충돌** 문제 발생 가능  
- 패키지를 이용하면 **디렉터리별로 클래스 관리** 가능  
  → 동일 이름의 클래스라도 **경로명이 다르면 별개 클래스**

📁 예시:
```

com.company.ui.Tool
com.company.db.Tool

```
→ 이름은 같지만, 서로 다른 패키지이므로 충돌하지 않음

---

## 2️⃣ 모듈(module)

### ▪ 개념
- 여러 **패키지 + 리소스(이미지, 설정 등)** 를 묶은 **컨테이너**
- 하나의 모듈은 **하나의 `.jmod` 파일**로 저장됨
- **Java 9부터 도입**

### ▪ 자바 플랫폼의 모듈화
- **Java 8까지**: 모든 API가 `rt.jar` 하나에 포함  
- **Java 9부터**: 자바 API를 **다수의 모듈(약 99개 → 현재 약 70개)** 로 분할

### ▪ 응용프로그램의 모듈화
- 클래스 → 패키지 → 모듈  
- 즉, 여러 패키지를 하나의 모듈로 구성 가능

---

## 3️⃣ 자바 모듈화의 목적

- **필요한 모듈만 포함한 경량 실행 환경 제공**
  - 소형 기기나 제한된 환경에서 메모리 낭비 최소화
- **보안 강화**  
  - 모듈 간 접근 제한을 명확히 설정 가능
- **유지보수 및 관리 용이**

💡 정리:
| 구분 | Java 8 이전 | Java 9 이후 |
|------|--------------|--------------|
| 구조 | `rt.jar` 하나 | 여러 개의 `.jmod` 파일 |
| 단위 | 패키지 중심 | 모듈 중심 |
| 장점 | 단순 | 효율적, 경량화 가능 |

---

## 4️⃣ 자바의 모듈 파일

- 위치: **`JDK 설치 디렉터리의 jmods 폴더`**
- 확장자: **`.jmod`**
- 포맷: **ZIP 압축 포맷**
- 포함 내용:
  - 자바 API 클래스
  - 패키지 및 리소스 파일

📦 예시:
```

C:\Program Files\Java\jdk-17\jmods\java.base.jmod

````

---

## 5️⃣ 패키지 사용하기 (import)

### ▪ import 없이 사용
→ 클래스의 **완전 경로명**을 작성해야 함
```java
java.util.Scanner sc = new java.util.Scanner(System.in);
````

### ▪ 특정 클래스 import

```java
import java.util.Scanner;  // Scanner 클래스만 가져옴
```

### ▪ 패키지 전체 import

```java
import java.util.*;  // java.util 패키지의 모든 클래스
```

⚠️ 단, **하위 패키지는 포함되지 않음**

예:
`import java.util.*;` → `java.util.Date` 가능
❌ `java.util.stream.*` 은 포함되지 않음

---

## 6️⃣ 패키지 만들기

### ▪ 클래스 파일 저장 위치

* 클래스나 인터페이스가 컴파일되면 `.class` 파일 생성
* 패키지명과 동일한 디렉터리에 저장됨

### ▪ 패키지 선언

* 자바 파일의 **맨 위에 작성**
* 해당 클래스가 저장될 **디렉터리 지정**

```java
package UI;

public class Tool {
    public void show() {
        System.out.println("UI Tool");
    }
}
```

컴파일 시:

```
UI 디렉터리 내에 Tool.class 생성
```

---

## 7️⃣ 디폴트 패키지 (default package)

* `package` 선언문이 **없는 클래스**는 **디폴트 패키지**에 포함
* 컴파일러가 자동으로 현재 디렉터리를 패키지로 간주
* 소규모 프로그램(실습, 테스트 등)에만 사용 권장
  → 실제 프로젝트에서는 명시적 패키지 선언이 필수

---

### ⚡정리 요약

| 구분              | 설명                            |
| --------------- | ----------------------------- |
| 패키지             | 클래스 묶음 (디렉터리 구조)              |
| 모듈              | 패키지 + 리소스 묶음 (컨테이너)           |
| 확장자             | `.jar` (패키지 압축), `.jmod` (모듈) |
| import          | 다른 패키지 클래스 사용                 |
| default package | package 선언 없는 경우 현재 디렉터리      |

---

📚 **기억 포인트**

* `Java 9` → 모듈 시스템 도입 (`.jmod`)
* `rt.jar` → 사라지고, `jmods` 폴더 등장
* `import java.util.*;` → 하위 패키지 포함 ❌
* `package` → 클래스가 저장될 디렉터리 지정

---
![테크페어](img/1106.jpg)
![테크페어2](img/1106_2.jpg)

# 2025-10-23 강의

## 1. 객체란?
- 객체(Object): **속성(state)과 행위(behavior)를 가지는 실체**  
- 클래스(Class)라는 설계도로부터 생성되는 구체적인 실체  
- 프로그램 실행 중 메모리에 생성되며, **인스턴스(instance)**라고도 부름  

**예시**
```java
class Car {  // 클래스
    String color; // 속성
    void drive() { System.out.println("운전 중"); } // 행위
}

Car myCar = new Car(); // 객체 생성
myCar.color = "빨강";
myCar.drive();
```


## 2. 자바의 객체 지향 특성

### 2-1. 캡슐화(Encapsulation)

* **정의**: 객체의 내부를 숨기고 필요한 인터페이스만 공개
* **목적**: 데이터 보호, 잘못된 접근 방지
* **자바 구현**

  * `private` 필드 + `public` 메소드 접근

```java
class Person {
    private String name; // 외부 접근 차단
    public void setName(String n){ name = n; }
    public String getName(){ return name; }
}
```

### 2-2. 상속(Inheritance)

* **정의**: 상위 클래스의 속성과 기능을 하위 클래스가 물려받음
* **자바 용어**

  * 상위 클래스: **Super class**
  * 하위 클래스: **Sub class**
* **예시**

```java
class Animal { void eat(){ System.out.println("먹는다"); } }
class Dog extends Animal { void bark(){ System.out.println("짖는다"); } }

Dog d = new Dog();
d.eat(); // Animal 클래스 기능 상속
d.bark();
```

### 2-3. 다형성(Polymorphism)

* **정의**: 같은 이름의 메소드가 상황에 따라 다르게 동작
* **종류**

  1. **메소드 오버로딩**: 같은 클래스 내에서 매개변수 다르게 사용
  2. **메소드 오버라이딩**: 상속 관계에서 메소드 재정의

```java
class Calculator {
    int sum(int a, int b){ return a+b; }          // 오버로딩
    double sum(double a, double b){ return a+b; }
}

class Animal { void sound(){ System.out.println("소리"); } }
class Cat extends Animal { 
    void sound(){ System.out.println("야옹"); }  // 오버라이딩
}
```

---

## 3. 객체 지향 언어의 목적

* 소프트웨어 재사용성 ↑, 생산성 ↑
* 절차 지향 프로그래밍과 비교
  | 구분 | 절차 지향 | 객체 지향 |
  |------|-----------|-----------|
  | 표현 방식 | 작업 순서 | 객체 간 상호작용 |
  | 구성 단위 | 함수 | 클래스/객체 |
  | 재사용 | 낮음 | 높음 |

---

## 4. 클래스와 객체

* **클래스**: 객체 설계도, 속성과 행위 선언
* **객체**: 클래스의 실체, 메모리에 생성

```java
class Circle {
    int radius;
    String name;

    public double getArea() {
        return 3.14 * radius * radius;
    }
}

Circle pizza = new Circle();
pizza.radius = 10; pizza.name = "자바피자";
System.out.println(pizza.name + "의 면적: " + pizza.getArea());
```

* **객체 배열**

```java
Circle[] circles = new Circle[3];
for(int i=0;i<3;i++) circles[i] = new Circle();
```

---

## 5. 생성자(Constructor)

* **정의**: 객체 초기화 메소드, 클래스 이름과 동일
* **특징**

  * 여러 개 작성 가능 (오버로딩)
  * 기본 생성자: 매개변수 없음, 자동 생성 가능

```java
class Circle {
    int radius;
    Circle(){ radius = 1; } // 기본 생성자
    Circle(int r){ radius = r; } // 매개변수 있는 생성자
}
```

* **this**

  * 객체 자신 참조
  * `this()`로 같은 클래스 다른 생성자 호출 가능 (첫 줄에서만)

---

## 6. 메소드

* **기본 타입 전달**: 값 복사, 원본 변경 없음
* **참조 타입 전달**: 객체/배열은 참조 전달

```java
void replaceSpaces(char[] arr){
    for(int i=0;i<arr.length;i++)
        if(arr[i]==' ') arr[i]=',';
}
```

* **메소드 오버로딩 조건**

  * 이름 동일, 매개변수 개수/타입 달라야 함
  * 리턴 타입만 다르면 오버로딩 불가

---

## 7. static 멤버

* **정의**: 클래스당 하나, 객체 간 공유
* **사용**

```java
class StaticSample {
    int n;          // non-static
    static int m;   // static

    void g() { }
    static void f() { }
}

// 접근
StaticSample.m = 3;
StaticSample.f();

StaticSample obj = new StaticSample();
obj.n = 5; // 객체 멤버
```

---

## 8. 접근 지정자

| 종류          | 접근 범위        |
| ----------- | ------------ |
| `private`   | 동일 클래스만      |
| `default`   | 같은 패키지       |
| `protected` | 패키지 + 상속 클래스 |
| `public`    | 모두           |

---

## 9. 객체 소멸과 가비지 컬렉션

* **Java**: JVM이 자동 관리, 개발자 직접 소멸 X
* **강제 가비지 요청**

```java
System.gc();
```

---

## 10. 패키지(Package)

* **정의**: 관련 클래스 모아 디렉터리 관리
* 접근 지정자 활용: 캡슐화 + 제한적 접근 허용

---

## 11. 요약 그림 (개념적)

```
클래스 ──> 객체(인스턴스)
          ↑
          | 상속
          ↓
      서브클래스
```

---

## 12. 주의점

* 객체 치환 = 참조 복사, 객체 복사 X
* 오버로드 실패 사례: 매개변수 시그니처 동일, 리턴 타입만 다름


# (10월 2일 강의)


## break
- 반복문 하나를 **즉시 종료**할 때 사용  
- **중첩 반복문**에서 break를 실행하면 **가장 가까운 반복문**만 벗어남
```java
for(int i=0;i<5;i++){
    for(int j=0;j<5;j++){
        if(j==2) break; // 안쪽 반복문만 종료
        System.out.println(i + "," + j);
    }
}
```

## 배열(Array)

* **동일 타입 데이터**를 순차적으로 저장하는 자료 구조
* **인덱스(index)**를 통해 각 원소에 접근 가능
* 반복문으로 처리하기 적합
* 배열 인덱스는 **0부터 시작**

```java
int[] intArray;         // 배열 선언
intArray = new int[5];  // 배열 생성 (원소 5개)
```

### 배열 선언과 생성

* **선언**: 배열 레퍼런스 변수 정의

  ```java
  int[] arr;  // or int arr[];
  ```
* **생성**: 메모리 공간 할당

  ```java
  arr = new int[5];
  ```
* **초기화**: 생성과 동시에 값 대입 가능

  ```java
  int[] arr = {1,2,3,4,5};
  ```

### 배열 원소 접근

```java
arr[0] = 10;   // 첫 번째 원소 접근
int value = arr[2]; // 세 번째 원소 읽기
```

* 선언만 하고 접근하면 오류 발생

```java
int[] arr;
arr[0] = 5; // ❌ 오류, 배열 생성 전 접근
```

### 레퍼런스 치환과 배열 공유

```java
int[] arr1 = new int[5];
int[] arr2 = arr1; // arr2와 arr1이 같은 배열 공유
arr2[0] = 100;
System.out.println(arr1[0]); // 100 출력
```

---

## 배열 크기 length

* 자바 배열은 객체이므로 `length` 필드 사용

```java
int[] arr = new int[5];
System.out.println(arr.length); // 5
```

---

## 배열과 for-each 문

* 배열 또는 나열(enumeration)의 **원소를 순차 접근**할 때 유용

```java
int[] arr = {1,2,3,4};
for(int n : arr){
    System.out.println(n);
}
```

---

## 2차원 배열

* 선언

```java
int[][] arr;
```

* 생성

```java
arr = new int[2][5]; // 2행 5열
```

* 접근

```java
arr[0][1] = 10; // 첫 번째 행, 두 번째 열
```

* length

```java
arr.length       // 행의 수
arr[0].length    // 첫 번째 행의 열의 수
```

---

## 메소드에서 배열 리턴

* **배열 레퍼런스만 반환**, 전체 복사 X
* 리턴 타입 배열 크기 지정 X, 타입만 맞추기

```java
int[] makeArray(){
    int[] arr = {1,2,3};
    return arr;
}
```

---

## 자바 예외 처리(Exception Handling)

* 예외 발생: 프로그램 실행 중 예상치 못한 오류
* 예: 0으로 나누기, 배열 범위 초과 등

### try-catch-finally 구조

```java
try {
    int result = 10 / 0; // 예외 발생
} catch(ArithmeticException e) {
    System.out.println("0으로 나눌 수 없습니다.");
} finally {
    System.out.println("항상 실행되는 블록");
}
```

### 배열 범위 벗어나기 예외

```java
int[] arr = new int[3];
try {
    arr[5] = 10; // ArrayIndexOutOfBoundsException 발생
} catch(ArrayIndexOutOfBoundsException e) {
    System.out.println("배열 범위를 벗어났습니다.");
}
```

---

### 정리 포인트

* `break`: 반복문 탈출
* 배열: 선언 → 생성 → 초기화 순서
* 2차원 배열: `arr.length`는 행, `arr[i].length`는 열
* 메소드에서 배열 리턴: **참조 반환**
* 예외 처리: `try-catch-finally`, 자주 쓰이는 예외 `ArithmeticException`, `ArrayIndexOutOfBoundsException`


# (9월 25일 강의)



## 반복문

### 1 for
- **조건 횟수가 정해져 있을 때** 사용  
- 조건식이 참인 동안 반복 실행
```java
for(int i=0; i<5; i++){
    System.out.println("i = " + i);
}
```

### 2 while

* **조건 횟수가 정해져 있지 않을 때** 사용
* 조건식이 참인 동안 반복 실행

```java
int i = 0;
while(i < 5){
    System.out.println(i);
    i++;
}
```

### 3 do-while

* 조건과 상관없이 **최소 한 번은 실행**

```java
int i = 0;
do {
    System.out.println(i);
    i++;
} while(i < 5);
```

### 4 중첩 반복

* 반복문 안에 또 다른 반복문 존재

```java
for(int i=0;i<3;i++){
    for(int j=0;j<3;j++){
        System.out.println(i + "," + j);
    }
}
```

---

## switch 문

* case 값과 일치하면 해당 case 실행
* `break` 만나면 switch 탈출
* 일치하는 값 없으면 `default` 실행 (선택적)

```java
int num = 2;
switch(num){
    case 1:
        System.out.println("1입니다");
        break;
    case 2:
        System.out.println("2입니다");
        break;
    default:
        System.out.println("기타");
}
```

### case 값 제한

* 허용: 문자, 정수, 문자열(JDK 1.7+)
* 허용 안됨: 실수

```java
case '+': break;
case 1: break;
case "예": break;
```

---

## 조건문

### 1 단순 if

```java
if(score >= 60){
    System.out.println("합격");
}
```

### 2 if - else

```java
if(score >= 60){
    System.out.println("합격");
} else {
    System.out.println("불합격");
}
```

### 3 다중 if - else

```java
if(score >= 90){
    System.out.println("A");
} else if(score >= 80){
    System.out.println("B");
} else {
    System.out.println("C");
}
```

* 조건이 많으면 `switch` 권장

---

## 연산자

### 1 대입 연산자

| 연산자  | 의미                 |            |
| ---- | ------------------ | ---------- |
| =    | 대입                 |            |
| +=   | 더한 후 대입            |            |
| -=   | 뺀 후 대입             |            |
| *=   | 곱한 후 대입            |            |
| /=   | 나눈 후 대입            |            |
| &=   | 비트 AND 후 대입        |            |
| ^=   | 비트 XOR 후 대입        |            |
|      | =                  | 비트 OR 후 대입 |
| <<=  | 왼쪽 시프트 후 대입        |            |
| >>=  | 오른쪽 시프트 후 대입       |            |
| >>>= | 부호 무시 오른쪽 시프트 후 대입 |            |

### 2 비교 연산자

| 연산자 | 의미        |
| --- | --------- |
| >   | 크다        |
| <   | 작다        |
| >=  | 크거나 같다    |
| <=  | 작거나 같다    |
| ==  | 같다 (값 비교) |
| !=  | 같지 않다     |

### 3 논리 연산자

| 연산자 | 의미              |
| --- | --------------- |
| &&  | 논리 AND          |
| ||  | 논리 OR           |
| !   | 논리 NOT          |
| ^   | 논리 XOR (배타적 OR) |

---

## 삼항 연산자

* 3개의 피연산자 사용

```java
int result = (score >= 60) ? 1 : 0; // score>=60이면 1, 아니면 0
```

* `if-else`를 한 줄로 간결하게 표현 가능

---

## 비트 연산

* 용도

  1. 데이터 압축 / 최적화
  2. 해싱 / 암호화
  3. 빠른 연산

```java
int a = 5;   // 0101
int b = 3;   // 0011
System.out.println(a & b);  // AND : 1 (0001)
System.out.println(a | b);  // OR  : 7 (0111)
System.out.println(a ^ b);  // XOR : 6 (0110)
System.out.println(~a);     // NOT : -6
System.out.println(a << 1); // 왼쪽 시프트 : 10
System.out.println(a >> 1); // 오른쪽 시프트 : 2
```

---

### 정리 포인트

* 반복문: `for`, `while`, `do-while`, 중첩 반복
* 조건문: `if`, `if-else`, `switch`
* 연산자: 대입, 비교, 논리, 삼항, 비트
* `switch` case 값은 문자/정수/문자열만 가능


# (9월 18일 강의)


## 자바의 특징
- 가비지 콜렉터(Garbage Collector, GC)
- 실기간 응용프로그램에 부적합
- 자바는 안전
- 프로그램 작성 쉬움
- 실행 속도 개선을위한 JIT 컴파일러 사용
    1. 바이드 코드를 인터프리터 방식 실행
    2. 기계어 보다 느림

## 코드 
1. 소스코드
    - `.java` 코드
    - 사람이 읽을 수 있는 고수준 언어 (High-Level Languag)
2. 바이코드
    - `.class` 코드
    - Java 컴파일러(javac)가 소스코드를 변환한 중간 코드
    - `JVM`이 실행 해야함 -> cpu가 실행 X
    - JIT 컴파일러가 기계어로 변환 실행
3. 기계어
    - cpu가 직접 실행 가능 - 0과 1의 이진 코드
    - 운영체제(os)와 cpu 아키텍처(intel , arm 등)에 따라 다름
    - 16진수 형태의 기계어

## 기본 구조
주석 / 클래스 생성/  main() 메서드/ 메서드 / 메소드 호출 / 변수 선언 / 문장 ; / 출력

### 식별자

- **정의** - 클래스 , 변수, 상수, 메소드에 붙이는 이름

- 유니코드 사용 가능, 한글 사용 가능 -> 한글 사용은 좋지 않다. 

- 자바의 언어 키워드는 식별자로 사용 불가

- 식별자의 첫 번째 문자로 숫자는 사용불가

- `_` , `$`를 식별자 첫번째 문자로 사용 할수는있다. 허나 일반적으로는 사용 안함

- 불릿 리터럴 `(true , false)`과 널 리터럴`(null)`은 식별자로 **사용불가**

- 길이 제한 없음

- 대소문자 구별 : `barChart` 와  `bahrchart`는 다른 식별자

## 데이터 타입
- 문자열은 기본 타입x, string 클래스로 문자열 표현

- 리터럴 : -> int a = `10` 에서 10 을 의미

- 문자열이나 문자열과 다른 자료형의 리터럴을 + 연산을 할 경우 결과는 문자열로 반환
- 객체를 참조하는 변수 유형, 힙(Heap) 영역에 저장된 객체의 메모리 주소를 가르킴
    - 기본 자료형은 스택 영역에 저장
- 객체를 참조 하지 않을 때 null 값을 가질수 있다.

- 일반적으로 `레퍼런스`라고 부른다.
## 참조 자료형 (Reference Type)
- 포인터는 임의의 메로리 주소를 저장 , 참조 자료형은 주소를 저장 X
- JVM이 해당 주소로 안내
- 객체를 참조하는 변수 휴형


## 메모리 관리
- jvm 이 관리 해준다.

## 메모리 구조

- 힙( heap - FIFO) 영역은 프로그래머가 직접 공간을 할당, 해제하는 메모리 공간, jvm이 담당
- 스택(stack - LIFO) 영역은 프로그램이 자동으로 사용하는 임시 메모리 영역
- 힙이 스택을 침범하는 경우를 힙 오버 플로우라고 한다. 
    - 스택이 힙을 침범하는 경우를 스택 오버 플로우

## 상수 선언
- final 키워드 사용
- 선언할 때 초기값 지정
- 실행 중 값 변경 불가능

## var 키워드
- type을 생략하고 변수 선언 
- 지역 변수에만 선언 가능 , class 필드에서는 사용할 수 없다.
    - 지역 변수 : 메소드 내부에 선언되는 변수.
    - 클래스 필드 : 클래스 내부에 선언되는 변수, 객체 생성과 함께 만들어지는 변수 
- 기본적으로는 명시적 자료형을 쓰는 것이 좋다


## print
- `System.out.print();`
- `System.out.println();`
- `System.out.printf();`


## 타입 변환
- 원래 타입보다 큰 타입으로 자동 변환
- 강제 변환
## java의 키 입력 
- System.in vs. Scanner
### Sysytem.in
- 키보드와 연결된 자바의 표준 입력 스트림
- 입력되는 키를 `바이트(문자 아님)로 리턴하는 저수준 스트림`
- 직접 사용하면 `바이트를 문자나 숫자로 변환하는 많은 어려움 있음`
### java.utill.Scanner
- 객체를 생성해서 사용
- 키보드에 연결된 System.in에게 키를 읽게 하고, 원하는 타입으로 변환하여 리턴
- 입력되는 키 값을 공백으로 구분되는 토큰 단위로 읽음
- 공백 문자 : `'/t' '/r' '/n' '' '/f'`(페이지 나누기, 폼 피드, 프린트 에서 사용)

## Scanner 주요 메서드
이런게 있다~

## 연산자
- 증감  
  - `++` : 변수 값을 1 증가  
  - `--` : 변수 값을 1 감소  

- 산술  
  - `+` : 더하기  
  - `-` : 빼기  
  - `*` : 곱하기  
  - `/` : 나누기  
  - `%` : 나머지  

- 시프트  
  - `>>` : 오른쪽 시프트 (부호 유지)  
  - `<<` : 왼쪽 시프트  
  - `>>>` : 오른쪽 시프트 (부호 무시, 0으로 채움)  

- 비교  
  - `>` : 크다  
  - `<` : 작다  
  - `>=` : 크거나 같다  
  - `<=` : 작거나 같다  
  - `==` : 같다 (값 비교)  
  - `!=` : 같지 않다  

- 비트  
  - `&` : 비트 AND  
  - `|` : 비트 OR  
  - `^` : 비트 XOR  
  - `~` : 비트 NOT  

- 논리  
  - `&&` : 논리 AND (그리고)  
  - `||` : 논리 OR (또는)  
  - `!` : 논리 NOT (부정)  
  - `^` : 논리 XOR (배타적 OR)  

- 조건  
  - `? :` : 조건 연산자 (삼항 연산자)  

- 대입  
  - `=` : 대입  
  - `*=` : 곱 후 대입  
  - `/=` : 나눈 후 대입  
  - `+=` : 더한 후 대입  
  - `-=` : 뺀 후 대입  
  - `&=` : 비트 AND 후 대입  
  - `^=` : 비트 XOR 후 대입  
  - `|=` : 비트 OR 후 대입  
  - `<<=` : 왼쪽 시프트 후 대입  
  - `>>=` : 오른쪽 시프트 후 대입  
  - `>>>=` : 부호 무시 오른쪽 시프트 후 대입  
  
<br>

# (9월 11일 강의)

Pascal Case 
camelCase
cabab-case
Snaek_case

서블릿(servlet) - Backend

<br>

# (9월4일 강의)
## Markdwon 문법

### HTML에서 `<h1>` ~ `<h6>`

## 문자 강조
*이탤릭체*  
**굵은 문자**

수평선
***

## 리스트 
* 언오더드 리스트
* 언오더드 리스트
* 언오더드 리스트
    * 언오더드 리스트
    * 언오더드 리스트
    * 언오더드 리스트
        * 언오더드 리스트
        * 언오더드 리스트
        * 언오더드 리스트

1. 오더드리스트
1. 오더드리스트
1. 오더드리스트


``` java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```
인라인 코드는 `버튼`이나 코드 조각을 강조할 때 사용

Vs Code에서 터미널을 열려면 `Ctrl` + `~`


## 링크

## 외부 링크
[구글 접속](https://google.com "구글 주소")

## 내부 링크
[링크 라벨](#markdwon-문법 "markdwon-문법")

## 그림 삽입
![ git 로고 ](OIP.webp "깃 로고")
