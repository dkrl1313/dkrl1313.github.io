---
layout: post
title: iOS Swift - sorted(by:)
tags: [Swift]
---

#sorted(by:)

```
func sorted(by areInIncreasingOrder: (Element, Element) throws -> Bool)
  rethrows -> [Element]
```

### 예제
##### 방법1. 내림차순
```
let students: Set = ["Kofi", "Abena", "Peter", "Kweku", "Akosua"]
let descendingStudents = students.sorted(by: >)
print(descendingStudents)
// Prints "["Peter", "Kweku", "Kofi", "Akosua", "Abena"]"
```
##### 방법2. 오름차순
```
print(students.sorted())
// Prints "["Abena", "Akosua", "Kofi", "Kweku", "Peter"]"
print(students.sorted(by: <))
// Prints "["Abena", "Akosua", "Kofi", "Kweku", "Peter"]"
```
##### 방법3.
```
func ascendantSort (sort1:Double, sort2:Double) -> Bool {
    return sort1 > sort2
}
let sortedPrices = vatPrices.sorted(by: ascendantSort)
```
##### 방법4.
```
let sortedPrices2 = vatPrices.sorted(by: {sort1, sort2 in
    return sort1 > sort2
})
```

##### 방법5.
```
let sortedPrices3 = vatPrices.sorted(by: {$0 > $1})
```

##### 방법6.
```
let sortedPrices4 = vatPrices.sorted(by: >)
```
