.. include:: /Includes.rst.txt

.. _introduction:

Introduction
------------


.. _about:

About this document
^^^^^^^^^^^^^^^^^^^

TypoScript can be used to create templates for the TYPO3 frontend, but
also to configure the TYPO3 backend. In this case, it is called
"TSconfig". TSconfig is divided into configuration for pages ("Page
TSconfig") and configuration for users and groups ("User TSconfig").
Each variant is further detailed in its own chapter. TSconfig offers
vast possibilities of customizing the TYPO3 backend.

For details about the nature of TypoScript as a syntax, please read
the document :ref:`TypoScript Syntax and In-depth Study <t3tssyntax:start>`.

.. _whatsnew:

What's new
^^^^^^^^^^

This version of the TSconfig Reference was updated for TYPO3 CMS
version 6.2.

For TYPO3 6.2 the User TSconfig property options.clearCache.system has been added
which allows a non-admin user to clear frontend and page-related caches, plus some backend-related caches.
The new property mod.web_view.previewFrameWidths allows to emulate device widths.
When using the property field.options.pageTree.searchInAlias the search in the pagetree (filter) also filters on the URL alias field.
The new User TSconfig property excludeDoktypes allows to hide pages with certain doktypes in the page tree.
And last but not least the new Page TSconfig property options.backendLayout.exclude allows to control which backend layouts are usable.


For TYPO3 6.1 the Page TSconfig property noExportRecordsLinks has been added,
which allows to hide the buttons "Export" and "Download CSV file" in the list
module.

In TYPO3 6.0 already the property mod.SHARED.colPos_list had been removed.
Use Backend Layouts instead (see :ref:`Example for Backend Layouts <example_for_backend_layout>`).


.. _whatsnew-list:

Full list of changed properties
"""""""""""""""""""""""""""""""

You can find a list of changes for more recent TYPO3 versions in the
forge:

TYPO3 4.7: https://forge.typo3.org/versions/1428.

TYPO3 6.0: https://forge.typo3.org/versions/1624.

TYPO3 6.1: https://forge.typo3.org/versions/1961.

TYPO3 6.2: https://forge.typo3.org/versions/2011.


.. _credits:

Credits
^^^^^^^

This document was originally written by Kasper Skårhøj. It has since
then been maintained successively by Michael Stucki, François Suter,
Christopher Stelmaszyk and Christian Wöbbeking.


.. _feedback:

Feedback
^^^^^^^^

For general questions about the documentation get in touch by writing
to `documentation@typo3.org <mailto:documentation@typo3.org>`_ .

If you find a bug in this manual, please be so kind as to check the
online version on https://docs.typo3.org/typo3cms/TSconfigReference/.
From there you can hit the "Edit me on GitHub" button in the top right corner
and submit a pull request via GitHub. Alternatively you can just file an issue
using the bug tracker: https://github.com/TYPO3-Documentation/TYPO3CMS-Reference-TSconfig/issues.


Maintaining high quality documentation requires time and effort
and the TYPO3 Documentation Team always appreciates support.
If you want to support us, please join the documentation
mailing list/forum (https://forum.typo3.org/index.php/f/44/).


.. _versionnumbers:

Version Numbers
^^^^^^^^^^^^^^^

For new features TSconfig includes a note in which TYPO3 version the
feature was added. If such a note is missing, the feature is part of
TYPO3 since version 6.2 at least.
