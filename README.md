# Quadratic residues

## Euler's Criterion and Legendre symbol

<p>
  Refer to [https://crypto.stanford.edu/pbc/notes/numbertheory/qr.html], I couldn't explain them better.
  The only thing which is not clear here is why we have $- 1$ as a quadratic residue if and only if

  $p \equiv 1 \mod 4$

  #### Fast ex.

  $4^2 \equiv -1 \mod 17$

  hence in this case we would have $- 1$ as a residue, indeed

  $(- 1)^{(p - 1)/2} = (- 1)^8 \equiv 1 \mod 17$

  It's quite intuitive at this point to say that if $(p - 1)/2$ is even then we can have $- 1$ as a residue, otherwise we can't. For ex. imagine $(- 1)^3 \equiv - 1 \mod 7$. Indeed $3$ is odd. 

  Now, following [https://math.stackexchange.com/questions/122048/1-is-a-quadratic-residue-modulo-p-if-and-only-if-p-equiv-1-pmod4] we can see that if we have a residue which is $- 1$, then it must be that

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

   If

   $a^2 \equiv - 1 \mod p^2$

   then

   $a^4 \equiv 1 \mod p^2$

   therefore by Lagrange $4 | p(p - 1)$, and since $p$ is not divisible by $4$ it must be that $4 | p - 1$, thus

   $p \equiv 1 \mod 4$

   This result can easily be extended to any $p^k$ since

   $\phi(p^3) = p(p(p - 1))$<br>
   $\phi(p^4) = p(p(p(p - 1)))$

   and so on.
 </p>

 ### Extension to $Z_{\phi(n)}^{\ast}$

 <p>

   $x^2 \equiv - 1 \mod 2^k$

   is impossible because

   $2 \equiv 2 \mod 4$

   and for $2^k, k > 1$
   
   $2^k \equiv 0 \mod 4$
  
   Now we can finally generalize and say that if

   $n = 2^{k}p_{i}^{k_{i}}$

   for odd distinct primes $p_{i}$, by the CRT, $- 1$ is a quadratic residue iff $k \leq 1$ and each $p_{i} \equiv 1 \mod 4$. The condition $k \leq 1$ is because

   $\phi(2p_{i}^k) = \phi(2)\phi(p_{i}^k) = 1(p(p \dots (p - 1) \dots )) = \phi(p_{i}^k)$

   therefore $2$ is irrelevant and can coexist, while if it was at least $2^2$ we would have

   $x^2 \equiv - 1 \mod 2^2$

   using the CRT; and since it doesn't have solutions we can state that $n$ can't have $- 1$ as quadratic residue (works for any $k$).

   To conclude we can see a similar behaviour between the existence of generators, and the existence of $- 1$ as quadratic residue $(\mod n)$, i.e. if we consider $Z_{\phi(n)}^{\ast}, n = 2^k*\dots, k > 1$ we can't have generators nor $- 1$ as quadratic residue. 
 </p>

 ## Miller-Rabin primality test

 <p>
   This is probably one of the best tests, if not the best to find out if a number is a prime quickly. We take $n$ and a random $a$ in $[2 \dots p - 2]$, if

   $a^{n - 1} \not\equiv 1 \mod n$

   we are done, $n$ is not a prime. Otherwise if it equals $1$, we take $n$ and compute

   $s_{1} = (n - 1) / 2, s_{2} = s_{1} / 2, \dots$

   $r$ times, until we get a number which is not divisible by $2$ (if it's not divisible by $2$ initially then $n$ is not prime and we are done), then we perform

   $a^{s_{i}} \mod n, i = [1, \dots, r]$

   if it equals $1$ we continue until we get $- 1$ at $s_{r}$, otherwise if any

   $a^{s_{i}} \not\equiv 1 \mod n$

   or

   $a^{s_{r}} \not\equiv - 1 \mod n$

   then $n$ is composite.<br>

   This test exploit the difference between primes subgroups structure and non-primes one, i.e. the structure of subgroups follow $\phi(n)$ is way different between primes and non-primes, thus every time we iterate we are basically breaking the structure and finding random numbers. Also $ Also for every iteration the probability to find a number which fools the test decreases exponentially by a factor of $\displaystyle \frac{1}{4}$. I guess that this number derives directly from our reasoning about $p \equiv 1 \mod 4$. Just note this:

   $a^{(n - 1) / 2} \not\equiv a^{\phi(n) / 2}$ for non-primes

   also $- 1$ does not appear around in every multiplicative subgroup, thus it's almost impossible to fool the test. Things should be analyzed better but I don't have the time to do it so for the moment I'm not delving this method further.
 </p>

## Gauss' Lemma

<p>
  I'm going straight to the proof here, refer to [https://crypto.stanford.edu/pbc/notes/numbertheory/gausslemma.html]. The linked resource is more than enough, I'm just rewriting the proof for completeness and for study purposes, also I'll provide a couple steps which could seem more intuitive compared to the linked proof.

  Let $p$ an odd prime and $q$ an integer coprime (i.e. every integer in the $[1, \dots, p - 1]$ set is fine). We compute

  $\\{q, q2, \dots, q(p - 1)/2\\}$

  Now we analyze this set, and call $b_1, \dots, b_t$ the elements of the set which are less than $p/2$, and $c_1, \dots, c_u$ the elements which are greater than $p/2$, then it must be that
  
  $0 < b_1, \dots, b_t, p - c_1, \dots, p - c_u < p/2$

  Also, each of these are distinct because if $b_i = p - c_j$ then

  $b_i + c_j = p$

  but this is impossible because $c_j - p < p/2$ and $b_i < p/2$, hence they must be different.
  
</p>
 
 
