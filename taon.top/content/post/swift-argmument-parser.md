---
title: "Swift Argmument Parser"
date: 2022-03-28T17:56:08+08:00
---

# swift-argument-parser 用例
## 简介

>swift-argument-parser 是Apple出品的swift写命令行app的工具，使用DSL，非常方便的实现参数、变量的设定及帮助等等。以下是代码用例

```swift
//
//  main.swift
//  sapTest
//
//  Created by tao ning on 3/28/22.
//


import ArgumentParser

struct SplitMix64: RandomNumberGenerator {
    private var state: UInt64

    init(seed: UInt64) {
        self.state = seed
    }

    mutating func next() -> UInt64 {
        self.state &+= 0x9e3779b97f4a7c15
        var z: UInt64 = self.state
        z = (z ^ (z &>> 30)) &* 0xbf58476d1ce4e5b9
        z = (z ^ (z &>> 27)) &* 0x94d049bb133111eb
        return z ^ (z &>> 31)
    }
}

struct RollOptions: ParsableArguments {
    @Option(name:.shortAndLong , help: ArgumentHelp("Rolls the dice <n> times.", valueName: "n"))
    var times = 1

    @Option(help: ArgumentHelp(
        "Rolls an <m>-sided dice.",
        discussion: "Use this option to override the default value of a six-sided die.",
        valueName: "m"))
    var sides = 6

    @Option(help: "A seed to use for repeatable random generation.")
    var seed: Int?

    @Flag(name: .shortAndLong, help: "Show all roll results.")
    var verbose = false
}

// If you prefer writing in a "script" style, you can call `parseOrExit()` to
// parse a single `ParsableArguments` type from command-line arguments.
let options = RollOptions.parseOrExit()

let seed = options.seed ?? .random(in: .min ... .max)
var rng = SplitMix64(seed: UInt64(truncatingIfNeeded: seed))

let rolls = (1...options.times).map { _ in
    Int.random(in: 1...options.sides, using: &rng)
}

if options.verbose {
    for (number, roll) in zip(1..., rolls) {
        print("Roll \(number): \(roll)")
    }
}

print(rolls.reduce(0, +))


```

## 输出结果
```shell
sapTest -h
USAGE: roll [--times <n>] [--sides <m>] [--seed <seed>] [--verbose]

OPTIONS:
  -t, --times <n>         Rolls the dice <n> times. (default: 1)
  --sides <m>             Rolls an <m>-sided dice. (default: 6)
        Use this option to override the default value of a six-sided die.
  --seed <seed>           A seed to use for repeatable random generation.
  -v, --verbose           Show all roll results.
  -h, --help              Show help information.
```