<!-- <style>
    details > summary * { display : inline; }
</style> -->


## Interesting Problems

<details>
<summary>Simulate 6 faced fair die using a fair coin.</summary>

- Toss the coin 3 times and call this action as `generate a set`.
- There are $2^3 = 8$ possible outcomes each with probability $1/8$.
- Select 6 outcomes and assign each outcome to a value of die.
- Reject 2 outcomes i.e if you get an outcome other than the assigned outcomes above `generate a set` again.
<details>

<summary>Outcome mapping</summary>

- HHH - Reject
- HHT - 1
- HTH - 2
- HTT - 3
- THH - 4
- THT - 5
- TTH - 6
- TTT - Rejected
</details>

<details>
<summary>Proof that the probability of each simulated die outcome is 1/6</summary>

- Let $X$ be an event that one of the die outcome is produced in a generation.
- Let $X_i$ be an event that the die outcome is produced as $i$.
- Let $X_{ij}$ be an event that the die outcome is produced as $i$ exactly in the $j$ th generation.

    $P(X_{11}) = 1/8$ for that matter $P(X_{i1}) = 1/8$\
    Hence $P(X) = \sum {P(X_{i1})} = 6 \times 1/8 = 3/4$\

    $P(X_{i2}) = (1 - P(X))(P(X_{i1}))$\
    $P(X_{i3}) = (1 - P(X))^2(P(X_{i1}))$\
    ...

    $P(X_{in}) = (1 - P(X))^{n-1}(P(X_{i1}))$\
    $P(X_{in}) = (1 - 3/4)^{n-1}(1/8) = (1/4)^{n-1}(1/8)$

    $P(Die\ outcome = 1) = \sum P(X_{1j}) = \sum (1/4)^{j-1}(1/8)$\
    $ = (1/8)/(1-1/4)$ *(Using sum of infinite G.P)*\
    $ = (1/8)/(3/4) = 1/6$\
    This is satisfied for all 1 to 6
</details>
<details>
<summary>Python code to simulate</summary>

[code](https://github.com/kadapallaNithin/mini_projects/blob/master/simulate_die_from_coin/simulate_die_from_fair_coin.py)

```python
import random
def toss_a_fair_coin():
    if random.random() >= 0.5:
        return 'H'
    return 'T'

def generate_a_set():
    return ''.join([toss_a_fair_coin() for _ in range(3)])

def simulate_die():
    s = generate_a_set()
    if s == 'HHH' or s == 'TTT':
        return simulate_die()
    return {"HHT":1,"HTH":2,"HTT":3,"THH":4,"THT":5,"TTH":6}[s]

def test():
    number_of_rolls = 100000
    counts = [0]*6
    total_count = 0
    for i in range(number_of_rolls):
        outcome = simulate_die()
        counts[outcome-1] += 1
        total_count += 1
    print(round(1/6,3),[round(count/total_count,3) for count in counts])

test()
```
</details>
</details>