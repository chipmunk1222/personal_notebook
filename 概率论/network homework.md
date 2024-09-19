**Binomial distribution:
- definition: Bin(n,p)~an event with n sample point,each point has p probability to success.
- algorithm:$$P(X=x)=C_n^xp^x(1-p)^{n-x}$$
- Validty:$$\Sigma_{i=0}^nC_np^i(1-p)^{n-i}=(p+(1-p))^n=1$$
- expectation:$E(X)=np$
- varience:Var(X)=$np(1-p)$
- monotonicity:$$\frac{p(i)}{p(i-1)}=\frac{C_n^ip^i(1-p)^{n-i}}{C_n^{i-1}p^{i-1}(1-p)^{n-i+1}}=\frac{(n-i+1)p}{i(1-p)}$$
- so$(n-i+1)p>=(i(1-p))=>p(i)>p(i-1)$

**Bernoulli Binomial random variable:
- defination:special Binomial distribution with n=1
- character:$P(X=0)=1-p , P(X=1)=p$

*Continuous Random Variable:*

**Normal random variable:
- defination:X~N(μ，$\sigma^2$)->normal distribution with mean value of μ and varience of σ^2
- algorithm:$$f(x)=\frac{1}{\sigma\sqrt{2\pi}}exp\{-\frac{(x-\mu)^2}{2\sigma^2}\},-\infty<x<+\infty$$
- Validity:$$I = \int_{-\infty}^{\infty}e^{-\frac{x^2}{2}}dx=\sqrt{2\pi}$$
$$\int_{-\infty}^{\infty}f(x)dx=f(x)=\frac{1}{\sigma\sqrt{2\pi}}\int_{-\infty}^{\infty} exp\{-\frac{(x-\mu)^2}{2\sigma^2}\}dx$$<=>$$y=\frac{x-\mu}{\sigma},\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{\infty}e^{-y^2/2}dy=1,-\infty<x<+\infty$$
- expectation:E(X)=μ
- varience:Var(X)=σ^2

**normalize:
- defination:X~N(μ，$\sigma^2$) = Z~N(0,1)
- algorithm：$$Z=\frac{X-\mu}{\sigma},P(x_1<X<x_2)=P(z_1<Z<z_2)$$
- characristic:E(Z)=0,Var(Z)=1

**cumulative distribution:
- algorithm:$$\Phi(x)=\int_{-\infty}^x\frac{1}{\sqrt{2\pi}}e^{-\frac{y^2}{2}}dy$$
- characteritic:Z~N(0,1),$\Phi(-x)=1-\Phi(x)$
- X~N(μ，σ^2),$F_x(x)=\Phi(\frac{x-μ}{\sigma})$
- $$Z=\frac{X-\mu}{\sigma},P(x_1<X<x_2)=P(z_1<Z<z_2)=\Phi(\frac{x_2-\mu}{\sigma})-\Phi(\frac{x_1-\mu}{\sigma})$$
- find the table to get the result