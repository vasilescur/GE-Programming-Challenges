# Week 1 - Easy

## Problem

Perfectly Balanced, as All Things Should Be (1 point)

Given a string containing only the characters `x` and `y`, find whether there are the same number of `x`’s and `y`’s. 
Input: string, output: boolean or truthy/falsy value.

Test Cases:
```
balanced("xxxyyy") => true
balanced("yyyxxx") => true
balanced("xxxyyyy") => false
balanced("yyxyxxyxxyyyyxxxyxyx") => true
balanced("xyxxxxyyyxyxxyxxyy") => false
balanced("") => true
balanced("x") => false
```

## Reference Implementation

```py
def balanced(word):
  return word.count('x') == word.count('y')
```

## Featured Solutions

```clojure
(defn balanced [letters] 
    (let [freqs (frequencies (char-array letters))]
        (= (get freqs \x) (get freqs \y))))
```

```java
public static Boolean balanced(String input)
{
   int counterX = 0;

   for(int i = 0; i < input.length(); i++)
   {
      if(input.charAt(i) == 'x')
      {
          counterX++;
      }
      if(input.charAt(i) == 'y')
      {
          counterX--;
      }
   }

   if(counterX == 0)
   {
      return true;
   }
   return false;
}
```
