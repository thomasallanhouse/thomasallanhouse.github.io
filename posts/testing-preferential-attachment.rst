.. title: Testing Preferential Attachment
.. slug: testing-preferential-attachment
.. date: 2015-10-13 10:44:53 UTC
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
.. has_math: true

.. role:: raw-html(raw)
   :format: html

I've recently had a `New paper out in EPJ Data Science
<http://www.epjdatascience.com/>`__ concerning preferential
attachment (the 'rich get richer' effect) in social networks.

This is a relatively controversial area, and the aim of the paper was to try to
be as systematic / objective as possible. The simplest way to explain our
results, suggested by one of two pleasingly constructive reviewers, is that we
estimate around 40% of social contacts arise due to the existence of existing
social contacts (e.g.  your friends introduce you to their friends) rather than
from direct social activity. If this figure had been much larger, it would have
created an epidemiological paradox - no infectious disease would be
controllable.

The main innovation was to use a general finite-state-space Markov chain for
the non-preferentially attached links, which generates a mechanistically
interpretable *phase-type* distribution as a way to capture other sources of
heterogeneity in contact numbers.

The journal's editor (quite a 'big name' with many followers) was
also nice enough to promote the work on social media:

:raw-html:`<blockquote class="twitter-tweet" data-cards="hidden" lang="en"><p lang="en" dir="ltr">Testing preferential attachment in social network formation&#10;<a href="http://t.co/2hXKf11dik">http://t.co/2hXKf11dik</a>&#10;<a href="https://twitter.com/EPJscience">@EPJscience</a> <a href="https://twitter.com/TAH_Sci">@TAH_Sci</a> <a href="http://t.co/X1hRXkAcFm">pic.twitter.com/X1hRXkAcFm</a></p>&mdash; alex vespignani (@alexvespi) <a href="https://twitter.com/alexvespi/status/653528967476080640">October 12, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>`

