========================
Documentation guidelines
========================

.. _docs.ckan.org: http://docs.ckan.org

This section gives some guidelines to help us to write consistent and good
quality documentation for CKAN.

Documentation isn't source code, and documentation standards don't need to be
followed as rigidly as coding standards do. In the end, some documentation is
better than no documentation, it can always be improved later. So the
guidelines below are soft rules.

Having said that, we suggest just one hard rule: **no new feature (or change to
an existing feature) should be missing from the docs** (but see `todo`_).

.. seealso::

   Jacob Kaplon-Moss's `Writing Great Documentation <http://jacobian.org/writing/great-documentation/>`_
     A series of blog posts about writing technical docs, a lot of our
     guidelines were based on this.

.. contents::
   :local:

.. _getting-started:

------------------
1. Getting started
------------------

This section will walk you through downloading the source files for CKAN's
docs, editing them, and submitting your work to the CKAN project.

CKAN's documentation is created using `Sphinx <http://sphinx-doc.org/>`_,
which in turn uses `Docutils <http://docutils.sourceforge.net/>`_
(reStructuredText is part of Docutils). Some useful links to bookmark:

* `Sphinx's reStructuredText Primer <http://sphinx-doc.org/rest.html>`_
* `reStructuredText cheat sheet <http://docutils.sourceforge.net/docs/user/rst/cheatsheet.txt>`_
* `reStructuredText quick reference <http://docutils.sourceforge.net/docs/user/rst/quickref.html>`_
* `Sphinx Markup Constructs <http://sphinx-doc.org/markup/index.html>`_
  is a full list of the markup that Sphinx adds on top of Docutils.

The source files for the docs are in `the doc directory of the CKAN git repo <https://github.com/okfn/ckan/tree/master/doc>`_. 
The following sections will walk you through the process of making changes to
these source files, and submitting your work to the CKAN project.

a. Install CKAN into a virtualenv
=================================

Create a `Python virtual environment <http://pypi.python.org/pypi/virtualenv>`_
(virtualenv), activate it, install CKAN into the virtual environment, and
install the dependencies necessary for building CKAN. In this example we'll
create a virtualenv in a folder called ``pyenv``. Run these commands in a
terminal:

.. versionchanged:: 2.1
   In CKAN 2.0 and earlier the requirements file was called
   ``pip-requirements-docs.txt``, not ``dev-requirements.txt`` as below.

::

    virtualenv --no-site-packages pyenv
    . pyenv/bin/activate
    pip install -e 'git+https://github.com/okfn/ckan.git#egg=ckan'
    pip install -r pyenv/src/ckan/dev-requirements.txt


b. Fetch CKAN's git submodules
==============================

CKAN's custom Sphinx theme is a kept in a git *submodule*, so before you can
build the docs you have to run these commands in a terminal to download the
submodule::

    cd pyenv/src/ckan
    git submodule init
    git submodule update

You may occasionally have to run ``git submodule update`` again, when someone
updates the theme, but this doesn't happen often.


c. Build the docs
=================

You should now be able to build the CKAN documentation locally. Make sure your
virtual environment is activated, and then run this command::

    python setup.py build_sphinx

Now you can open the built HTML files in
``pyenv/src/ckan/build/sphinx/html``, e.g.::

    firefox pyenv/src/ckan/build/sphinx/html/index.html


d. Edit the reStructuredText files
==================================

To make changes to the documentation, use a text editor to edit the ``.rst``
files in ``pyenv/src/ckan/doc/``. Save your changes and then build the docs
again (``python setup.py build_sphinx``) and open the HTML files in a web
browser to preview your changes.

Once your docs are ready to submit to the CKAN project, follow the steps in
:ref:`making a pull request`.

.. _structure:

-------------------------
2. Structure and audience
-------------------------

:doc:`index` describes the overall structure of the docs, and the intended
audience for each part. This structure is intended to be clear, simple and
extendable.  If you're adding a new section to the docs, try to fit it into
this structure.

Within a particular page, for example a new page documenting a new feature, our
suggestion for what sections the page should have is:

#. **Overview**: a conceptual overview of or introduction to the feature.
   Explain what the feature provides, why someone might want to use it,
   and introduce any key concepts users need to understand.
   This is the **why** of the feature.

   If it's developer documentation (extension writing, theming, API, or
   core developer docs), maybe put an architecture guide here.

#. **Tutorials**: tutorials and examples for how to setup the feature,
   and how to use the feature. This is the **how**.

#. **Reference**: any reference docs such as config options or API functions.

#. **Troubleshooting**: common error messages and problems, FAQs, how to
   diagnose problems.


.. _style:

--------
3. Style
--------

.. 
    http://jacobian.org/writing/great-documentation/technical-style/

This section covers things like what tone to use, how to capitalize section
titles, etc.  Having a consistent style will make the docs nice and easy to
read and give them a complete, quality feel.


Use American spelling
=====================

Use American spellings everywhere: organization, authorization, realize,
customize, initialize, color, etc. There's a list here:
https://wiki.ubuntu.com/EnglishTranslation/WordSubstitution


Commonly used terms
===================

CKAN
  Should be written in ALL-CAPS.
email
  Use email not e-mail.
|postgres|, |sqlalchemy|, |nginx|, |python|, |sqlite|, |javascript|, etc.
  These should always be capitalized as shown above (including capital first
  letters for Python and Nginx even when they're not the first word in a
  sentence). ``doc/conf.py`` defines substitutions for each of these so you
  don't have to remember them, see :ref:`sphinx substitutions`.
Web site
  Two words, with Web always capitalized
frontend
  Not front-end
command line
  Two words, not commandline or command-line
  (this is because we want to be like `Neal Stephenson <http://www.cryptonomicon.com/beginning.html>`_)
CKAN config file or configuration file
  Not settings file, ini file, etc. Also, the **config file** contains **config
  options** such as ``ckan.site_id``, and each config option is **set** to a
  certain **setting** or **value** such as ``ckan.site_id = demo.ckan.org``.


Section titles
==============

Capitalization in section titles should follow the same rules as in normal
sentences: you capitalize the first word and any `proper nouns
<http://en.wikipedia.org/wiki/Proper_noun>`_.

This seems like the easiest way to do consistent capitalization in section
titles because it's a capitalization rule that we all know already (instead of
inventing a new one just for section titles).

Right:

* Installing CKAN from package
* Getting started
* Command line interface
* Writing extensions
* Making an API request
* You're done!
* Libraries available to extensions

Wrong:

* Installing CKAN from Package
* Getting Started
* Command Line Interface
* Writing Extensions
* Making an API Request
* You're Done!
* Libraries Available To Extensions

For lots of examples of this done right, see
`Django's table of contents <https://docs.djangoproject.com/en/1.5/contents/>`_.

In Sphinx, use the following section title styles::

    ===============
    Top-level title
    ===============

    ------------------
    Second-level title
    ------------------

    Third-level title
    =================

    Fourth-level title
    ------------------

If you need more than four levels of headings, you're probably doing something
wrong, but see:
http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html#sections


Be conversational
=================

Write in a friendly, conversational and personal tone:

* Use contractions like don't, doesn't, it's etc.

* Use "we", for example *"We'll publish a call for translations to the
  ckan-dev and ckan-discuss mailing lists, announcing that the new
  version is ready to be translated"* instead of *"A call for translations will
  be published"*.


* Refer to the reader personally as "you", as if you're giving verbal
  instructions to someone in the room: *"First, you'll need to do X. Then, when
  you've done Y, you can start working on Z"* (instead of stuff like
  *"First X must be done, and then Y must be done..."*).


Write clearly and concretely, not vaguely and abstractly
========================================================

`Politics and the English Language <http://www.orwell.ru/library/essays/politics/english/e_polit/>`_
has some good tips about this, including:

#. Never use a metaphor, simile, or other figure of speech which you are used
   to seeing in print.
#. Never use a long word where a short one will do.
#. If it's possible to cut out a word, always cut it out.
#. Never use the passive when you can be active.
#. Never use a foreign phrase, scientific word or jargon word if you can think
   of an everyday English equivalent.

This will make your meaning clearer and easier to understand, especially for
people whose first language isn't English.

Facilitate skimming
===================

Readers skim technical documentation trying to quickly find what's
important or what they need, so break walls of text up into small, visually
identifiable pieces:

* Use lots of `inline markup <http://sphinx-doc.org/rest.html#inline-markup>`_::

      *italics*
      **bold**
      ``code``

  For code samples or filenames with variable parts, uses Sphinx's
  `:samp: <http://sphinx-doc.org/markup/inline.html#role-samp>`_
  and `:file: <http://sphinx-doc.org/markup/inline.html#role-file>`_
  directives.

* Use `lists <http://sphinx-doc.org/rest.html#lists-and-quote-like-blocks>`_
  to break up text.

* Use ``.. note::`` and ``.. warning::``, see Sphinx's
  `paragraph-level markup <http://sphinx-doc.org/markup/para.html#paragraph-level-markup>`_.

  (|restructuredtext| actually supports lots more of these: ``attention``,
  ``error``, ``tip``, ``important``, etc. but most Sphinx themes only style
  ``note`` and ``warning``.)

* Break text into short paragraphs of 5-6 sentences each max.

* Use section and subsection headers to visualize the structure of a page.


.. _sphinx tips:

---------
4. Sphinx
---------

This section gives some useful tips about using Sphinx.


Don't introduce any new Sphinx warnings
=======================================

When you build the docs, Sphinx prints out warnings about any broken
cross-references, syntax errors, etc. We aim not to have any of these warnings,
so when adding to or editing the docs make sure your changes don't introduce
any new ones.

It's best to delete the ``build`` directory and completely rebuild the docs, to
check for any warnings::

    rm -rf build; python setup.py build_sphinx


Maximum line length
===================

As with Python code, try to limit all lines to a maximum of 79 characters.


Cross-references and links
==========================

Use ``:doc:`` to cross-reference to other files by filename::

    See :doc:`theming`

see `Cross-referencing documents <http://sphinx-doc.org/markup/inline.html#cross-referencing-documents>`_
for details.

Use ``:ref:`` to cross-reference to particular sections within the same or
another file. First you have to add a label before the section you want to
cross-reference to::

    .. _getting-started:

    ---------------
    Getting started
    ---------------

then from elsewhere cross-reference to the section like this::

    See :ref:`getting-started`.

see `Cross-referencing arbitrary locations <http://sphinx-doc.org/markup/inline.html#cross-referencing-arbitrary-locations>`_.

With both ``:doc:`` and ``:ref:`` if you want the link text to be different
from the title of the section you're referencing, do this::

    :doc:`the theming document <theming>`

    :ref:`the getting started section <getting-started>`

The syntax for linking to external URLs is slightly different from
cross-referencing, you have to add a trailing underscore::

    `Link text <http://example.com/>`_

or to define a URL once and then link to it in multiple places, do::

    This is `a link`_ and this is `a link`_ and this is
    `another link <a link>`_.

    .. _a link: http://example.com/

see `Hyperlinks <http://sphinx-doc.org/rest.html#hyperlinks>`_ for details.

Use ``:py:`` to reference other Python or JavaScript functions, modules,
classes, etc. See :ref:`Referencing other code objects`.


.. _sphinx substitutions:

Substitutions
=============

`Substitutions <http://sphinx-doc.org/rest.html#substitutions>`_ are a useful
way to define a value that's needed in many places (eg. a command, the location
of a file, etc.) in one place and then reuse it many times.

You define the value once like this::

    .. |production.ini| replace:: /etc/ckan/default/production.ini

and then reuse it like this::

   Now open your |production.ini| file.

``|production.ini|`` will be replaced with the full value
``/etc/ckan/default/production.ini``.

Substitutions can also be useful for achieving consistent spelling and
capitalization of names like |restructuredtext|, |postgres|, |nginx|, etc.

The ``rst_epilog`` setting in ``doc/conf.py`` contains a list of global
substitutions that can be used from any file.

Substitutions can't immediately follow certain characters (with no space
in-between) or the substitution won't work. If this is a problem, you can
insert an escaped space, the space won't show up in the generated output and
the substitution will work::

     pip install -e 'git+\ |git_url|'

Similarly, certain characters are not allowed to immediately follow a
substitution (without a space) or the substitution won't work. In this case you
can just escape the following characters, the escaped character will show up in
the output and the substitution will work::

     pip install -e 'git+\ |git_url|\#egg=ckan'

Also see :ref:`parsed-literals` below for using substitutions in code blocks.


.. _parsed-literals:

Parsed literals
===============

Normally things like links and substitutions don't work within a literal code
block. You can make them work by using a ``parsed-literal`` block, for
example::

    Copy your development.ini file to create a new production.ini file::

    .. parsed-literal::

       cp |development.ini| |production.ini|


autodoc
=======

.. _autodoc: http://sphinx-doc.org/ext/autodoc.html

We try to use `autodoc`_ to pull documentation from source code docstrings into
our Sphinx docs, wherever appropriate. This helps to avoid duplicating
documentation and also to keep the documentation closer to the code and
therefore more likely to be kept up to date.

Whenever you're writing reference documentation for modules, classes, functions
or methods, exceptions, attributes, etc. you should probably be using autodoc.
For example, we use autodoc for the :ref:`api-reference`, the
:ref:`plugin-reference`, etc.

For how to write docstrings, see :ref:`docstrings`.

.. _todo:

todo
====

No new feature (or change to an existing feature) should be missing from the
docs. It's best to document new features or changes as you implement them,
but if you really need to merge something without docs then at least add a
`todo directive <http://sphinx-doc.org/ext/todo.html>`_ to mark where docs
need to be added or updated (if it's a new feature, make a new page or section
just to contain the ``todo``)::


    =====================================
    CKAN's Builtin Social Network Feature
    =====================================

    .. todo::

       Add docs for CKAN's builtin social network for data hackers.




versionadded and versionchanged
===============================

Use Sphinx's ``versionadded`` and ``versionchanged`` directives to mark new or
changed features. For example::

    ================
    Tag vocabularies
    ================

    .. versionadded:: 1.7

    CKAN sites can have *tag vocabularies*, which are a way of grouping related
    tags together into custom fields.

    ...

With ``versionchanged`` you usually need to add a sentence explaining what
changed (you can also do this with ``versionadded`` if you want)::

    =============
    Authorization
    =============

    .. versionchanged:: 2.0
       Previous versions of CKAN used a different authorization system.

    CKAN's authorization system controls which users are allowed to carry out
    which...


deprecated
==========

Use Sphinx's `deprecated directive <http://sphinx-doc.org/markup/para.html#directive-deprecated>`_
to mark things as deprecated in the docs::

    .. deprecated:: 3.1
       Use :func:`spam` instead.


seealso
=======

Often one page of the docs is related to other pages of the docs or to external
pages. A `seealso <http://sphinx-doc.org/markup/para.html?highlight=seealso#directive-seealso>`_
block is a nice way to include a list of related links::

    .. seealso::

       :doc:`The DataStore extension <datastore>`
         A CKAN extension for storing data.

       CKAN's `demo site <http://demo.ckan.org/>`_
         A demo site running the latest CKAN beta version.
