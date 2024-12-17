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

   $((p - 1)/2)! \equiv (2)(4)(6) \dots (p - 5)(p - 3)(p - 1)(- 1)^{(p^2 - 1)/8} \equiv (- 1)(2)(- 3)(4) \dots ((p - 1)/2)(- 1)^{(p^2 - 1)/8} (\mod p)$<br>
   $->$<br>
   $2^{(p - 1)/2}((p - 1)/2)! \equiv ((p - 1)/2)!(- 1)^{(p^2 - 1)/8} \mod p$<br>
   $->$<br>
   $2^{(p - 1)/2} \equiv (- 1)^{(p^2 - 1)/8} \mod p$

   where the second step is quite tricky, and it basically means that
   
   $(2)(4)(6) \dots (p - 5)(p - 3)(p - 1) \equiv (2)(4)(6) \dots (p - 5)(p - 3)(p - 1) (\mod p)$
   
   and $(p^2 - 1)/8$ is derived using the Gauss' Formula:

   $\displaystyle \frac{(p - 1)/2((p - 1)/2 + 1)}{2} = \frac{(p - 1)/2(p + 1)/2}{2} = \frac{p^2 - 1}{8}$

   Now we can further analyze when $(p^2 - 1)/8$ is even. 

   $\displaystyle \frac{p^2 - 1}{8}$<br>
   $->$<br>
   $\displaystyle \frac{(p - 1)(p + 1)}{8}$<br>

   If either $p - 1 | 8$ or $p + 1 | 8$ (can't be both) our result will be matched since both are even. Thus

   $p \pm 1 \equiv 0 \mod 8$<br>
   $->$<br>
   $p \equiv 1 \mod 8$ or $p \equiv - 1 \mod 8$

   Now, the problem with the initial hypothesis is that we can't be sure it covers every case.
   Let's analyze every other possible case.

   $p \equiv 3 \mod 8$<br>
   $->$<br>
   $p + 1 \equiv 4 \mod 8$<br>
   $p - 1 \equiv 2 \mod 8$

   From the **multiplication property** this would produce $(p - 1)(p + 1) \equiv 0 \mod 8$, and $4 \cdot 2 = 8, 8 / 8 = 1$ which is odd. Now why is this enough to say that the result will be odd? Imagine $(p - 1)/8$ and $(p + 1)/8$ as separated entities, the results will be even or odd, but if we sum these quotients we get an even result. Now since we know that the final remainders will produce an odd result we see that $even + odd = odd$. Same below.

   $p \equiv 5 \mod 8$<br>
   $->$<br>
   $p + 1 \equiv 6 \mod 8$<br>
   $p - 1 \equiv 4 \mod 8$

   From the **multiplication property** this would produce $(p - 1)(p + 1) \equiv 0 \mod 8$, and $6 \cdot 4 = 24, 24 / 8 = 3$ which is odd. Hence we see that if

   $p \equiv \pm 1 \mod 8$

   $2^{(p - 1)/2} \equiv 1 \mod p$

   otherwise if

   $p \equiv \pm 3 \mod 8$

   then

   $2^{(p - 1)/2} \equiv - 1 \mod p$

   </p>

 ## The '3' case

 <p>

   By Gauss' Lemma
   
   $3^{(p - 1)/2} \equiv (- 1)^u \mod p$

   We have the same problem faced above, that is, to find $u$. Recalling that $u$ is the number of elements of the set we seen above which is $> p/2$, we find that (substituting $q$ with $3$) the set we are looking for will be

   $3 \cdot \\{(p - 1)/6 + 1, \dots, (p - 1)/3\\}$

   Thus

   $\displaystyle \frac{p - 1}{3} - \frac{p - 1}{6} = \frac{p - 1}{6}$

   is the number of elements of the previous set. This means that we will end up having

   $3^{(p - 1)/2} \equiv (- 1)^{(p - 1)/6} \mod p$

   Thus we'll have $(p - 1)/6$ even for

   $(p - 1)/6 = 2m$<br>
   $->$<br>
   $p - 1 = 12m$<br>
   $->$<br>
   $p \equiv 1 \mod 12$

   Now considering the odd result we would have

   $(p - 1)/6 = 2m + 1$<br>
   $->$<br>
   $p - 1 = 12m + 6$<br>
   $->$<br>
   $p \equiv 7 \mod 12$

   Since $7 \mod 12 = - 5 \mod 12$ we end up having

   $3^{(p - 1)/2} \equiv - 1 \mod p$

   if

   $p \equiv - 5 \mod 12$

   and 

   $3^{(p - 1)/2} \equiv 1 \mod p$

   if

   $p \equiv 1 \mod 12$

   These results are partially correct for some arcane reason that we will probably better understand after the following sections. Most of the times very little explanations are made involving this stuff and so I tried to find complete solutions looking around on the web. For more you could also check [http://mathonline.wikidot.com/legendre-symbol-rules-for-3-p-and-6-p#:~:text=Legendre%20Symbol%20(3%2Fp),-Determine%20a%20rule&text=We%20first%20note%20that%20p,or%2011%20(mod%2012).].
   
 </p>
   
   ### Quadratic reciprocity prelude (yet another Gauss' Theorem)

   Let $p$ be an odd prime and $q$ an integer which is coprime with $p$. Let

   $m = q/p + q2/p + \dots + q(p - 1)/2/p$

   then 

   $m \equiv u \mod 2$

   The proof for this theorem can be found at [https://crypto.stanford.edu/pbc/notes/numbertheory/quadrecip.html]. I won't copy paste it since it would be useless. This theorem is important because knowing such result allows us to use $m$ instead of $u$ to derive the results of Gauss' Lemma, which simplify the process a lot.
   
 </p>

## Eisenstein's Lemma

<p>
  
  $a^{(p - 1)/2} \equiv (- 1)^{\sum_{u}\lfloor au/p \rfloor} (\mod p)$

  where

  $\lfloor x \rfloor = floor(x)$

  Let $u$ be any even integer in the set $\\{1, \dots, p - 1\\}$. Let $a$ any positive integer coprime with $p$, and $r(u) = au \mod p$, then

  $(- 1)^{r(u)}r(u)$

  is even. Furthermore every result will be distinct because if

  $au_1 \equiv au_2 \mod p$

  then $p | u_1 - u_2$ which is impossible since they are even. This means that there will be exactly $(p - 1)/2$ results mapped by $r(u)$ and every one of them will be distinct and therefore that these results will be a rearrangement of $\\{2, 4, \dots, p - 1\\}$ since they are all even. Multiplying them we get

  $(- 1)^{r(2)}2a \cdot (- 1)^{r(4)}4a \cdot \dots \cdot (- 1)^{r(p - 1)}(p - 1)a \equiv 2 \cdot 4 \cdot \dots \cdot (p - 1) (\mod p)$

  Using the **cancellation law** we get

  $a^{(p - 1)/2}(- 1)^{r(2) + r(4) + \dots + r(p - 1)} \equiv 1 \mod p$

  This means that $a^{(p - 1)/2}$ always produce a remainder $\pm 1$ which has the same sign as $(- 1)^{r(2) + r(4) + \dots + r(p - 1)}$, and then

  $a^{(p - 1)/2} \equiv (- 1)^{r(2) + r(4) + \dots + r(p - 1)} \mod p$

  Now we can note that 

  $\displaystyle \frac{au}{p} = \lfloor \frac{au}{p} \rfloor + \frac{r(u)}{p}$

  keeping in mind that $au/p$ won't be integer. From this result we can notice that

  $\displaystyle au = p \lfloor \frac{au}{p} \rfloor + r(u)$

  and since $p$ is odd and $u$ even, that $\lfloor au/p \rfloor$ and $r(u)$ are congruent $\mod 2$. To better understand this last step, note that $au$ will be always even, and to get an even result on the right we will need $r(u)$ and $\lfloor au/p \rfloor$ congruent $\mod 2$ (they are both even or odd). This because $p$ is always odd and $odd \cdot odd = odd$, in such case we will necessary have $r(u)$ odd too because $odd + odd = even$ (but $odd + even = odd$). In the case where $\lfloor au/p \rfloor$ will be even we will have $odd \cdot even = even$, therefore if $r(u)$ was odd we would end up having $even + odd = odd$ which is wrong because $au$ is even, and therefore $r(u)$ should be even and finally this means that we necessary have

  $\displaystyle \lfloor \frac{au}{p} \rfloor \equiv r(u) \mod 2$

  This is a more elegant way to prove this fact compared to Gauss' Theorem.<br>
  Now to finally complete the lemma, since they are congruent $\mod 2$ we can use $\displaystyle \lfloor \frac{au}{p} \rfloor$ instead of $r(u)$ as exponent into the previous result and see that

  $a^{(p - 1)/2} \equiv (- 1)^{\sum_{u}\lfloor au/p \rfloor} (\mod p)$

  where $\sum_{u}\lfloor au/p \rfloor$ is the summation for every $u$ in the set

  $\\{2, 4, \dots, p - 1\\}$
  
</p>

 ## ~Eisenstein's proof of quadratic reciprocity

 <p>
   Let $p, q$ be two prime numbers. We can see that this is more than enough to state

   $\displaystyle (\frac{q}{p}) = q^{(p - 1)/2} \equiv (- 1)^{\sum_{u}\lfloor qu/p \rfloor} (\mod p)$

   and

   $\displaystyle (\frac{p}{q}) = p^{(q - 1)/2} \equiv (- 1)^{\sum_{u}\lfloor pu/q \rfloor} (\mod q)$

   Now, let's try to make this magical proof to work. Consider

   $\sum_{u}\lfloor qu/p \rfloor + \sum_{u}\lfloor pu/q \rfloor$

   We can rewrite these as

   $2(\sum_{Z = 1}^{(p - 1)/2} \lfloor qZ/p \rfloor + \sum_{Z = 1}^{(q - 1)/2} \lfloor pZ/q \rfloor)$
   
   because

   $2 = 1(2)$<br>
   $4 = 2(2)$<br>
   $6 = 3(2)$<br>
   $\dots$

   Now you should try to refer to [https://dms.umontreal.ca/~revealed/App8A.pdf] (last part). We can start by analyzing

   $\sum_{Z = 1}^{(p - 1)/2} \lfloor qZ/p \rfloor$

   and note that for ex., computing

   $\displaystyle \frac{q(p - 1)/2}{p}$

   means that we are multiplying $q$ by a value which is less than half $p$, and then we divide by $p$. It follows almost intuitively that the result will fall under $q/2$. Now consider the geometrical structure which Eisenstein made. Consider the line which splits the rectangle $R$ in half: the formula of the line is

   $py = qx$<br>
   $->$<br>
   $y = qx / p$

   Let's consider $q > p$ for simplicity, so you can refer to $a$ as $q$ and $b$ as $p$ in the pictures of the linked paper; everything should be more intuitive setting this constraint. We can see how the previous formula of the line simply scale $x$ by $q/p$ factor, which is quite intuitive. Now let's retake the previous formula

   $\displaystyle \frac{q(p - 1)/2}{p}$

   We said this value must be lower than $q/2$; do you notice any correlation with our line formula? They are the exact same formula (substituting $x$ with $Z$). Now our initial formula had the floor function, then we need to rewrite the latter as

   $\displaystyle \lfloor \frac{q(p - 1)/2}{p} \rfloor$

   It's really intuitive now to see that the results of this formula will always be lower than the previous one, since $qZ / p$ will never be an integer. We can see every term which will be erased by the floor function compared to $\displaystyle \frac{qZ}{p}$, iterating on $Z$ backwards and solving the numerator making it dependent on $(p - 1)/2$, $\displaystyle \frac{q(p - 1)/2}{p} = \frac{qp/2}{p} - \frac{q/2}{p} \mapsto - \frac{q/2}{p}$ (as we did earlier in the '2' case of Gauss Lemma), by

   $- q/2, - 3q/2, - 5q/2, \dots, - (q/2 - 7q/2), - (q/2 - 5q/2), - (q/2 - 3q/2)$<br>
   $->$<br>
   $- q/2, - 3q/2, - 5q/2, \dots, 3q, 2q, q$

   I know this looks completely nonsense, how is that possible that the floor function adds where it clearly only subtracts? Well ask god why is that, I think that the reason is that what we are actually finding is not that the floor function adds something. We can notice that for ex.

   $- 3q/2 = (q - 3)/2= (q - 1)/2 - 1$

   and therefore

   $\sum_{Z = 1}^{(p - 1)/2} \\{ qZ/p \\} = (q^2 - 1)/8$

   where $\\{ x \\}$ in this case means 'the fractional part of $x$'.<br>
   Now this means that

   $\sum_{Z = 1}^{(p - 1)/2} \lfloor qZ/p \rfloor + \sum_{Z = 1}^{(p - 1)/2} \lfloor pZ/q \rfloor = \sum_{Z = 1}^{(p - 1)/2} qZ/p - (q^2 - 1)/8 + \sum_{Z = 1}^{(p - 1)/2} pZ/q - (p^2 - 1)/8$

   and therefore since

   $\sum_{Z = 1}^{(p - 1)/2} qZ/p + \sum_{Z = 1}^{(p - 1)/2} pZ/q = q(p^2 - 1)/8p + p(q^2 - 1)/8q$<br>
   $->$<br>
   $\sum_{Z = 1}^{(p - 1)/2} \lfloor qZ/p \rfloor + \sum_{Z = 1}^{(p - 1)/2} \lfloor pZ/q \rfloor = q(p^2 - 1)/8p - (p^2 - 1)/8 + p(q^2 - 1)/8q - (q^2 - 1)/8$<br>
   $->$<br>
   $\displaystyle q(p^2 - 1)/8p - (p^2 - 1)/8 + p(q^2 - 1)/8q - (q^2 - 1)/8 = \frac{(q - p)(p^2 - 1)/8)}{p} + \frac{(p - q)(q^2 - 1)/8)}{q} = \frac{q(q - p)(p^2 - 1)/8) + p(p - q)(q^2 - 1)/8)}{pq} = \frac{q^2(p^2 - 1)/8) - pq(p^2 - 1)/8) + p^2(q^2 - 1)/8) - pq(q^2 - 1)/8)}{pq}$
   $->$<br>
   $\frac{q^2(p + 1)(p - 1)/8 - pq(p^2 - 1)/8 + p^2(q + 1)(q - 1)/8 - pq(q^2 - 1)/8}{pq} = \frac{(q^2p - q^2 + q^2p + q^2)/8 - pq(p^2 - 1)/8 + (p^2q - p^2 + p^2q + p^2)/8 - pq(q^2 - 1)/8}{pq} = \frac{2(q^2p)/8 - pq(p^2 - 1)/8 + 2(p^2q)/8 - pq(q^2 - 1)/8}{pq}$
   $->$<br>
   $\displaystyle \frac{2(q^2p)/8 - pq(p^2 - 1)/8 + 2(p^2q)/8 - pq(q^2 - 1)/8}{pq} = q/4 - (p^2 - 1)/8 + p/4 - (q^2 - 1)/8$

   we basically map every lattice point of the triangle $A$. Since it is delimited by $[1, (p - 1)/2]$ (left, right) and $Z \lfloor q/p \rfloor = Z$ (upper) with $Z = \\{1, 2, \dots, (q - 1)/2\\}$ we can calculate the area of the triangle and find every lattice point which coincides with the intial summation result, then

   $\displaystyle \frac{(p - 1)(q - 1)}{8}$

   and

   $2(\sum_{Z = 1}^{(p - 1)/2} \lfloor qZ/p \rfloor + \sum_{Z = 1}^{(q - 1)/2} \lfloor pZ/q \rfloor)$
   $->$<br>
   $\displaystyle \frac{(p - 1)(q - 1)}{4}$
   
   
 </p>


   

   

   
 </p>
