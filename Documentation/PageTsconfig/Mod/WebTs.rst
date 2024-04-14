:orphan:
..  include:: /Includes.rst.txt

======
web_ts
======

..  versionchanged:: 12.0
    The :guilabel:`Web > Template` module has been replaced by the
    :guilabel:`Web > TypoScript` module. The only option in this namespace
    has been removed.

..  contents::
    :local:

..  index::
    web_info.menu.function
    Module menu; Template
..  _pageblindingfunctionmenuoptions-webts:

menu.function
=============

..  versionchanged:: 12.0
    The TSconfig option :tsconfig:`mod.web_ts.menu.function` has been removed
    with TYPO3 v12.0.

..  _pageblindingfunctionmenuoptions-webts-migration:

Migration from menu.function to options.hideModules
---------------------------------------------------

..  todo: link to options.hideModules once it is documented

..  code-block:: typoscript

    # before
    mod.web_ts.menu.function {
        TYPO3\CMS\Tstemplate\Controller\TemplateAnalyzerModuleFunctionController = 0
    }

    # after
    options.hideModules := addToList(web_typoscript_analyzer)

You can find the names of all TypoScript modules in
:file:`EXT:tstemplate/Configuration/Backend/Modules.php`.
