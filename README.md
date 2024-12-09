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

   This test exploit the difference between primes subgroups structure and non-primes one, i.e. the structure of subgroups follow $\phi(n)$ is way different between primes and non-primes, thus every time we iterate we are basically breaking the structure and finding random numbers. Also for every iteration the probability to find a number which fools the test decreases exponentially by a factor of $\displaystyle \frac{1}{4}$. I guess that this number derives directly from our reasoning about $p \equiv 1 \mod 4$. Just note this:

   $a^{(n - 1) / 2} \not\equiv a^{\phi(n) / 2}$ for non-primes

   also $- 1$ does not appear around in every multiplicative subgroup, thus it's almost impossible to fool the test. Things should be analyzed better but I don't have the time to do it so for the moment I'm not delving this method further.
 </p>

## Gauss' Lemma

<p>
  I'm going straight to the proof here, refer to [https://crypto.stanford.edu/pbc/notes/numbertheory/gausslemma.html]. The linked resource is more than enough, I'm just rewriting the proof for completeness and for study purposes, also I'll provide a couple steps which could seem more intuitive compared to the linked proof.

  Let $p$ an odd prime and $q$ an integer coprime (i.e. every integer in the $[1, \dots, p - 1]$ set is fine). We compute

  $\\{q, q2, \dots, q(p - 1)/2\\} (\mod p)$

  Now we analyze this set, and call $b_1, \dots, b_t$ the elements of the set which are less than $p/2$, and $c_1, \dots, c_u$ the elements which are greater than $p/2$. Every $b_i \neq b_j, c_i \neq c_j (i \neq j)$ (easily provable using the **cancellation law**). Then it must be that
  
  $0 < b_1, \dots, b_t, p - c_1, \dots, p - c_u < p/2$

  and each of these are distinct because if $b_i = p - c_j$ then

  $b_i + c_j = p$<br>
  $->$<br>
  $b_i + c_j - p = 0$

  but this is impossible because $c_j - p < p/2$ and $b_i < p/2$, hence they must be different. This means that

  $q(q2)\dots (q(p - 1)/2) \equiv (- 1)^{u}b_1 \dots b_t(p - c_1) \dots (p - c_u) (\mod p)$

  because since every 

  $0 < b_1, \dots, b_t, p - c_1, \dots, p - c_u < p/2$

  is different, then they map every number in the set $[1, \dots, (p - 1)/2]$. To set the equality we just need to see how the original $q$ set is the same as this if we consider $(- 1)^u$.<br>
  Now restarting from

  $q(q2)\dots (q(p - 1)/2) \equiv (- 1)^{u}b_1 \dots b_t(p - c_1) \dots (p - c_u) (\mod p)$<br>
  $->$<br>
  $q^{(p - 1)/2}((p - 1)/2)! \equiv (- 1)^{u}((p - 1)/2)! (\mod p)$

  Now to safely remove that co-factor we can use the **cancellation law**, i.e. since $((p - 1)/2)! \nmid p$ it must be that

  $q^{(p - 1)/2} \equiv (- 1)^{u} (\mod p)$ _
  
  or using the Legendre Symbol:

  $\displaystyle (\frac{q}{p}) = (- 1)^{u}$
  
</p>

## Gauss' Formula

<p>
  When he was like $0$ years old Gauss proved that the sum of elements of the set $[1, 2, \dots, n]$ is

  $\displaystyle \frac{n(n + 1)}{2}$

  I don't want to prove this but it's easy (he proved it at $10$ years or something like that, then you can understand it quite easily, as long as he was a genius, a $10$ years old boy can't compete with an average $20$ years old guy). To understand it, do it as a funny math game and find a smart way to compute the sum of numbers from $1$ to $100$. You'll end up finding that formula, and you also could propose this simple problem to your friends (and lose them).
</p>

 ## The '2' case of Gauss' Lemma

 <p>
   The problem with the Gauss' Lemma is clearly to know $u$. For $q = 2$ we have
   
   $\displaystyle (\frac{2}{p}) = (- 1)^{(p^2 - 1)/8} = (- 1)^{(p + 1)/4}$
   
   Let's get why. Restarting from

   $q^{(p - 1)/2}((p - 1)/2)! \equiv ? (\mod p)$

   we can break down $((p - 1)/2)!$ as

   $1 = (- 1)(- 1)$<br>
   $2 = (2)(- 1)^2$<br>
   $3 = (- 3)(- 1)^3$<br>
   $\dots$<br>
   $(p - 1)/2 = (p - 1)/2(- 1)^{(p - 1)/2}$

   It's easy to see that the lelft part produces $((p - 1)/2)!$, while for the right part we can further split it and take the left part:

   $- 1$<br>
   $2$<br>
   $- 3$<br>
   $\dots$<br>
   $(p - 1)/2$

   Now before considering the $(- 1)^?$ we can introduce our $2$ which substitutes $q$ and note that considering the numbers backwards we get

   $2(p - 1)/2 \mod p = - 1 \mod p$<br>
   $2((p - 1)/2 - 1) \mod p = 2(p - 3)/2 \mod p = - 3 \mod p$<br>
   $2((p - 1)/2 - 2) \mod p = 2(p - 5)/2 \mod p = - 5 \mod p$<br>
   $\dots$<br>
   $2((p - 1)/2 - ((p - 1)/2 - 3)) \mod p = 2(6/2) = 6 \mod p$<br>
   $2((p - 1)/2 - ((p - 1)/2 - 2)) \mod p = 2(4/2) = 4 \mod p$<br>
   $2((p - 1)/2 - ((p - 1)/2 - 1)) \mod p = 2(2/2) = 2 \mod p$<br>

   Thus

   $((p - 1)/2)! \equiv (2)(4)(6) \dots (p - 5)(p - 3)(p - 1)(- 1)^{(p^2 - 1)/8} \equiv (- 1)(2)(- 3)(4) \dots ((p - 1)/2)(- 1)^{(p - 1)/2} (\mod p)$<br>
   $->$<br>
   $2^{(p - 1)/2}((p - 1)/2)! \equiv ((p - 1)/2)!(- 1)^{(p^2 - 1)/8} \mod p$<br>
   $->$<br>
   $2^{(p - 1)/2} \equiv (- 1)^{(p^2 - 1)/8} \mod p$

   where the second step is quite hard, and $(p^2 - 1)/8$ is derived using the Gauss' Formula:

   $\displaystyle \frac{(p - 1)/2((p - 1)/2 + 1)}{2} = \frac{(p - 1)/2(p + 1)/2}{2} = \frac{p^2 - 1}{8}$

   ### Quadratic reciprocity prelude

   Let $p$ be an odd prime and $q$ an integer which is coprime with $p$. Let

   $m = q/p + q2/p + \dots + q(p - 1)/2/p$

   then 

   $m \equiv u \mod 2$

   Here we can immediately spot that this structure is almost the same as the one we saw in the Gauss' Lemma, the difference is that the numbers are added together and are divided by $p$.
   
 </p>

 ### Theorem of quadratic reciprocity

 <p>
   
 </p>
