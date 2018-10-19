---
layout: post
title: iOS Swift - If let 구문
tags: [Swift]
---

### Optional Binding

```
var optionalName: String? = "John Appleseed"
var greeting = "Hello!"

if let name = optionalName
{
  greeting = "Hello, \(name)"
}
```
-> non-optional 변수인 name에 Optional 변수인 optionalName안에 들어있는 값을 할당할수있으면 {}안의 내용을 실행하라.

#### Optional 변수란?
Optional 변수란 “아무 값도 들어 있지 않은(nil 값)” 혹은 “어떠한 값”이 저장되어 있는 변수이다. 반대로 ? 없이 선언되는 일반 변수는 항상 값을 가지고 있는 것이 보편적이다.

즉, String? 변수와 String 변수는 다른 자료형이며 서로 호환되지 않는다.

```
let optional: String? = "abcd@gmail.com"
let required: String = optionalEmail // 컴파일 에러!
let required: String = nil // 컴파일 에러!
```
또한, Optional 변수를 출력시 Optional()로 바인딩되어 출력이 된다. Optional 변수의 바인딩을 강제로 푸는 방법은 변수 뒤에 !를 붙여주는 것이다. 이 방법은 강제로 바인딩을 푸는 것으로 만약 Optional 변수 안에 값이 저장되어 있지 않다면, runtime error를 일으킨다. 고로, 안전한 방법이 아니다.

```
let optional: String? = "abcd@gmail.com"
print(optional) //Optional("abcd@gmail.com") 출력

let required: String = optional! // optional이 할당되어 있지 않다면 컴파일 에러!
print(required) //abcd@gmail.com 출력
```
최상단에 설명되어 있는 Optional Binding 역시 이 Optional 변수 안에 값을 unwrap하는 방법 중 하나이다. 만약 코드가 아래와 같을 경우, optionalName 변수 안에 아무 값도 저장되어 있지 않기 때문에 if 구문은 실행되지 않는다.
```
var optionalName: String?
var greeting = "Hello!"

if let name = optionalName
{
    greeting = "Hello, \(name)"
}
print(greeting) //Hello! 출력
```
