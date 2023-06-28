.. title: Spreading of Mood on Social Networks
.. slug: spreading-of-mood-on-social-networks
.. date: 2015-08-20 12:00:00 UTC
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
.. has_math: true

.. role:: raw-html(raw)
   :format: html

Together with `Ed Hill
<http://www2.warwick.ac.uk/fac/cross_fac/complexity/people/students/dtc/students2012/hill/>`__
and `Frances Griffiths <http://www2.warwick.ac.uk/fac/med/staff/griffiths/>`__,
I had a `paper out in Proceedings B yesterday
<http://rspb.royalsocietypublishing.org/content/282/1813/20151180/>`__.  There
has been a bit of media interest in the paper (e.g. `The Atlantic
<http://www.theatlantic.com/health/archive/2015/08/how-friendship-fights-depression/401807/>`__
and the `Daily Telegraph
<http://www.telegraph.co.uk/news/science/science-news/11809754/Depression-is-not-contagious-but-an-upbeat-mood-is-say-scientists.html>`__)
but I assume that anyone reading this page is more interested in how the
mathematics works. This is given in relatively full detail in the paper and
`Supplementary Material
<https://royalsocietypublishing.org/action/downloadSupplement?doi=10.1098%2Frspb.2015.1180&file=rspb20151180supp1.pdf>`__,
so below I give a more informal account.

A ubiquitous problem in epidemiology is *confounding*, which is (very loosely
speaking) where something else correlates with the actual causal mechanism for
disease. In the current context, the issue is that there may be clusters of ill
people on a social network due to spreading of the illness on the network, or
it could be that people who share a risk factor tend to be linked on the
network. So for depression (which we studied) it could be that people who drink
heavily tend to be friends, but it is the drinking that causes the clusters of
depression rather than the friendships.

There is a lot of interesting discussion of such questions in the context of
social networks in a `Special issue of Statistics in Medicine
<http://onlinelibrary.wiley.com/doi/10.1002/sim.v32.4/issuetoc>`__. Personally,
I tend to think that while it is never possible to eliminate all forms of
confounding in observational studies, these offer information that is not
possible to obtain in experiments. Therefore the task for methodologists is to
try to come up with methods that allow information to be reliably extracted
from observational data. In the paper in question, we tried to reduce the
possible role for confounding in the following way.

.. figure:: https://royalsocietypublishing.org/cms/asset/f69bbae6-4e5e-4cf6-b5a7-a55827b4acf6/rspb20151180f03.jpg
   :figwidth: 240px
   :alt: Figure 3 from the paper
   :align: right
   :target: https://royalsocietypublishing.org/cms/asset/f69bbae6-4e5e-4cf6-b5a7-a55827b4acf6/rspb20151180f03.jpg

   Figure 3 from the paper. D and N in the paper are equivalent to 1 and 0 in
   the discussion here respectively.

Suppose we have a Markov chain :raw-html:`\(\mathbf{X}_t = (X^i_t)\)`, where
:raw-html:`\(X^i_t=1\)` if individual :raw-html:`\(i\in\{1,2,\ldots,N\}\)` is
ill at time :raw-html:`\(t\)` and :raw-html:`\(X^i_t=0\)` otherwise. If there
is no social influence, then a standard modelling approach is to let
:raw-html:`\[\mathrm{Pr}(X^i_t=1) = f(\boldsymbol{\theta}_i) \mathrm{ ,}\]`
where :raw-html:`\(\boldsymbol{\theta}_i\)` is a vector of individual-level
properties / behaviours for individual :raw-html:`\(i\)`, and the function
:raw-html:`\(f\)` is usually a logit transform on
:raw-html:`\(\boldsymbol{\beta}\cdot\boldsymbol{\theta}_i\)`. Here there is
a lot of room for confounding if different elements of the vectors in
:raw-html:`\(\{\boldsymbol{\theta}_i\}_{i=1}^{N}\)` are correlated with each
other.

Now add the social network - a matrix with elements :raw-html:`\[G_{i,j} =
\begin{cases} 1 & \text{ if } j \text{ is } i \text{'s friend,} \\ 0 & \text{
otherwise.}\end{cases}\]` Clustering in such a network is a tendency for
friends to be in the same disease state - :raw-html:`\(\mathrm{Pr}(X^i_t = X^j_t \vert
G_{i,j}=1) \gt \mathrm{Pr}(X^i_t = X^j_t \vert G_{i,j}=0)\)`. The issue of confounding
then becomes whether the links :raw-html:`\(\{G_{i,j}\}_{i,j=1}^{N}\)` (usually
thought of as Bernoulli random variables like the disease states) are
correlated with the :raw-html:`\(\{\boldsymbol{\theta}_i\}_{i=1}^{N}\)`, or
whether there is evidence for "spreading" of the disease as in Figure 3 of the
paper.

Our way of answering this rests on the bit of stochastic process theory that
says that distinct Markov chains can share the same stationary distribution,
meaning that observations from this distribution alone cannot distinguish them,
but may have different transition probabilities. A direct observation of
*transitions* between disease states therefore allows us to consider determine
model probabilities like :raw-html:`\(\mathrm{Pr}(X^i_{t+1} = 1 \vert
\mathbf{X}_t,\mathbf{G})\)`, and thereby distinguish between spreading over a
network, and correlation of other properties / behaviours. The full details are
given in the paper and supplement, but the basic idea that a lot of confounding
is related to equivalent stationarity of stochastic processes behind the
hypotheses to be considered, and could be mitigated by fitting to temporal
observations (or other features that do distinguish those processes) is, I
believe, a relatively general one.

