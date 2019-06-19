---
title: "Play With Chunks"
date: 2019-06-19T16:19:10+07:00
draft: false
---

Have you imagine 😇 you have an array of elements and you want to split them into chunks of a size you specify. Here's the extension

```swift
extension Collection {
    func chunked(by maxLength: Int) -> [SubSequence] {
        precondition(maxLength > 0, "chunk size must be greater than zero")
        var start = startIndex
        return stride(from: 0, to: count, by: maxLength).map { _ in
            let end = index(start, offsetBy: maxLength, limitedBy: endIndex) ?? endIndex
            defer { start = end }
            return self[start..<end]
        }
    }
}
```

`chunked` function will convert array into array, using whatever size you specify. 

Let's test that `chunked` functions.

```swift
[1, 2, 3, 4, 5, 6, 7, 8].chunked(by: 2)
/// It will print
[[1, 2], [3, 4], [5, 6], [7, 8]]

"Ah, shit here we go again".chunked(by: 3)
/// some white space included the chunk :)
["Ah,", " sh", "it ", "her", "e w", "e g", "o a", "gai", "n"]
```

