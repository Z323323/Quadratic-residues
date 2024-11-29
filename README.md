# Quadratic-residues

## Euler's Criterion and Legendre symbol

<p>
  Refer to [https://crypto.stanford.edu/pbc/notes/numbertheory/qr.html], I couldn't explain them better.
  The only thing which is not clear here is why we have $- 1$ as a quadratic residue if and only if

  $p \equiv 1 \mod 4$

  Imagine to take a random $a \in Z_{p}^{*}$ and compute

  $a^{(p - 1)/2} \equiv - 1 \mod p$

  We would normally conclude that $a$ is a quadratic non-residue, because if it was a residue, by the Euler's Criterion it would equal $1$. Now, following [https://math.stackexchange.com/questions/122048/1-is-a-quadratic-residue-modulo-p-if-and-only-if-p-equiv-1-pmod4] we can see that if we have a residue which is $- 1$, then it must be that

  $a^2 \equiv - 1 \mod p$

  And since $(- 1)^2 = 1$, then it must be that

  $a^4 \equiv 1 \mod p$

  which means that we chosed $a \in Z_{q}^{*}$ where $Z_{q}^{\ast}$ is a subgroup of $Z_{p}^{\ast}$ of order $4$. By Lagrange's Theorem it must be that $4|p - 1$, and therefore

  $p \equiv 1 \mod 4$
</p>

 ### Extension to $Z_{\phi(p^k)}^{\ast}$

 <p>
   We want to prove that the former section's result holds for powers of odd primes.
   
   $\phi(p^2) = p(p - 1)$

   thus by the CRT:

   $x^2 \equiv - 1  (\mod p^2)$<br>
   $iff$<br>
   $x^2 \equiv - 1 (\mod p)$<br>
   $x^2 \equiv - 1 (\mod p - 1)$

   which proves the result for $Z_{\phi(p^2)}^{\ast}$ because the first exists iff $x \in Z_{\phi(p^2)}^{\ast}$, and the second is the former section's case. Inducting on $k$ we can easily state that $Z_{\phi(p^k)}^{\ast}$ will always have at least one subgroup which is the same as the above case $(Z_{\phi(p^2)}^{\ast})$ by Lagrange, proving that a quadratic residue which is $- 1$ exists iff $p \equiv 1 \mod 4$. 
 </p>

 ### Extension to $Z_{\phi(n)}^{\ast}$

 <p>
   If

   $x^2 \equiv 1 \mod 2^k$

   it will necessary be that

   $x^2 \equiv 1 \mod 2^{k - 1}$

   because by Lagrange every subgroup's order divide $2^k$, thus iterating until we get

   $x^2 \equiv 1 \mod 2$

   we will eventually have $x^{(p - 1)/2}$ which is considerable as $- 1$ because $1 \mod 2 = - 1 \mod 2$.
   Also we will never face

   $x^2 \equiv - 1 \mod 2^k$

   because if it existed, by the same resoning of the previous section, we should necessary have some

   $x^4 \equiv - 1 \mod 2^k$

   which is impossible because it would coincide with the order of another subgroup which is $1$.
   Now we can finally generalize and say that if

   $n = 2^{k}p_{i}^{k_{i}}$

   for odd distinct primes $p_{i}$, by the CRT $- 1$ is a quadratic residue iff $k \leq 1$ and each $p_{i} \equiv 1 \mod 4$.
 </p>

 ## Miller-Rabin primality test

 <p>
   
 </p>

 
 
