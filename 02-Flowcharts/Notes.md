# Flowcharts
- Diagrames to represent commands
    - Start/Stop : Circle/Oval
    - Input/Output : Parallelogram
    - Processing setp : Rectangle
    - Conditions : Diamond
    - Flow : Arrow lines

# Pseudocode
- General english like words which describes how the algorithm works
- It is irrespective of any programming langauge syntax
- There is no specific way to write pseudocode, can be written in multiple ways

E.g Find if number is prime

```
start
input number
c=2
while c<num:
    if number%c==0:
        output "not prime"
        exit
    c=c+1
end while
output "prime"
exit
```

## Observation
- For number=36, to check if it prime
```
1 * 36 = 36
2 * 18 = 36
3 * 12 = 36
4 * 9 = 36
6 * 6 = 36
9 * 4 = 36
12 * 3 = 36
18 * 2 = 36
36 * 1 = 36
```

- Here we can see after 6*6 the numbers are actually reapeated
- If we check for 2*18=36 then we need not check if 18*2=36
- So the number start to repeat after the sqrt(number)

- Optimized psuedocode to find number is prime
```
start
input number
c=2
while c<sqrt(num):  //while c*c<number:
    if number%c==0:
        output "not prime"
        exit
    c=c+1
end while
output "prime"
exit
```

## Also using sqrt() function takes some time, instead we can check if c*c<number