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
\ddot{z}\, .\]` Dredging still further, we might remember that momentum is
:raw-html:`\(p = m\dot{z}\)`, which gives us dynamics :raw-html:`\[\dot{z} =
\frac{1}{m} p \, , \qquad \dot{p} = -kz - \frac{\nu}{m} p + \varphi(t) \, .
\qquad \mathrm{(1)} \]`

Next, let us consider an SIRS model with forcing, :raw-html:`\[\dot{S} = \omega
R - \beta(t) S I \, , \quad\ \dot{I} = \beta(t) S I - \gamma I \, , \quad
\dot{R} = \gamma I - \omega R \, .\]` This models a system where individuals move
from susceptible to infections upon contact with other infectious individuals,
then recover, and after that immunity wanes and they become infectious again.
the rate :raw-html:`\(\beta(t)\)` depending on time is supposed to capture
different exogenous events: schools opening and closing; new vaccines; new
variants; policy changes; and all sorts of other complexity. If you want to
experiment with these equations numerically, check out `this Jupyter notebook
<https://github.com/thomasallanhouse/covid19-incidence/blob/main/bmj.ipynb>`__
that I make available on GitHub.

This set of equations does not have a general closed form, but we can look for
an approximate one using the Ansatz :raw-html:`\[S(t) = S_* + \epsilon x(t) \,
, \quad\ I(t) = I_* + \epsilon y(t) \, , \quad R(t) = N - S(t) - I(t) \, ,
\quad \beta(t) = \beta_* + \epsilon \phi(t) \, .\]` We want this to correspond
to a fixed point of the dynamical system when :raw-html:`\(\epsilon = 0\)`,
leading to the equations :raw-html:`\[0 = \omega (N - S_* - I_*) - \beta_* S_*
I_* \, , \qquad\ 0 = \beta_* S_* I_* - \gamma I_* \, .\]` These have a solution
when :raw-html:`\(I_* = 0\)` that is unstable if the disease can go endemic,
i.e. when :raw-html:`\(\mathcal{R}_0 = \beta_*/\gamma > 1 \)`; the other fixed
point is when :raw-html:`\(I_* = 1 - (1/\mathcal{R}_0)\)`, which I hope to blog
about later. The expression for the expected number of susceptibles
:raw-html:`\(S_*\)` at endemicity is more complex; feel free to derive it for
fun!  For our purposes here, we are interested in what we obtain at first order
in :raw-html:`\(\epsilon\)`, which gives us :raw-html:`\[\dot{x} = - \omega x -
\omega y - \beta_* x I_* - \beta_* S_* y - \phi S_* I_* +
\mathcal{O}(\epsilon^2)  \, , \qquad\ \dot{y} = \beta_* x I_* + \beta_* S_* y +
\phi S_* I_* - \gamma y  + \mathcal{O}(\epsilon^2) \, .  \qquad \mathrm{(2)}
\]`

OK, so take a breath. Now, with a bit of work, we can write both equations (1)
and (2) (neglecting quadratic terms in :raw-html:`\(\epsilon\)`) above in the
form of a two-dimensional vector differential equation
:raw-html:`\[\dot{\mathbf{v}} = \boldsymbol{J} \mathbf{v} + \mathbf{F}(t) \, ,
\qquad \mathrm{(3)} \]` where :raw-html:`\(\mathbf{v}\)` is a vector containing
the dynamical variables -- :raw-html:`\((z,p)\)` for the spring and
:raw-html:`\((x,y)\)` for the SIRS model -- :raw-html:`\(\boldsymbol{J}\)` is a
matrix depending on rate constants, and :raw-html:`\(\mathbf{F}(t)\)` is a
vector function of time. The eagle-eyed will note that the details of the
versions of (3) derived from (1) and (2) are not quite the same, but also that
equation (3) takes the same structure under the linear transformation
:raw-html:`\[\tilde{\mathbf{v}} = \boldsymbol{T} \mathbf{v} \, ,\quad
\tilde{\boldsymbol{J}} = \boldsymbol{T}\boldsymbol{J}\boldsymbol{T}^{-1} \,
,\quad \tilde{\mathbf{F}} = \boldsymbol{T} \mathbf{F} \, . \]` They might also
have fun trying to work with (3) via matrix integrating factor, Eigensystem
analysis, or maybe Fourier transform.

So, that was quite fiddly (although not much beyond high-school level
mathematics apart from the last bit). But the TL;DR is this: imagine all the
complexity that you can generate by bouncing a weight up and down. If your taps
line up just right with the how the spring behaves, you can get regular
oscillations, but it's not difficult to make the weight jump irregularly all
over the place. And this is exactly what we can see with an endemic disease:
there's no guarantee that oscillatory behaviour will be regular or predictable.

Now, for many diseases that are  

