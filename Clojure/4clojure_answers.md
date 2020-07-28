# 4Clojure

It's a site that brings various levels of clojure's exercises, excellent for training.

I will bring some selected answers (follow lucaspepper):

``` clojure
#26:
Write a function which returns the first X fibonacci numbers.

#(take %
       (map first
            (iterate
             (fn [[a b]] [b (+ a b)]) [1 1])))

```

```clojure
#38:
Write a function which takes a variable number of parameters and returns the maximum value.

(fn [& params] (reduce (fn [a b] (if (< a b) b a)) 0 params))

OR

#(last (sort %&))
```
