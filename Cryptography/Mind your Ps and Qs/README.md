# Mind your Ps and Qs
### AUTHOR: SARA
### Challenge Points: 20

## Category
Cryptography

## Challenge Description
In RSA, a small e value can be problematic, but what about N? Can you decrypt this? [values](values)
## Hints
Bits are expensive, I used only a little bit over 100 to save money
## Solution
Here are the contents of values:

```text
Decrypt my super sick RSA:
c: 8533139361076999596208540806559574687666062896040360148742851107661304651861689
n: 769457290801263793712740792519696786147248001937382943813345728685422050738403253
e: 65537
```

`n` is small and can be factored into `p` and `q`:

```python
from factordb.factordb import FactorDB
import gmpy2

c = 8533139361076999596208540806559574687666062896040360148742851107661304651861689
n = 769457290801263793712740792519696786147248001937382943813345728685422050738403253
e = 65537

f = FactorDB(n)
f.connect()
p, q = f.get_factor_list()
ph = (p-1)*(q-1)
d = gmpy2.invert(e, ph)
plaintext = pow(c, d, n)
print("Flag: {}".format(bytearray.fromhex(format(plaintext, 'x')).decode()))
```

Output:
```console
root@kali:/Cryptography/Mind_your_Ps_and_Qs# python3 script.py
Flag: picoCTF{sma11_N_n0_g0od_45369387}
```

## Flag
`picoCTF{sma11_N_n0_g0od_45369387}`