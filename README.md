# StringFilter

[![Build Status](https://travis-ci.org/tnantoka/StringFilter.svg?branch=master)](https://travis-ci.org/tnantoka/StringFilter) [![codecov.io](https://codecov.io/github/tnantoka/StringFilter/coverage.svg?branch=master)](https://codecov.io/github/tnantoka/StringFilter?branch=master) [![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)

A swifty text converter.

## Installtion

### Carthage

```
github "tnantoka/StringFilter"
```

### CocoaPods

```
pod 'StringFilter'
```

## Usage

```swift
import StringFilter

let message = "ifmmp-!xpsme"
let filters = [
    StringFilter.Shift(-1),
    .Capitalize,
    .Replace("$", "!")
]
print(message.str_filter(filters)) // "Hello, World!"
```

### Built-in filters

Case | Source | Result
--- | --- | ---
`.Capitalize` | `test` | `Test`
`.Lowercase` | `TEST` | `test`
`.Uppercase` | `test` | `TEST`
`.Shift(1)` | `test` | `uftu`
`.Repeat(2))` | `test` | `testtest`
`.Replace("t", "T")` | `test` | `TesT`
`.Japanese(.Hiragana, .Katakana)` | `あいうえお` | `アイウエオ`
`.Japanese(.Katakana, .Hiragana)` | `アイウエオ` | `あいうえお`
`.Japanese(.Full(.Alphabet), .Half(.Alphabet)))` | `ＡＢＣＤＥ` | `ABCDE`
`.Japanese(.Half(.Alphabet), .Full(.Alphabet)))` | `ABCDE` | `ＡＢＣＤＥ`
`.Japanese(.Full(.Number), .Half(.Number)))` | `０１２３４５６７８９` | `0123456789`
`.Japanese(.Half(.Number), .Full(.Number)))` | `0123456789` | `０１２３４５６７８９`

### Custom filter

```swift
struct ExclaimFilter: StringFilterType {
    func transform(string: String) -> String {
        return string + "!"
    }
}

let customFilter = ExclaimFilter() * 3 * StringFilter.Uppercase
print("Hello".str_filter(customFilter)) // "HELLO!!!"
```

## TODO

- [ ] Chinese numeral
- [ ] One-byte katakana 

## Acknowledgements

- https://github.com/objcio/functional-swift
- https://github.com/niwaringo/moji
- https://github.com/gimite/moji
- https://github.com/yoshitsugu/zen_to_i

