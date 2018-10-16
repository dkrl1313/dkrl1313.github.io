---
layout: post
title: [iOS Swift입문] Class
tags: [Swift]
---


### Class

1.	데이터 모델의 주요한 구성요소
2.	오브젝트를 생성
3.	참조로 동작

### 예제

```
import UIKit

struct Task {
    var title:String
    var time:Int?

    var owner:Employee
    var participant:Employee?
}

class Employee {
    var name:String?
    var phoneNumber:String?
    var boss:Employee?
}

let me:Employee = Employee()
me.name = "Alex"
me.phoneNumber = "010-1234-5678"

let toby = Employee() // class는 let으로 선언해도 수정가능.
toby.name = "Toby"
toby.phoneNumber = "011-5678-1234"

print("\(toby.phoneNumber)")

var callTask = Task(title: "Call to Toby", time: 10*60, owner: me, participant: toby)
var reportTask = Task(title: "Report to Boss", time: nil, owner: me, participant: nil)

callTask.participant?.phoneNumber = "010-5678-1234"

print("\(toby.phoneNumber)")

```

### 실행결과

```
Optional("011-5678-1234")
Optional("010-5678-1234")
```

참조로 동작하기 때문에 callTask의 name값을 변경하면 toby의 name값도 변경된다.
