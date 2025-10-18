# automata-lib

https://pypi.org/project/automata-lib/

```python3
from automata.fa.dfa import DFA

# DFA which matches all binary strings ending in an odd number of '1's
my_dfa = DFA(
    states={'q0', 'q1', 'q2'},
    input_symbols={'0', '1'},
    transitions={
        'q0': {'0': 'q0', '1': 'q1'},
        'q1': {'0': 'q0', '1': 'q2'},
        'q2': {'0': 'q2', '1': 'q1'}
    },
    initial_state='q0',
    final_states={'q1'}
)

my_dfa
```

![output](https://github.com/user-attachments/assets/cdaf3312-b480-4218-a7e6-5acc8efcbbee)

```python
my_dfa.accepts_input('110011')
# False

my_dfa.accepts_input('001')
# True
```

