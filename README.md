SwiftLevenshteinDistance
========================

> The "Fast" Levenshtein Distance implemented in Swift.


I've uploaded a playground (can be run in Xcode6+), if you just want the source code it's here:

```
func LevenshteinDistance(s:NSString, t:NSString) -> Int {
    let n = s.length
    let m = t.length
    if (n == 0) { return 0 }
    if (m == 0) { return 0 }

    var v0:Array<Int> = Array()
    var v1:Array<Int> = Array()
    for r in 0..m+1 { v0.append(r); v1.append(0) }

    for i in 0..n {
        v1[0] = i + 1
        for j in 0..m {
            let sChar = s.substringWithRange(NSRange(location: i, length: 1)) as NSString
            let tChar = t.substringWithRange(NSRange(location: j, length: 1)) as NSString

            let cost:Int = sChar.isEqualToString(tChar) ? 0 : 1

            v1[j+1] = min(v1[j] + 1, v0[j+1] + 1, v0[j] + cost)
        }

        for j in 0..v0.count {
            v0[j] = v1[j]
        }
    }
    return v1[m]
}


LevenshteinDistance("GAAMBOAL", "GAMBOL") // result is 2
```
Or you can find the `.swift` file inside the .playground folder named "section-1.swift".
