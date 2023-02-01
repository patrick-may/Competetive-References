# Competetive Programming References

Commonly, problems can generally be broken down into being solved by a few main different methods. 

This will detail the general structure of the "sliding window" paradigm

## Largest Contiguous Sum

*Kadane's Algorithm*
```py
# python styled but really pseudocode here
best_sum = INT_MIN # or first element of array. can be anything small
cum_sum = 0

for num in num_arr:
    cum_sum += num

    if best_sum < cum_sum:
        best_sum = cum_sum
    
    if cum_sum < 0:
        cum = 0

return best_sum
```