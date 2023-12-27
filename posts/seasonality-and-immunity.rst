.. title: Seasonality and Immunity
.. slug: seasonality-and-immunity
.. date: 2021-08-18 18:33:04 UTC
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
.. has_math: true

.. role:: raw-html(raw)
   :format: html

**Note:** This blogpost was conceptualised in August 2021, and should be public
early in 2024. My attempts to do long-form outreach were somewhat put on hold
by work around the COVID pandemic. Anyway, with the problems going on at 𝕏
(formerly Twitter), it's struck me that putting any such content on a website
that I control probably has its advantages, so I hope to use this site more
going forwards.

.. image:: ../spring.jpg
   :width: 240px
   :alt: Spring being pushed, with displacement z from equilibrium
   :align: right

So let's start by considering a weight on a spring as pictured - this is going
to give us a physical 'model' of disease dynamics for an endemic infection. The 
weight on the spring is a distance :raw-html:`\(z(t)\)` from the point at which
the system would be at rest. There are three forces acting on the weight:

* The spring pulls it towards equilibrium, to a first approximation,
  proportionally to its spring constant giving a force contribution
  :raw-html:`\(k z\)`;

* As the weight moves, friction dissipates kinetic energy giving a force
  contribution :raw-html:`\(\nu \dot{z}\)`;

* A human is pushing at the weight giving a time-dependent force contribution
  :raw-html:`\(\varphi(t)\)`.

Now, dredging up our high-school physics we remember that Newton's equation is
:raw-html:`\(F = ma\)`. Noting that acceleration is the second derivative of
position so that :raw-html:`\(a = \ddot{z}\)` and combining the three force
contributions above we get :raw-html:`\[-kz - \nu \dot{z} + \varphi(t) = m
\ddot{z}\, .\]`

and :raw-html:`\(p = m\dot{z}\)`
respectively

Next, let us consider an SIRS model with forcing, :raw-html:`\[\dot{S} = \omega
R - \beta(t) S I \, , \quad\ \dot{I} = \beta(t) S I - \gamma I \, , \quad
\dot{R} = \gamma I - \omega R \, .\]` This set of equations does not have a
general closed form, but we can look for an approximate one using the Ansatz
:raw-html:`\[S(t) = S_* + \epsilon x(t) \, , \quad\ I(t) = I_* + \epsilon y(t)
\, , \quad R(t) = N - S(t) - I(t) \, , \quad \beta(t) = \beta_* + \epsilon
\phi(t) \, .\]`. We want this to correspond to a fixed point of the dynamical
system when :raw-html:`\(\epsilon = 0\)`, leading to the equations
:raw-html:`\[0 = \omega (N - S_* - I_*) - \beta_* S_* I_* \, , \qquad\ I_* =
\beta_* S_* I_* - \gamma I_* \, .\]` These have a solution when
:raw-html:`\(I_* = 0\)` that is unstable if the disease can go endemic (which
happens when :raw-html:`\(\mathcal{R}_0 = \beta_*/\gamma > 1 \)`; otherwise we
have the interesting result that :raw-html:`\(I_* = 1 - (1/\mathcal{R}_0)\)`,
which I hope to blog about later. The expression for the expected number of
susceptibles at endemicity is more complex; feel free to derive it for fun!
For our purposes here, we are 

