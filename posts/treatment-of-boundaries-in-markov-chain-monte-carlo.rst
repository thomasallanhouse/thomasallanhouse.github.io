.. title: Treatment of boundaries in Markov chain Monte Carlo
.. slug: treatment-of-boundaries-in-markov-chain-monte-carlo
.. date: 2025-04-14 14:35:10 UTC
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

.. role:: raw-html(raw)
   :format: html

I have been asked by multiple students what to do with MCMC at
boundaries, in particular how to treat proposals that lie outside the
support of the target. Suppose we have a vector of parameters
:math:`\theta` and want to target a density (proportional to)
:math:`\pi(\theta)` using a proposal distribution
:math:`q(\theta'|\theta)`. In MCMC, we seek to define a Markov process
in discrete time, :math:`(\theta_0, \theta_1, \ldots, \theta_N)` that
has stationary distribution with density :math:`\pi`. In the Metropolis
Hastings scheme, the law of such a process is that at step :math:`m`,
when the state of the system is :math:`\theta_m`, we pick a proposed new
value :math:`\tilde{\theta}` with density :math:`q(\cdot | \theta_m)`,
then

.. math::


   \mathrm{Pr}(\theta_{m+1} = \tilde{\theta}) = \mathrm{max}\left( 1, \frac{\pi(\tilde{\theta}) q(\theta | \tilde{\theta})}{\pi(\theta)q(\tilde{\theta} | \theta)}\right) \, , \quad
   \mathrm{Pr}(\theta_{m+1} = \theta_{m}) = 1 - \mathrm{Pr}(\theta_{m+1} = \tilde{\theta}) \, . \quad (\dagger)

The natural question is, if there is somewhere we can
propose but not move (e.g. because the likelihood is not defined) then
what should be done?

Let us consider one parameter, a probability :math:`p\in [0,1]`, with a
density :math:`\pi(p) = \mathrm{Uniform}(0,1)`, and a proposal
distribution :math:`q(p'|p) = \mathcal{N}(p'|p,1)`. We will run chains
of length :math:`N=10^7`.

.. container:: cell

   .. code:: r

      N <- 10000000
      output <- matrix(0,ncol=2,nrow=N)
      sig <- 1

In the first chain (‘Keep picking’) we will keep proposing new values
until one is within the allowed region

.. container:: cell

   .. code:: r

      p <- 0.5
      for(m in 1:N){
        pprop <- -1
        while((pprop<0)|(pprop>1)){
          pprop <- p + rnorm(1,mean=0,sd=sig)
        }
        p <- pprop
        output[m,1] <- p
      }

In the second chain (‘Reject’) we will reject proposals outside the
region and remain at the position the proposal was made.

.. container:: cell

   .. code:: r

      p <- 0.5
      for(m in 1:N){
        pprop <- p + rnorm(1,mean=0,sd=sig)
        if((pprop>=0)&(pprop<=1)){
          p <- pprop
        }
        output[m,2] <- p
      }

Now look at some plots

.. container:: cell

   .. code:: r

      hist(output[,1], breaks=seq(0,1,0.1), freq=FALSE, ylim=c(0,1.2),
           xlab='p', main='Keep picking')

   .. container:: cell-output-display

      .. image:: ../unnamed-chunk-4-1.png
         :width: 672px

   .. code:: r

      hist(output[,2], breaks=seq(0,1,0.1), freq=FALSE, ylim=c(0,1.2),
           xlab='p', main='Reject')

   .. container:: cell-output-display

      .. image:: ../unnamed-chunk-4-2.png
         :width: 672px

   .. code:: r

      ts.plot(output[1:500,1],gpars=list(xlab="m", ylab="p"))

   .. container:: cell-output-display

      .. image:: ../unnamed-chunk-4-3.png
         :width: 672px

   .. code:: r

      ts.plot(output[1:500,2],gpars=list(xlab="m", ylab="p"))

   .. container:: cell-output-display

      .. image:: ../unnamed-chunk-4-4.png
         :width: 672px

What we see is that the first approach, the trace plot looks
superficially ‘better’, but the output is biased. From the
Metropolis-Hastings algorith as specified in :math:`(\dagger)` this is what we
would expect; mathematically, we can interpret the ‘Reject’ approach as
taking :math:`\pi(\theta<0) = \pi(\theta>1) = 0`, while the ‘Keep
picking’ approach the proposal distribution effectively becomes a
truncated normal. Such a truncated normal could be evaluated as the
:math:`q(\cdot|\cdot)` in :math:`(\dagger)`, and this might be a good algorithm,
but the naïve implementation introduces bias.

