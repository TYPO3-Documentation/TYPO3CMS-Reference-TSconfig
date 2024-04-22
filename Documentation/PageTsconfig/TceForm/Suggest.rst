..  include:: /Includes.rst.txt
..  index::
    Records; Suggest wizard
    Suggest wizard
..  _pagetceformsuggest:

suggest
-------

Configuration of the suggest wizard that is available and often enabled
for :ref:`TCA type=group <t3tca:columns-group>` fields.

..  figure:: /Images/ManualScreenshots/List/TcaTypeGroupSuggest.png
    :alt: A configured suggest wizard

    A configured suggest wizard

The properties listed below are available on various levels. A more specific setting overrides
a less specific one:

Configuration of all suggest wizards in all tables for all target query tables:
    `TCEFORM.suggest.default`

Configuration of all suggest wizards in all tables looking up records from a specific target table:
    `TCEFORM.suggest.[queryTable]`

Configuration of one suggest wizard field in one table for all target query tables:
    `TCEFORM.[tableName].[fieldName].suggest.default`

Configuration of one suggest wizard field in one table for a specific target query table:
    `TCEFORM.[tableName].[fieldName].suggest.[queryTable]`

Configuration of one suggest wizard field in a flex form field of one table for all target query tables:
    `TCEFORM.[tableName].[fieldName].[dataStructureKey].[sheetName].[flexFieldName].suggest.default`

Configuration of one suggest wizard field in a flex form field of one table for a specific target query table:
    `TCEFORM.[tableName].[fieldName].[dataStructureKey].[sheetName].[flexFieldName].suggest.[queryTable]`

..  index::
    Suggest wizard; Search fields additional
..  _tceform-suggest-additionalSearchFields:

suggest.additionalSearchFields
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  confval:: suggest.additionalSearchFields
    :name: tceform-suggest-additionalSearchFields
    :type: string

    Comma-separated list of fields the suggest wizard should also search in. By default the wizard looks only in the
    fields listed in the :ref:`label <t3tca:ctrl-reference-label>` and :ref:`label_alt <t3tca:ctrl-reference-label-alt>`
    of TCA :ref:`ctrl properties <t3tca:ctrl-reference>`.


..  index::
    Suggest wizard;  Where statement
..  _tceform-suggest-addWhere:

suggest.addWhere
~~~~~~~~~~~~~~~~

..  confval:: suggest.addWhere
    :name: tceform-suggest-addWhere
    :type: string

    Additional WHERE clause (with AND at the beginning).

    Markers possible for replacement:

    *   ###THIS_UID###
    *   ###CURRENT_PID###
    *   :ref:`###PAGE_TSCONFIG_ID### <page_tsconfig_id>`
    *   :ref:`###PAGE_TSCONFIG_IDLIST### <page_tsconfig_idlist>`
    *   :ref:`###PAGE_TSCONFIG_STR### <page_tsconfig_str>`

..  _tceform-suggest-addWhere-example:

Example: limit storage_pid to the children of a certain page
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.pages.storage_pid.suggest.default {
        addWhere = AND pages.pid=###PAGE_TSCONFIG_ID###
    }

..  index::
    Suggest wizard; CSS class
..  _tceform-suggest-cssClass:

suggest.cssClass
~~~~~~~~~~~~~~~~

..  confval:: suggest.cssClass
    :name: tceform-suggest-cssClass
    :type: string

    Add a CSS class to every list item of the result list.

    ..  code-block:: typoscript
        :caption: EXT:site_package/Configuration/page.tsconfig

        TCEFORM.suggest.pages {
            # Configure all suggest wizards which list records from table "pages"
            # to add the CSS class "pages" to every list item of the result list.
            cssClass = pages
        }


..  index::
    Suggest wizard; hide
..  _tceform-suggest-hide:

suggest.hide
~~~~~~~~~~~~

..  confval:: suggest.hide
    :name: tceform-suggest-hide
    :type: boolean

    Hide the suggest field. Works only for single fields.

..  _tceform-suggest-hide-example:

Example: Hide the suggest field for the storage_pid
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.pages.storage_pid.suggest.default {
        hide = 1
    }


..  index::
    Suggest wizard; Characters max
..  _tceform-suggest-maxPathTitleLength:

suggest.maxPathTitleLength
~~~~~~~~~~~~~~~~~~~~~~~~~~

..  confval:: suggest.maxPathTitleLength
    :name: tceform-suggest-maxPathTitleLength
    :type: positive integer

    Maximum number of characters to display when a path element is too long.

..  _tceform-suggest-maxPathTitleLength-example:

Example: Limit the suggest field to 30 characters
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.suggest.default {
        maxPathTitleLength = 30
    }

..  index::
    Suggest wizard; Characters min
..  _tceform-suggest-minimumCharacters:

suggest.minimumCharacters
~~~~~~~~~~~~~~~~~~~~~~~~~

..  confval:: suggest.minimumCharacters
    :name: tceform-suggest-minimumCharacters
    :type: positive integer
    :Default: 2

    Minimum number of characters needed to start the search. Works only for single fields.

..  _tceform-suggest-minimumCharacters-example:

Example: Start the suggest search after 3 characters
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.pages.storage_pid.suggest.default {
        minimumCharacters = 3
    }


..  index::
    Suggest wizard; pid levels
..  _tceform-suggest-pidDepth:

suggest.pidDepth
~~~~~~~~~~~~~~~~

..  confval:: suggest.pidDepth
    :name: tceform-suggest-pidDepth
    :type: positive integer

    Expand pidList by this number of levels. Only has an effect, if pidList has a value.

..  _tceform-suggest-pidDepth-example:

Example: Set search depth for suggest field
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.suggest.default {
        pidList = 6,7
        pidDepth = 4
    }

..  index::
    Suggest wizard; pid list
..  _tceform-suggest-pidList:

suggest.pidList
~~~~~~~~~~~~~~~

..  confval:: suggest.pidList
    :name: tceform-suggest-pidList
    :type: list of values

    Limit the search to certain pages (and their subpages). When pidList is empty all pages will be included
    in the search as long as the backend user is allowed to see them.

..  _tceform-suggest-pidList-example:

Example: Limit suggest search to records on certain pages
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.suggest.default {
        # sets the pidList for a suggest fields in all tables
        pidList = 1,2,3,45
    }


..  index::
    Suggest wizard; receiver php class
..  _tceform-suggest-receiverClass:

suggest.receiverClass
~~~~~~~~~~~~~~~~~~~~~

..  confval:: suggest.receiverClass
    :name: tceform-suggest-receiverClass
    :type: Fully Qualified PHP class name
    :Default: :php:`\TYPO3\CMS\Backend\Form\Element\SuggestDefaultReceiver`

    PHP class alternative receiver class - the file that holds the class should be derived
    from :code:`\TYPO3\CMS\Backend\Form\Element\SuggestDefaultReceiver`.

..  index::
    Suggest wizard; rendering user function
..  _tceform-suggest-renderFunc:

suggest.renderFunc
~~~~~~~~~~~~~~~~~~

..  confval:: suggest.renderFunc
    :name: tceform-suggest-renderFunc
    :type: string

    User function to manipulate the displayed records in the result.

..  index::
    Suggest wizard; Where statement
..  _tceform-suggest-searchCondition:

suggest.searchCondition
~~~~~~~~~~~~~~~~~~~~~~~

..  confval:: suggest.searchCondition
    :name: tceform-suggest-searchCondition
    :type: string

    Additional WHERE clause (no AND needed to prepend).

..  _tceform-suggest-searchCondition-example:

Example: Only search on pages with doktype=1
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    ..  code-block:: typoscript
        :caption: EXT:site_package/Configuration/page.tsconfig

        TCEFORM.pages.storage_pid.suggest.default {
            # Configure the suggest wizard for the field "storage_pid" in table "pages"
            # to search only for pages with doktype=1
            searchCondition = doktype=1
        }

..  index::
    Suggest wizard; Search whole phrase
..  _tceform-suggest-searchWholePhrase:

suggest.searchWholePhrase
~~~~~~~~~~~~~~~~~~~~~~~~~

..  confval:: suggest.searchWholePhrase
    :name: tceform-suggest-searchWholePhrase
    :type: boolean
    :Default: 0

    Whether to do a `LIKE=%mystring%` (searchWholePhrase = 1) or a
    `LIKE=mystring%` (to do a real find as you type).

..  _tceform-suggest-searchWholePhrase-example:

Example: Search only for whole phrases
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.pages.storage_pid.suggest.default {
        # Configure the suggest wizard for the field "storage_pid" in table "pages" to search only for whole phrases
        searchWholePhrase = 1
    }
