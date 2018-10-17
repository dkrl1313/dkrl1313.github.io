---
layout: post
title: iOS Swift입문 - Enumerations
tags: [Swift]
---

### Enumerations

1.	연관성 있는 값들의 그룹을 만들어 Type-Safe 하게 사용
2. 일련의 값(Raw Value)을 주지 않아도 됨

#### enum

```
enum CompassPoint {
    case north
    case south
    case east
    case west
}

enum CompassPoint {
    case north, south, east, west
}

```
#### 예제
```
import Foundation

struct Task {
    var title:String
    var time:Int?

    var owner:Employee
    var participant:Employee?

    var type:TaskType
    enum TaskType {
        case Call
        case Report
        case Meet
        case Support

        var typeTitle:String {
            get {
                let titleString:String
                switch self {
                case .Call:
                    titleString = "Call"
                case .Report:
                    titleString = "Report"
                case .Meet:
                    titleString = "Meet"
                case .Support:
                    titleString = "Support"
                }
                return titleString
            }
        }
    }
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

var callTask = Task(title: "Call to Toby", time: 10*60, owner: me, participant: toby, type:.Call)
var reportTask = Task(title: "Report to Boss", time: nil, owner: me, participant: nil, type:Task.TaskType.Report)

```
