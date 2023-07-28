# Scanner 클래스의 메서드

 <img width="50%" src="https://github.com/Jhyeri/TIL/assets/111175466/c22ad703-62d2-4529-ba55-8d3d082bece2"/>

## 📌 next()

- 공백을 기준으로 한 단어 또는 한 문자씩 입력받는다.
- 버퍼에 입력된 문자나 문자열에서 **공백 전까지의** 단어를 읽는다.
- **개행 문자를 가져오지 않는다.**

## 📌 nextLine()

- 문자 또는 엔터를 치기 전까지의 문장 전체를 입력받는다.
- 버퍼에 입력된 문자열을 개행문자까지 다 가져온다.

## 📌 next()와 nextLine()의 차이점

- 개행문자 포함 여부의 차이
<br/>

### [nextLine() 메서드 사용하기]

<details>
<summary><b>코드 펼치기</b></summary>
<div markdown="1">
	
```java
import java.util.Scanner;
 
public class Test {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
 
        int num;
	String str;
	System.out.println("숫자입력");
	num = sc.nextInt();
	
	System.out.println("str입력");
	str = sc.nextLine();
	
	System.out.println("num : " + num);
	System.out.println("str : " + str);
	sc.close();

    }
}
```

```java
숫자입력
1
str입력
num : 1
str :
```
</div>
</details>
<br/> 
숫자만 입력하자마자 바로 출력이 된다.

**next()는 개행문자를 무시하고 문자를 받는다.**

nextLine()은 **한줄 단위로 입력**을 받기 때문에 개행문자도 포함한다.

숫자 1을 입력하고 엔터를 쳤을 때 버퍼에는 **1\n**이 존재한다.

nextInt()가 버퍼의 내용을 가져올 때 **분리자를 제외하고** 가져오기 때문에 1만 가져오게 된다.

그럼 버퍼에 개행문자만 남게 되는데, **nextLine()은 개행문자인 분리자를 포함**시키기 때문에 \t만 가져오고 프로그램이 종료된다. 

### [next() 메서드 사용하기]
<details>
<summary><b>코드 펼치기</b></summary>
<div markdown="1">
	
```java
import java.util.Scanner;

public class Test{

	public static void main(String[] args) {

	Scanner sc = new Scanner(System.in);
		 
        int num;
	String str;
	System.out.println("숫자입력");
	num = sc.nextInt();

	System.out.println("str입력");
	str = sc.next();

	System.out.println("num : " + num);
	System.out.println("str : " + str);
	sc.close();
	
	}

}
```

```java
**숫자입력
1
str입력
abc
num : 1
str : abc**
```
</div>
</details>
<br/>

## 📌 입력과 버퍼 정리

키보드를 통해 키 입력을 받으면, 그 내용이 **버퍼** 라는 기억공간에 저장된다.

콘솔에서 키를 입력하고 **엔터키를 눌러야** 지금까지 쓴 내용이 버퍼에 전달되어 저장된다.<br/>

키보드로 120을 쓰고 엔터를 치면, 버퍼에는 **120\r\n**(엔터의 코드문자)가 들어가게 된다.

입력은 **nextInt()**메서드가 실행된 **이후**에  버퍼에 내용이 있는지 확인하게 된다.

실행 직후에는 처음이니 버퍼에 내용이 없다. 따라서 키보드로부터 사용자의 입력을 기다리는 상태가 되고, 위에 가정한대로 입력을 받게 된다.

그리고 버퍼에서 공백, 탭문자, 개행문자(엔터)를 **구분자**로 하여 하나의 단어를 가져오게 된다.

버퍼에서는 ‘120’까지를 가져오게 되며, **버퍼에는 개행문자 \r\n만 남는다.** <br/> 

만약 이 뒤에 또 다시 nextInt() 메서드가 실행된다면?

버퍼를 확인해서 비어있는지 살펴봐야 한다.<br/>

비어있지는 않지만 **개행문자만 있으므로 건너뛰고**, 내용이 없으므로 사용자로부터 입력을 받게 된다.

그리고 200 엔터를 치면,

nextInt()는 200이라는 값만 가지고 가게 되고, **버퍼에** **엔터 문자가 남게 된다.**

그 다음, nextLine()이 아닌 메서드가 실행되는 경우 엔터코드는 무시하고 다음 문자를 찾게 되어 상관 없지만

이 상태에서 nextLine()이 실행된다면 문제가 발생한다.

nextLine()는 한줄의 입력내용을 받는다.

**💡 한 줄 : 처음부터 개행문자까지의 문자열을 의미**

<br/>

즉, **nextLine()은 분리자도 읽어**오는 반면, **next()와 nextInt()는 분리자는 제외**하고 읽어온다.

어떤 값이 입력되었든 엔터까지 문자열을 모두 가져오게 되고,

지금같은 경우는 nextLine()가 개행문자만 읽게 된다.

버퍼가 비어있지 않으며 개행문자를 가지고 있는 상태이기 때문이다.

따라서 nextLine()을 실행한 후에는 아무 값도 남지 않게 된다.<br/> 

그래서 nextInt() 등을 쓴 후에는 언제나 엔터 개행문자가 버퍼에 남아있기 때문에

그 다음에 nextLine()을 쓰게 되면 위와 같은 현상이 일어난다.

아래와 같은 코드를 추가하면 nextLine()을 쓰고도 문제가 발생하지 않을 수 있다.

```java
int num = sc.nextInt();

sc.nextLine();

String str = sc.nextLine();
```

반환문자는 필요 없으므로 메서드만 호출한 후, 새로 nextLine()을 실행해서 한 줄을 받아오면 된다.<br/> 

다른 방법으로는 nextInt() 대신

```java
Integer.parseInt(sc.nextLine());
```

아예 한 줄 (개행문자포함)을 다 가져온 뒤에(어차피 버려짐) 정수형으로 반환하는 것이다.
