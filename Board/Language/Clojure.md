# Clojure

## Data Structure ##
- hash-map
 ```clojure
 {:a 1 :b 2}

(get (:a 1 :b 2) :a)   
;=>1

(get (:a 1 :b 2) :c)
;=>nil

(:a (:a 1 :b 2) )
;=> 1
 ```
- vector
```clojure
[1 2 3 4]

(get [1 2 3 4] 1)
;=> 2

(conj [ 1 2 3 4] 5)
;=> [ 1 2 3 4 5 ]
```
- set
```clojure
#{1 2  3 3}
;=> #{ 1 2}

```
- list
```clojure
'(1 2 3 4)

(nth '(1 2 3 4) 0)
:=>1s

(clojure '(1 2 3 4) 5)
:=> ( 1 2 3 4 5)
```
- String
```clojure
(def myname "my name is \"chensitan\"")
```

## Calling Functions

- Arity
The number of arguments

- Default Argument
```clojure
(defn x-chop
    "Describe the kind of chop you are inflicting on some one."
    ([name chop-type] 
     (str  "I " chop-type  " chop " name " !  Take that!" ))
    ([name] 
    (x-chop name "karate")))
```

- rest parameters
```clojure
(defn add
"just like + "
[& numberlist]
(+ numberlist))
```

- Destrcuturing
```clojure
;vector/list
(defn my-first()
    [[first-thing]]
    first-thing)
(my-first [ 1 2 3]) => 1
```

```clojure
;map
(defn summary
[{n :name a :age }]
(str n " is " a " this year")
(summary {:name "chensitan" :age "33"}) => "chensitan is 33 this year"
```

```clojure
(defn summary
[{:keys [name age]} :as myInfo]
(str n " is " a " this year") )
```

- Anonymous Functions
```clojure
(def myfunc (fn [x] (* x 2))
(map myfunc [1 2 3])
```

```clojure
(map #(+ % 1) [1 2 3])
(#(+ %1 %2) 2 3)
(#(+ % &) 1 2 3)
```