=============================================
Guidelines for scientific software developers
=============================================

The purpose of this document is to provide developers of scientific
software, often scientists themselves, with guidelines on

- how to develop the software in a efficient way
- how to make it easily deployable by users across a variety of
  platforms
- how to reach a large audience and what benefits would it might
  provide

Why?
====

Academia and research are constant generators of a software, often as
a by-product of research projects.  Some popular commercial
(e.g. Mathworks Matlab) and free and open-source (e.g. Linux kernel)
software products grew up from academic environments.  Often
scientific software is developed by students or researchers neither
experienced in software development and deployment, nor having a
vision of making it available to public right from the beginning of
the development.  Reasons why, finally, software often becomes
available could be numerous -- from necessity to demonstrate the
method, to making it available to others for adoption of the method,
to seeking contributors and collaborators.  But how to make a software
project easy to deploy, use, and contribute?

There exist quite a few of other guidelines for software developers.
Some of them accent on development aspects, some on distribution and
deployment.  Covering all aspects becomes a tedious job requiring the
document to grow considerably.  In this little document we want to
touch upon a few aspects which are of special importance/use
in the domain of scientific software development.

References
----------

http://wiki.debian.org/GettingPackaged
 ... "what we do to your software, what we do for you and what you can
 do to help us." with references to other guides

http://us.pycon.org/media/2010/talkdata/PyCon2010/038/paper.html
 Cross-platform Application Development and Distribution

http://mail.python.org/pipermail/python-dev/2010-April/099729.html
 [Python-Dev] what to do if you don't want your module in Debian

.. contents::

.. accompany each section not only with a verbal description but a
.. concise list/references of possibly useful technologies and tools.
.. I wouldn't mind referencing Debian packages pages whenever possible

General guidelines
==================

.. Maybe later group into important and not so important


Have your code under control
----------------------------

Keep it under version control
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Version control systems became integral part of nearly any software
development.  You might like to research and choose the one which you
feel comfortable with the most.  If you are already experienced with
one of them but feel that you might be missing advantages of the other
existing systems, do not hesitate to research -- you might be missing
a lot.

Proper version control system would allow easy separation between what
is made to public and what should be kept private temporarily
(bleeding edge development, material waiting for accompanying
publication) or permanently (commercial interest).

Having sources under version control might help to determine specific
change which lead to a change in the results (`git bisect`_).

Comment your commits.  You might like to adhere to a prefix scheme
where some commits are marked as change in documentation, bug fixes,
new features (possibly extending API), remove feature, enhancements
(no API changes, but internal improvements, e.g. optimization), or
refactoring (no functional changes but could be API changes).
Following set of prefixes could be chosen then: DOC, BF, NF, RM, ENH,
RF correspondingly.  Prefixes allow for easy grouping for the summary
between the releases of what was accomplished, and make it easier to
grasp the evolution of the development.

Provide brief description for the commit message, do not leave it
uncommented.  If you cannot come up with a simple description, it is
questionable that you have anything valuable to commit.

If some command line construct (shell pipe of sed/awk/grep) was used
to produce the desired effect to be committed, include command line
with the extended commit message -- it might be found handy later on
or clarify what lead to a mistake.

Atomic commits within version control repository ease sharing of bug
fixes among both development and already released versions of
software (if merging of branches is not an option, look into commands
analogous to `git cherry-pick`_).

.. _git bisect: http://www.kernel.org/pub/software/scm/git/docs/git-bisect.html
.. _git cherry-pick: http://www.kernel.org/pub/software/scm/git/docs/git-cherry-pick.html


Version it
~~~~~~~~~~

- Do not be afraid to release
- `Release early, release often`_
- Whenever API exposed -- keep users and developers in mind, and do
  not forget about distributions (ABI).
- Be consistent with versioning, choose a common scheme

.. _`Release early, release often`: http://en.wikipedia.org/wiki/Release_early,_release_often

http://www.python.org/dev/peps/pep-0386/#the-new-versioning-algorithm
http://plan99.net/~mike/writing-shared-libraries.html


Document the sources
~~~~~~~~~~~~~~~~~~~~

Have unit-tests
~~~~~~~~~~~~~~~

Have a regression test suite
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For libraries -- think about API
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

http://people.redhat.com/drepper/goodpractice.pdf


Approach the users
------------------

Choose appropriate license and attribution
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Figure out copyright -- institution might be the one to hold it.

Try to use maximally possible permissible license, do not constrain
types of usage without real necessity.

It would be much harder later on to change the license to more
permissible; on contrary you can always create a derivative work
(effectively simply changing the license of the project if you are
core developer) to more restrictive compatible with original license
(i.e. go from any GPL-compatible license, such as MIT, BSD to GPL)

"Which license to choose?" [SMC+07]_ , keep in mind DFSG

.. [SMC+07] The Need for Open Source Software in Machine Learning
  Sören Sonnenburg, Mikio L. Braun, Cheng Soon Ong, Samy Bengio, Leon
  Bottou, Geoffrey Holmes, Yann LeCun, Klaus-Robert Müller, Fernando
  Pereira, Carl Edward Rasmussen, Gunnar Rätsch, Bernhard Schölkopf,
  Alexander Smola, Pascal Vincent, Jason Weston, Robert Williamson;
  Journal of Machine Learning Research 8(Oct):2443--2466, 2007.
  http://www.jmlr.org/papers/volume8/sonnenburg07a/sonnenburg07a.pdf

Please do not enforce, but rather advise, users to reference your
software or a corresponding scientific publication relevant to the
software.  For that, provide references to be used to cite your work.

It is conventional that copyright/license information usually
distributed along with the software in file COPYING.txt or LICENSE.txt

Document it
~~~~~~~~~~~

At minimum provide README.txt describing briefly what is the software
good for and how to use it, and INSTALL.txt for generic installation
steps at least on your own platform.

sphinx  wiki

Provide clean ways to contact you
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- email
- mailing list


Have a bugtracker
~~~~~~~~~~~~~~~~~



.. NEEDS MORE THOUGHT
.. Be an engineer
.. Do not over-engineer

Do not take unnecessary burden
------------------------------

Make use of build tools
~~~~~~~~~~~~~~~~~~~~~~~

If there is a shadow of thought that current build tools you know and
using are suboptimal, have a brief look at other tools already
available. Choosing the right build platform could save you countless
hours of unnecessary work:

make/cmake/scons


Get to know useful tools
~~~~~~~~~~~~~~~~~~~~~~~~

Keep an eye on the tools available for a specific aspect of
development.  Choose IDE which you feel convenient with, discover the
tools to ease debugging and troubleshooting (e.g. gdb, valgrind,
ccache, prof).


Do not fork 3rd-party software
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



Keep sources separate from binaries and data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Get it wrapped
--------------

- possibly make use of one of existing portals
- Expose VCS
- Provide transparent means to obtain ("register"/"login" isn't advisable)
- If possible, provide convenient distribution across multiple platforms


Announce
--------

- specialized mailing lists
- scientific software portals
- mention at scientific conferences


Debian-specific guidelines
==========================

Debian
------

What is Debian?
~~~~~~~~~~~~~~~

- free and open
- democratic / non-profit
- no control by any commercial company
- mature: almost 20 years old


Why Debian?
~~~~~~~~~~~

- driven by enthusiasts
- ideology behind stable/testing/unstable vs time-based marathon
- everything in Debian is supported by Debian:
  + upgrades
  + transition points
- pros of binary- vs source-based distribution
- a base for lots of derived distributions
- supports largest number of architectures
- provides already over 30,000 packages for you to make us of


What could Debian do for you?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- got electrolytes: brief overview of tool(kit)s present
  how that helps to escape from the "ivory tower development model"
- automagic binaries for numerous hardware architectures
- automagic delivery and mirroring throughout the world
- numerous tests for build- and upgrade-path stability
- bugtracking with adequate environment information


Get it into Debian
------------------

Blend it
~~~~~~~~

+ visibility
+ convenience


ITP and Package it or RFP
~~~~~~~~~~~~~~~~~~~~~~~~~


Benefit from Debian
-------------------

- enjoy a safety layer (DM) between you and users taking care about
  deployment on Debian systems
- popcon -- observe actual usage statistics/comparisons
- point your users to ready packaging within Debian
- check/troubleshoot Debian easily (virtual box or chroot via
  debootstrap)
- reproducibility (snapshot.debian.org)


Copyright and license
=====================

This document is copyright of its authors (see list below) and licensed under
the `Creative Commons Attribution-ShareAlike`_ license.

* Copyright © 2010 Yaroslav O. Halchenko
* Copyright © 2010 Michael Hanke

.. _Creative Commons Attribution-ShareAlike: http://creativecommons.org/licenses/by-sa/3.0/


Miscellaneous yet to be placed in
=================================

Some research projects do not wait for publication but make software
available and become extremely popular (even at times without adhering to
advises described above): e.g. LIBSVM


