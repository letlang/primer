# Loops in LetLang

Loop statements are one the *few* things LetLang does different
than other languages.


## Pre-Test-Loop

A java-ish while-loop:

```
while (condition()) {
    postTest();
}
```

Is written:

```
repeat {
    while Condition()
    PostTest()
}
```

## Post-Test-Loop


A java-ish do-while-loop:

```
do {
    preTest();
}
while (condition());
```

Is written:

```
repeat {
    PreTest()
    while Condition()
}
```

## Mid-Test-Loop

The while-statement does not have to be
at the begining or the end of the repeat
block. It can be everywhere.

```
repeat {
  PreTest()
  while Condition()
  PostTest()
}
```

This sort of loop can not be written easily
in other languages. Most of them would require
the use of a `break` statement.

Java-ish:
```
while (true) {
  preTest();
  if (!condition()) {
    break;
  }
  postTest();
}
```

## While as Break

And essentially the while is syntactig sugar for:

```
repeat {
  PreTest()
  if (not Condition()) then { break() }
  PostTest()
}
```

Means break and continue also exist in LetLang.

## Repeat is a DSL (WIP!)

Means repeat is a function. At least an intrinsic one.

```
fun repeat(let Body: (in (:RepeatDSL)) -> Unit): Unit

type RepeatDSL = trait {

  fun while(let Condition: Boolean): Unit

  fun break(): Nothing

  fun continue(): Nothing

  // etc.
}
```

## Iteration (WIP!)

```
foreach {
  let X in Coll1
  let Y in Coll2
}
repeat {
  Env.IO.WriteLine(X ++ " " ++ Y)
}
```

Or more simple:

```
Coll.Each {
  let it -> Env.IO.WriteLine(it) 
}
```

## Counter-Loops

```
foreach { let i in 0 until 10 by 1 } repeat {
  Env.IO.WriteLine(i)
}
```

