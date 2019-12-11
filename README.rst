=======
Wikioff
=======

Wikioff is an offline-first (local) wiki. It is primarily designed to serve as
my own state-of-the-art tool for computer graphics, hence some design choices
and the overall absence of features (which I like to call
simplicity-and-ergonomics-in-a-Vim-environment). It is quite inspired by the
static website generator hugo_.

It is not designed to support the primary purpose of huge collaborative wikis
- use for this the magnificient MediaWiki_ instead. Neither is it designed for
cool dynamic web diagrams and WebGL stuff. The goal is clearly to be able to
carry a personnal encyclopedia on a USB key (they still exist, that's right
!).

.. _hugo: https://gohugo.io
.. _MediaWiki: https://www.mediawiki.org/wiki/MediaWiki

It is made of content files (text), organised under a certain way, assets
(images, videos, etc...), tags files, and a metadata file. And that's all.
This can be version controlled easily, and the wikioff program generate a pile
of html pages out of this. It sounds cheap but I like it.

Usage
=====

1. Initialise a folder containing the wiki (``wikioff init``)
2. Create content files (with a specific hierarchy), assets...
3. Compile (``wikioff build``)

Content files
=============

Content files are simple text files in a given markup language. My personnal
choice on this one is reStructuredText (directives, images, simple, simple,
latex-friendly, simple, etc...). They are pandoc-converted to HTML, which will
be displayed with some appropriate CSS sheets.

**TODO** Talk about MathJax/WebGL/etc... support.

Organisation
------------

Only the first level of hierarchy is meaningful to wikioff. Apart from that
the whole structure is completely free (but a standard hierarchy is
recommanded, being it only for convention purpose). Content files should be
placed in the ``content/`` folder ("a surprise, for sure"), and assets should
go to ``assets/``. As an example ::

   .
   ├── assets
   │   └── images
   │       └── cornell-box-some-version.exr
   ├── content
   │   ├── manifold-exploration-path-tracing.rst
   │   ├── practical-path-guiding.rst
   │   └── volumetric-path-guiding.rst
   ├── path-guiding.tag
   └── mlt.tag

The assets directory can be configured to point outside of the repository,
with a relative path, e.g. ``../wiki-assets``. This can be necessary to avoid
overfilling the VCS. This requires:

1. A convention amongst users (the hard part)
2. Some other tool for sharing the files, like

   . `Git LFS`_
   . `Nextcloud`_
   . Anything else !

.. _`Git LFS`: https://git-lfs.github.com/
.. _`Nextcloud`: https://nextcloud.com/

Cross-references
----------------

Referencing clearly is the biggest advantage of wikis systems. In wikioff case
however everything is to be done by hand. This is the biggest drawback brought
by simplicity. Here are some details and tips to deal with it without tears.

First and foremost, HTML files will be named exactly the same as their
*<whatever the markup>* counterpart, and be placed in an identical folder
structure. Therefore to refer to a file ``distribution/probability-tree.rst``,
just refer to ``distribution/probability-tree.html``.

Accessing a subsection is done the usual way by appending
``#Id_of_the_section``. There might be some instabilities at the moment,
though. **FIXME**

Tags
====

Tag files are simple text files whose name are <tag name>.tag, and containing
a list of files being part of that tag. Lines starting with ``#`` are
understood as comments. For instance, publications on path guiding could be
listed in ::

   $ cat ../path-guiding.tag 
   # Path guiding related files, specified by a path relative to the root
   # directory. Examples :

   # Content files
   content/rendering/practical-path-guiding-muller-2017.rst

   # Assets
   assets/images/cornell-box-some-version.exr
   assets/images/path-guiding-folder

Research engine
===============

At some point I will try to generate a JS script enabling research
functionnalities. This can be very practical.

Languages support
=================

The default language is english. Files having an equivalent specified by
``<language>.<filename>`` will be made available in the other language as
well, e.g. ::

   .
   ├── cloud-computing.rst
   └── fr.cloud-computing.rst     # Infonuagique mon amour !

