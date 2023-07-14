# Competetive Programming References

Within programming problems, sometimes various math formulas are useful. Curated here will be various different formulas and a brief explanation on how to use them.

${n \choose k} = \frac{n!}{k!(n-k)!}$
Used for counting the number of combinations in something. Commonly thought of as the "$_n C _k$"

$_n P _k = \frac{n!}{k!}$
Counts the number of *permutations* within a total pool of $n$, with each permutation having size $k$.

The main differences between permutations and combinations: **Order matters in permutations**. So of a pool of letters "ABCDEF", a combination of length 3 is "ABC", but the same permutations of that combination are "ABC", "BCA", "CAB", "BAC", "ACB", "CBA"

## Polygon Area

**Bretschneider's Formula** for maximal quadrilateral polygon:
K = $\sqrt{(s-a)(s-b)(s-c)(s-d)-(abcd\times\cos^2{\frac{\alpha + \gamma}{2}})}$

Presume angle to be 180, then:
```cpp
double maxArea(double a, double b, double c, double d) {
    double s = (a + b + c + d ) / 2;
    return sqrt((s - a) * (s - b) * (s - c) * (s - d))
}
```
