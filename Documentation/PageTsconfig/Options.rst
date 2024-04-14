..  include:: /Includes.rst.txt

..  _pageoptions:

=======
options
=======

Various options for the page affecting the Core at various points.

Properties
==========

..  contents::
    :depth: 2
    :local:

..  index::
    options.backendLayout
    Backend; Layout
..  _pagebackendlayout:

backendLayout.exclude
---------------------

..  confval:: backendLayout.exclude
    :name: options-backendLayout-exclude
    :type: list of identifiers / uids

    Exclude a list of backend layouts from being selectable when assigning a backend layout
    to a page record.

    Use the uid/identifier of the record in the default data provider.

..  _pagebackendlayout-example:

Example: Exclude two backend layouts from drop down selector
------------------------------------------------------------

..  figure:: /Images/ManualScreenshots/List/BackendLayoutID.png
    :alt: Two backend layout records shown in list module

    Before: Two backend layout records shown in list module

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    # Exclude two backend layouts from drop down selector
    options.backendLayout.exclude = 1,2

..  figure:: /Images/ManualScreenshots/List/BackendLayoutsExcluded.png
    :alt: Drop down without backend layouts

        Drop down without backend layouts
