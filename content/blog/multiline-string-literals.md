---
title: "Multiline String Literals"
date: 2017-07-01T14:07:14+00:00
draft: false
categories: [String, Swift4]
tags: [String, Swift4]
author: rogermolas
---

Long strings are strings delimited by `"""triple quotes"""`  that can contain newlines and individual " characters without the need to escape them. [SE-0168 Multi-Line String Literals](https://github.com/apple/swift-evolution/blob/master/proposals/0168-multi-line-string-literals.md)

### Multi-Line String Literal Creation
```
let lines = """
            This is line one
            This is line two
            This is line three
            """

print("Multi-Line String: \(lines)")
```

### Mutation

```
let myString = """
                Hello Multi line string!
                This is sample of mutating string.
                End here
                """

let startingIndex = myString.index(myString.startIndex, offsetBy: 25)
let endingIndex = myString.index(myString.startIndex, offsetBy: 60)
let range = startingIndex..<endingIndex
let substring = myString.substring(with: range)

print("Second line: \(substring)")
```

### Inserting value

```
let array = ["A", "Hello", 10] as [Any]
let myString = """
                Letter \(array[0])
                \(array[1]) Word
                Number \(array[2])
                """

print("\(myString)")
```


