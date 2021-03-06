## 2A: Higher-order Procedures

Gerald Jay Sussman

### See some eg that cannot be implement by other language.

1. sum int

   ``` lis
   (DEFINE (SUM-INT A B)
   	(IF (> a b)
   		0
   		(+ a (SUM-INT (1+ a) b))
   	)
   )
   ```

2. Sum square

   ```lis
   (DEFINE (SUM-SQUARE A B)
   	(IF (> a b)
   		0
   		(+ )
   	)
   )
   ```

3. common pattern

   ```lis
   (define (<name> a b)
   	(if (> a b)
   		0
   		(+ (<term> a)
   		(<name> (<next> a) b))
   		)
   )
   ```

4. sigma notation

   ```lisp
   (define (SUM TERM A NEXT B)
     (IF (> A B)
     	0
       (+ (TERM A)
          (SUM TERM
               (NEXT A)
               NEXT
               B
          )
       )
     )
   )
   ```

5. sum-int use sigma

   ```lis
   (define (sum-int a b)
   	(define (identity x) x)
   	(SUM identity a 1+ b)
   )
   ```

6. sum-sq 

   ```lisp
   (DEFINE (SUM-SQ A B)
   	(SUM SQUARE A 1+ B) 
   )
   ```

7. pi-sum

   ```lisp
   (DEFINE (PI-SUM A B)
   (SUM (lamda (i) (/ 1 (* i (+ i 2)))) 
        a
        (lamda (i) (+ i 4))
        b
        )        
   )
   ```

### Iterative implementation of sum 

```lis
(define (sum term a next b)
	(define (iter j ans)
		(if (> j b)
			ans
			(iter (next j)
				(+ (term j) ans)
			)
		)
	)
	(iter a 0)
)
```

### Square Root of Fixed Point

```lisp
(DEFINE (SQRT X)
	(FIXED-POINT 
    	(lamda (y) (AVERAGE (/ X Y) Y))
     	1
     )
)
```

```lisp
(DEFINE (FIXED-POINT f START)
	(DEFINE (ITER OLD NEW)
   		(IF (CLOSE-ENUF? OLD NEW)
            NEW
            (ITER NEW (F NEW))
        )
    )
   (ITER START (F START))
)
```

```lisp
(define (fixed-point f start)
  (define tolerance 0.0001)
  (define (close-enuf? u v)
    (< (abs (- u v)) tolerance))
  (define (iter old new)
    (if (close-enuf? old new)
        new
        (iter new (f new))))
  (iter start (f start))
)
```



### why use this average to get square root ,not other function?

```lisp
(DEFINE (SQRT X)
	(FIXED-POINT
    	(AVERAGE-DAMP (lamda (y) (/ x y)))
     	1
    )
)

(DEFINE AVERAGE-DAMP
	(lamda (f)
		(lamda (x) (AVERAGE f(x) x))
	)
)
```

### Question : Use lamda to define anonymous procedure should to learn deeply!!

```lisp
(DEFINE (AVERAGE-DAMP F)
	(DEFINE (FOO X)
		(AVERAGE (F X) X)
	)
    FOO
)
```


### Newton Method

> Newton Method is to find roots of a function.

#### 用牛顿法求平方根

```lisp
(DEFINE (SQRT X)
	(NEWTON (lambda (y) (- x (SQARE y)))
		1
	)
)

(DEFINE (NEWTON f guess)
	(DEFINE DF (DERIV F))
    (FIXED-POINT
    	(lambda (x) (- x (/ (f x) (df x))))
     	guess
    )
)

(DEFINE DERIV
	(lambda (f)
		(lambda (x)
			(/ (- (f (+ x dx))
                  (f x))
               dx
            )
		)
	)
)
```

### Chris Strachey

- inventors of **denotational semantics**
- He was a great advocate of making procedures or functions first-class citizens in a programming language

```markdown
The rights and privileges of first-class citizens
- To be named by variables
- To be passed as arguments to procedures
- To be returned as values of procedures
- To be incorporated into data structures (目前课程还没有讲到)
```

### QA

```lisp

```

