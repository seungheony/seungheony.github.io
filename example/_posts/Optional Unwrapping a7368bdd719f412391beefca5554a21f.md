---
layout: post
title: Optional Unwrapping
image: /assets/img/blog/jj-ying.jpg
accent_image: 
  background: url('/assets/img/blog/jj-ying.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  Swift의 Optional Unwrapping에 대해 알아보자
invert_sidebar: true
---

# Optional Unwrapping

링크: https://seungheony.tistory.com/13
상태: 발행 완료
카테고리: Swift
태그: 문법

![블로그 썸네일 (4).png](Optional%20Unwrapping%20a7368bdd719f412391beefca5554a21f/%25EB%25B8%2594%25EB%25A1%259C%25EA%25B7%25B8_%25EC%258D%25B8%25EB%2584%25A4%25EC%259D%25BC_(4).png)

```swift
var name: String?
name = "승헌"
print(name) // Optional("승헌")
```

위의 코드와 같이 `name` 이라는 변수에 `“승헌”` 을 넣어도 해당 변수가 옵셔널 타입이기 때문에 `“승헌”` 을 출력하는 것이 아니라 `Optional(”승헌”)` 을 출력한다. 

이처럼 Optional은 포장시에 싸여있는 형태를 가지기 때문에, Non-Optional Type으로서 값을 사용하려면 포장지를 까는 작업을 해줘야 한다. 이 작업을 **Optional Unwrapping** 이라고 한다. 

![Untitled](Optional%20Unwrapping%20a7368bdd719f412391beefca5554a21f/Untitled.png)

**하지만 Optional Unwrapping을 하기 위해서는 절대 Unwrapping 하고자 하는 변수가 `nil` 이면 안된다.** 

`nil` 은 값이 아니다. “값 없음”을 나타내는 표현일 뿐, `nil` 을 어떠한 값이라고 생각하면 안된다. 따라서 만약 값이 없으면 `nil` 이지 `Optional(nil)`이 아니란 말이다.  

```swift
let a: Int? = nil
print("a == \(a)")

let b: Int? = 4
print("b == \(b)")
```

![Untitled](Optional%20Unwrapping%20a7368bdd719f412391beefca5554a21f/Untitled%201.png)

이와 같이 `nil` 은 값이 없는 것이기 때문에 Optional이란 포장지도 없고 따라서 Optional이란 포장지를 까는 Unwrapping도 하면 안된다. 

---

지금부터는 Optional Unwrapping을 하는 여러 방법들을 알아보자

# 1. 강제 추출(Forced Unwrapping)

> **옵셔널에 값이 `nil` 이건 말건 강제로 옵셔널을 벗겨버리는 것을 말한다.**
> 

강제 추출 연산자로는 **! (느낌표)**를 사용한다. Optional로 선언된 변수를 사용할 때 그 **뒤에 !를 붙혀주어 사용**한다. 

```swift
var myInfo = "내 나이는 \(age!)살 입니다. " // 내 나이는 25살 입니다. 
```

이렇게 내가 원하는 Optional이 해제된 값을 얻을 수 있다. 

> **하지만, `nil` 일 경우에도 값을 해제하는데, 앞서 말했듯이 `nil` 은 포장지가 없다. 그런데 포장지를 까려고 하면 에러가 발생한다.**
> 

이것이 컴파일 에러로 끝나면 다행이지만 만약 **런타임 에러로 떨어지면 가장 심각한 버그인 비정상 종료 버그가 발생한다.** 

> **그래서 이 ‘강제 추출’방법은 실제 프로그래밍에서는 거의 쓸 일이 없다.**
> 

---

# 2. Optional Binding

**옵셔널 바인딩을 사용하면 안전하게 Optional의 값을 Unwrapping 할 수 있다.** 

그 방법은 다음 세 가지 Syntax를 통한다. 

```swift
if let name Type = OptionalExpression {
		// code
}

while let name Type = OptionalExpression {
		// code
}

guard let name Type = OptionalExpression else {
		// code
}
```

이 세가지 방식은 다음과 같은 공통점을 가지고 있다. 

1. **옵셔널 표현식을 먼저 평가한다.** 
2. **값이 있는 경우(`nil`이 아닌 경우) 정의된 상수(`name`) 에 옵셔널이 해제된 값을 저장하고 `true`를 ㅂ**
3. **값이 없는 경우(`nil`) `false`를 반환한다.** 
4. **타입 추론이 되므로 Type Annotaion은 대부분 생략한다.** 

지금부터는 각 Syntax 별 예제를 알아볼텐데, `while let`은 거의 사용되지 않기 떄문에 생략하겠다. 

## 1. `if let`

```swift
let optionalNum: Int? = 4
```

이처럼 옵셔널 타입의 optionalNum이라는 상수가 있다. `if let` 을 이용하여 **옵셔널 바인딩**을 하면 다음과 같이 사용이 가능하다. 

```swift
if let nonOptionalNum= optionalNum {
		// The 'optionalNum' is not nil
		print(nonOptionalNum)
} else {
		// The 'optionalNum' is nil
		print(optionalNum)
}
```

이렇게 사용한다. 

이 구문의 결과 값은 4인데, 만약에 `optionalNum`에 `nil` 이 할당됐다면, 결과 값은 `nil` 일 것이다. 

`if let` 의 메커니증은 다음과 같다. 

### 1) 표현식이 `nil` 인지 아닌지 판별한다.

![Untitled](Optional%20Unwrapping%20a7368bdd719f412391beefca5554a21f/Untitled%202.png)

### 2) 표현식이 `nil` 이 아닌 경우

![Untitled](Optional%20Unwrapping%20a7368bdd719f412391beefca5554a21f/Untitled%203.png)

> `**optionalNum`의 값이 `nil` 이 아닌 경우, `optionalNum` 을 Unwrapping한 값을 `NonOptionalNum` 에 대입한다.**
> 

### 3) 표현식이 `nil` 인 경우

![Untitled](Optional%20Unwrapping%20a7368bdd719f412391beefca5554a21f/Untitled%204.png)

### Tip

![Untitled](Optional%20Unwrapping%20a7368bdd719f412391beefca5554a21f/Untitled%205.png)

> 위와 같이 한번에 **여러 개의 옵셔널 타입을 바인딩**할 수도 있고, 흔히 사용하는 **조건문을 추가**하는 것도 가능하다.
> 

`name`, `age` 가 `nil` 이 아니고, `age` 의 값이 5보다 커야 `if` 가 `true` 를 받는다. 

---

## 2. `guard let`

> `**guard let` 은 특성상 함수에서만 쓰이며, `guard` 구문의 조건을 만족하지 못하면 `else` 문으로 빠져서 함수의 실행을 종료(`return`)시킬 때 사용한다.**
> 

즉, “너 이조건 만족 못하면 내 함수에서 나가!” 이렇게 가드하는 것이라고 이해하면 좋겠다. 

```swift
guard let nonOptionalNum = optionalNum else {
		// The 'optionalNum' is nil
		return
}

// The 'optionalNum' is not nil
```

`guard let` 의 메커니증은 다음과 같다. 

### 1) 표현식이 `nil` 인지 아닌지 판별한다.

![Untitled](Optional%20Unwrapping%20a7368bdd719f412391beefca5554a21f/Untitled%206.png)

### 2) 표현식이 `nil` 이 아닌 경우

![Untitled](Optional%20Unwrapping%20a7368bdd719f412391beefca5554a21f/Untitled%207.png)

`guard` 문에서는 표현식이 `nil` 이 아닐 경우 `else` 문으로 빠지지 않고 원래 `guard` 문을 실행시키던 scope로 돌아온다. 

![Untitled](Optional%20Unwrapping%20a7368bdd719f412391beefca5554a21f/Untitled%208.png)

주의할 점: 옵셔널 바인딩 된 `nonOptionalNum` 의 Scope는 `guard` 구분 밖이다. 따라서 `else` 문에서는 `nonOptionalNum`을 사용할 수 없다. 

### 3) 표현식이 `nil` 인 경우

![Untitled](Optional%20Unwrapping%20a7368bdd719f412391beefca5554a21f/Untitled%209.png)

표현식이 `nil` 인 경우에는 `else` 구문으로 빠져서 `return`을 하거나 실행을 종료하는 것이 일반적이다. 

### Tip

> `if let` 과 동일하게 한번에 **여러 개의 옵셔널 타입을 바인딩**할 수도 있고, 흔히 사용하는 **조건문을 추가**하는 것도 가능하다.
> 

---

# 정리

|   | if let | guard let |
| --- | --- | --- |
| 선언 | if let name: Type = OptionalExpression { | guard let name: Type = OptionalExpression else { |
| 표현식이 nil일 경우 | if 조건문이 false가 됨 | else문이 실행됨 |
| 표현식이 nil이 아닐 경우 | if 조건문이 true가 됨 | guard 구문 종료(함수 이어서 실행) |
| 사용 용도 | 표현식이 nil인지 평가하여 간단한 피드백을 줄 때 | 표현식이 nil인지 평가하여nil일 경우 함수 실행을 종료시킬 때 |
| 바인딩된 상수의 scope(선언 구문에서 name이 바인딩된 상수) | if 구문 안에서만 사용 가능(else 구문 및 밖에서 사용 불가) | guard 구문 밖에서만 사용 가능(else 구문에서 사용 불가) |