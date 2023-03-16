# Iteration Analysis

Because loops are a defining factor of the runtime of any algorithm, we can examine their structure and function to understand how their iteration affects runtime.

For clarity, we use *for* loops as they are clearly defined in terms of the number of times they run.

# Simple Loops

```python
for(i = 0; i < n; i++)

for(j = 0; j < n; j++)
```

These simple for-loops *alone* iterate from 0 → n-1, thus *n* times. They *depend* on the size of the input, thus their minimum runtime is *n*. 

If both for-loops were operating together, one after the other, then we simply **add** their runtimes.

$n + n = 2n$

This is now *double* the runtime, but is not how we classify the runtime itself. We knpw that as *n* continues to grow, the only mathematical term that continues to grow is *n* itself. Thus, we can omit the constant coefficient.

# Nested Loops

These configurations of loops are special, since for every iteration of the outside loop, another inside loop runs its course.

```python
for(i = 0; i < n; i++):
		for(k = 0; k < n; k = k*2)
```

The *k* loop is nested within the *i* loop, and thus in every iteration of the *i* loop, the *k* loop runs.

An important note here is that the increment to the *k* loop is $k*2$, which doubles *k*. Thinking about it deeper, if *k* is larger every iteration, then it reaches the end-condition *faster,* so it iterates *less*.

<aside>
💡 k = 0, 1, 2, 4, 8, 16, 32, 64, 128, ...

</aside>

→ this *halves* the values *k* could take on, and follows the $logn$ runtime.

→ if *n* were 10, then the *k* loop runs only 5 times. This means that for every iteration of *i*, k runs 5 times.

<aside>
💡 Whenever loops halve or double its values, then it is $logn$ runtime. The base of the logarithmic depends on the coefficient. Doubles/Halves mean log base 2, Triples/Thirds mean log base 3, ...

</aside>

Since every iteration of *i* calls for *logn* runtime, *n* times, then it follows a *multiplicative rule*.

<aside>
💡 Nested loop runtimes are *multiplicative*, only when the nested loops are not dependent on *eachother*, rather on external variables.

</aside>