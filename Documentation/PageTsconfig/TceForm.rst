..  include:: /Includes.rst.txt
..  index::
    TCEFORM
    Records; editing options
..  _tceform:
..  _pagetceformconfobj:
..  _pagetceformflexformsheet:

=======
TCEFORM
=======

Allows detailed configuration of how editing forms are rendered for a page
tree branch and for individual tables if you like. You can enable and
disable options, blind options in selector boxes etc.

See the core API document section :ref:`FormEngine <t3coreapi:FormEngine>` for more
details on how records are rendered in the backend.

..  _tceform-properties:

Properties
==========

..  contents::
    :depth: 2
    :local:

..  index::
    Records; select items added
..  _tceform-addItems:

addItems
--------

..  confval:: addItems
    :name: tceform-addItems
    :type: localized string

    Change the list of items in :ref:`TCA type=select <t3tca:columns-select>` fields. Using this property,
    items can be added to the list. Note that the added elements might be removed if the selector represents
    records: If the select box is a relation to another table. In that case only existing records
    will be preserved.

    The subkey :typoscript:`icon` will allow to add your own icons to new values.

    ..  versionadded:: 12.1
         The subkey :typoscript:`group` can be used to insert a new element into an
         existing select item group by settings the value to the group identifier.
         The grouping is usually displayed in select fields with groups available.

    This property is available for various levels:

    table level, example:
        `TCEFORM.tt_content.header_layout.addItems`

    table and record type level, example:
        `TCEFORM.tt_content.header_layout.types.textpic.addItems`

    Flex form field level, example:
        `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.settings\.myfield.addItems`

        Where `sDEF` is the sheet name. For a description
        see the section :ref:`tceformApplyPropertiesFlexForm` on this page.

    ..  warning::
        Do not add page types this way (using `TCEFORM.pages.doktype.addItems`), instead the proper
        PHP API should be used to do this, see :ref:`Core APIs <t3coreapi:page-types>` for details.

..  _tceform-addItems-example:

Example: Add header layout option
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.tt_content.header_layout {
        # Add another header_layout option:
        addItems.1525215969 = Another header layout
        # Add another one with localized label, icon and group
        addItems.1525216023 = LLL:EXT:my_ext/Resources/Private/Language/locallang.xlf:header_layout
        addItems.1525216023.icon = EXT:my_ext/icon.png
        addItems.1525216023.group = special
    }

    Instead of adding files by path, icon identifiers should be used.

..  index::
    Records; labels changed
..  _tceform-altLabels:

altLabels
---------

..  confval:: altLabels
    :name: tceform-altLabels
    :type: localized string

    This property applies to :ref:`TCA type=select <t3tca:columns-select>`,
    :ref:`TCA type=check <t3tca:columns-check>` and :ref:`TCA type=radio <t3tca:columns-radio>`.

    This property allows you to enter alternative labels for the items in the list. For a single checkbox or radio
    button, use `default`, for multiple checkboxes and radiobuttons, use an integer for their position starting at 0.

    This property is available for various levels:

    table level:
        `TCEFORM.[tableName].[fieldName].altLabels`

    table and record type level:
        `TCEFORM.[tableName].[fieldName].types.[typeName].altLabels`

    Flex form field level, example:
        `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.settings\.myfield.altLabels`

        Where `sDEF` is the sheet name. For a description
        see the section :ref:`tceformApplyPropertiesFlexForm` on this page.

..  _tceform-altLabels-example:

Example: Override labels for document types
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.pages.doktype {
        # Set a different item label
        altLabels.1 = STANDARD Page Type
        altLabels.254 = Folder (for various elements)
        # Sets the default label for Recycler via "locallang":
        altLabels.255 = LLL:EXT:my_ext/Resources/Private/Language/locallang_tca.xlf:recycler
    }

..  figure:: /Images/ManualScreenshots/List/PagesDoktypeDifferentLabels.png
    :alt: The Page types with modified labels

    The Page types with modified labels

..  note::

    If the item has an **empty** value, the syntax is slightly different and an additional dot must be provided,
    like on this example:

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.tt_content.space_before_class.altLabels.. = foo

Note the *double dot* after `altLabels`.

..  _tceform-page_tsconfig_id:

PAGE_TSCONFIG_ID
----------------

..  confval:: PAGE_TSCONFIG_ID
    :name: tceform-PAGE_TSCONFIG_ID
    :type: integer

    This option allows to provide a value for dynamic SQL-WHERE parameters. The
    value is defined for a specific field of a table. For usage with flexform
    fields, the entire path to a sub-field must be provided.

..  note::

    This value can be used for the TCA property :ref:`foreign_table_where <t3tca:columns-select-properties-foreign-table-where>`
    and for the `addWhere` part of the :ref:`suggest wizard <pagetceformsuggest>`.

..  _tceform-page_tsconfig_id-example:

Example: Substitute a marker in a plugin FlexForm
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.myField.PAGE_TSCONFIG_ID = 22

In this example, the value will substitute the marker in a plugin FlexForm.

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.tx_myext_table.myfield.PAGE_TSCONFIG_ID = 22

This example might be used for a record in an extension. It refers to a
table called `tx_myext_table` and the field `myfield`. Here the marker will
be substituted by the value `22`.

..  _tceform-page_tsconfig_idlist:

PAGE_TSCONFIG_IDLIST
--------------------

..  confval:: PAGE_TSCONFIG_IDLIST
    :name: tceform-PAGE_TSCONFIG_IDLIST
    :type: list of integers

    See above.

..  _tceform-page_tsconfig_idlist-example:

Example: Substitute a list of IDs in a plugin FlexForm
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.myField.PAGE_TSCONFIG_IDLIST = 20,21,22

In this example, the value will substitute the marker in a plugin FlexForm.

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.tx_myext_table.myfield.PAGE_TSCONFIG_IDLIST = 20,21,22

This example might be used for a record in an extension. It refers to a
table called `tx_myext_table` and the field `myfield`. Here the marker will
be substituted by the list of integers.


..  _tceform-page_tsconfig_str:

PAGE_TSCONFIG_STR
-----------------

..  confval:: PAGE_TSCONFIG_STR
    :name: tceform-PAGE_TSCONFIG_STR
    :type: string

    See above.

..  _tceform-page_tsconfig_str-example:

Example: Substitute a string in a plugin FlexForm
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.myField.PAGE_TSCONFIG_STR = %hello%

In this example, the value will substitute the marker in a plugin FlexForm.

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.tx_myext_table.myfield.PAGE_TSCONFIG_STR = %hello%

This example might be used for a record in an extension. It refers to a
table called `tx_myext_table` and the field `myfield`. Here the marker will
be substituted by the given value.


..  index::
     Records; field configuration
..  _pageTsConfigTceFormColorPalette:

colorPalette
------------

..  versionadded:: 13.0

..  confval:: colorPalette
    :name: tceform-colorPalette
    :type: string

     Assign a :ref:`color palette <pagecolorpalettes>` to a specific field of a
     table, for all fields within a table or a global configuration affecting all
     color pickers within :ref:`FormEngine <t3coreapi:FormEngine>`. If no palette
     is defined, FormEngine falls back to all configured colors.

..  _pageTsConfigTceFormColorPalette-example:

Example: Assign a palette to a field
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  code-block:: typoscript
    :caption: EXT:my_sitepackage/Configuration/page.tsconfig

    # Assign a palette to a specific field
    TCEFORM.tx_myext_table.myfield.colorPalette = messages

    # Assign a palette to all color pickers used in a table
    TCEFORM.tx_myext_table.colorPalette = key_colors

    # Assign global palette
    TCEFORM.colorPalette = main


..  index::
     Records; field configuration
..  _pageTsConfigTceFormConfig:

config
------

..  confval:: config
    :name: tceform-config

     This setting allows to override TCA field configuration. This will influence configuration settings in
     :php:`$GLOBALS['TCA'][<tableName>]['columns'][<fieldName>]['config'][<key>]`, see
     :ref:`TCA reference <t3tca:columns-properties-config>` for details.

     Not all configuration options can be overridden, the properties are restricted and depend on the
     :ref:`field type <t3tca:columns-types>`. The array
     :code:`typo3/sysext/backend/Classes/Form/Utility/FormEngineUtility.php->$allowOverrideMatrix`
     within :ref:`FormEngine code <t3coreapi:FormEngine>` defines details:

     ..  code-block:: php

          'input' => ['size', 'max', 'readOnly'],
          'number' => ['size', 'readOnly'],
          'email' => ['size', 'readOnly'],
          'link' => ['size', 'readOnly'],
          'password' => ['size', 'readOnly'],
          'datetime' => ['size', 'readOnly'],
          'color' => ['size', 'readOnly'],
          'uuid' => ['size', 'enableCopyToClipboard'],
          'text' => ['cols', 'rows', 'wrap', 'max', 'readOnly'],
          'json' => ['cols', 'rows', 'readOnly'],
          'check' => ['cols', 'readOnly'],
          'select' => ['size', 'autoSizeMax', 'maxitems', 'minitems', 'readOnly', 'treeConfig', 'fileFolderConfig'],
          'category' => ['size', 'maxitems', 'minitems', 'readOnly', 'treeConfig'],
          'group' => ['size', 'autoSizeMax', 'maxitems', 'minitems', 'readOnly', 'elementBrowserEntryPoints'],
          'folder' => ['size', 'autoSizeMax', 'maxitems', 'minitems', 'readOnly', 'elementBrowserEntryPoints'],
          'inline' => ['appearance', 'behaviour', 'foreign_label', 'foreign_selector', 'foreign_unique', 'maxitems', 'minitems', 'size', 'autoSizeMax', 'symmetric_label', 'readOnly'],
          'file' => ['appearance', 'behaviour', 'maxitems', 'minitems', 'readOnly'],
          'imageManipulation' => ['ratios', 'cropVariants'],

     The reason that not all properties can be changed is that
     internally, the :ref:`DataHandler <t3coreapi:datahandler-basics>` performs database
     operations which require finalized :ref:`TCA <t3tca:start>` definitions
     that are accessed without this TSconfig getting interpreted. This mismatch
     would then lead to inconsistencies.

     An `input` or `text` TCA field can *not* enable the
     :ref:`RTE <typo3/cms-rte-ckeditor:introduction>` via the
     :typoscript:`config.enableRichtext` option due to similar reasons in respect
     to the DataHandler.

     Also, if for example the :typoscript:`max` definition of a field is made
     larger than the TCA definition of that field, you may need to to change
     the file :file:`ext_tables.sql` (see :ref:`t3coreapi:ext_tables-sql`)
     to adjust column definitions, especially when using the
     :ref:`Auto-generated structure <t3coreapi:auto-generated-db-structure>`.

     The property :typoscript:`config` is available for these levels:

     table level, example:
          :typoscript:`TCEFORM.tt_content.header.config.max`

     table and record type level, example:
          :typoscript:`TCEFORM.tt_content.header.types.textpic.config.max`

     Flex form field level, example:
          No current TYPO3 version allows to override the configuration of
          Flex form fields, even though this was previously documented here.
          This may change in future versions.

     ..  todo: Removed, because this is broken in every known TYPO3 version.
     ..  todo: Maybe re-enable this, if it gets fixed in a future release
          :typoscript:`TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.myInputField.config.max`

          Where :typoscript:`sDEF` is the sheet name and :typoscript:`myext_pi1` the name
          of the plugin.

..  index::
    Records; tree configuration
..  _pageTsConfigTceFormConfigTreeConfig:

config.treeConfig
-----------------

..  confval:: config.treeConfig
    :name: tceform-config-treeConfig
    :type: int

    The `treeConfig` sub properties of :ref:`TCEFORM.config <pageTsConfigTceFormConfig>` are dedicated to the TCA config type
    `select` with :ref:`renderType=selectTree <t3tca:columns-select-rendertype-selectTree>`. A couple of
    :ref:`treeConfig <t3tca:columns-select-properties-treeconfig>` properties can be overriden on page TSconfig level, see their detailed description
    in the :ref:`TCA reference <t3tca:columns-select-properties-treeconfig>`:

    ..  code-block:: typoscript
        :caption: EXT:site_package/Configuration/page.tsconfig

        config.treeConfig.startingPoints = 1,42
        config.treeConfig.appearance.expandAll = 1
        config.treeConfig.appearance.maxLevels = 2
        config.treeConfig.appearance.nonSelectableLevels = 1

    This property is available for various levels:

    table level, example:
        `TCEFORM.tt_content.myField.config.treeConfig.startingPoints`

    table and record type level, example:
        `TCEFORM.tt_content.header.types.config.treeConfig.startingPoints`

    Flex form field level, example:
        No current TYPO3 version allows to override the configuration of
        Flex form fields, even though this was previously documented here.
        This may change in future versions.

    ..  todo: Removed, because this is broken in every known TYPO3 version.
    ..  todo: Maybe re-enable this, if it gets fixed in a future release
        `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.settings\.myfield.config.treeConfig.startingPoints`

        Where `sDEF` is the sheet name and :typoscript:`myext_pi1` the name
        of the plugin. For a description
        see the section :ref:`tceformApplyPropertiesFlexForm` on this page.


..  index::
    Records; field description
..  _tceform-description:

description
-----------

..  include:: /Images/AutomaticScreenshots/Input1.rst.txt

..  confval:: description
    :name: tceform-description
    :type: string

    This property sets or overrides the TCA property
    :ref:`TCA description <t3tca:columns-properties-description>`, which allows to
    define a description for a TCA field, next to its label.

    ..  code-block:: typoscript
        :caption: EXT:site_package/Configuration/page.tsconfig

        TCEFORM.tt_content.header.description = override description

    As already known from other properties, this can also be configured for a
    specific language.

    ..  code-block:: typoscript
        :caption: EXT:site_package/Configuration/page.tsconfig

        TCEFORM.tt_content.header.description.de = override description for DE

    The option can be used on a per record type basis, too.

    ..  code-block:: typoscript
        :caption: EXT:site_package/Configuration/page.tsconfig

        TCEFORM.tt_content.header.types.textpic.description = override description for textpic

    Also referencing language labels is supported.

    ..  code-block:: typoscript
        :caption: EXT:site_package/Configuration/page.tsconfig

        TCEFORM.tt_content.header.description = LLL:EXT:my_ext/Resources/Private/Language/locallang.xlf:override_description

..  index::
    Records; field disabled
..  _tceform-disabled:

disabled
--------

..  confval:: disabled
    :name: tceform-disabled
    :type: boolean

    If set, the field is not displayed in the backend form of the record.
    However, the field can still be set by other means. For example if
    this property is set:
    :typoscript:`TCEFORM.tt_content.colPos.disabled = 1` the :guilabel:`Column` field
    will not be displayed in the content elements form. The
    content element can still be moved to another column which internally also
    sets the field :sql:`colPos`. Fields with the TSconfig property
    :tsconfig:`TCEFORM.<table>.<field>.disable` therefore show the same
    behaviour as fields of the TCA type :ref:`passthrough <t3tca:columns-passthrough>`.

    table level, example:
        `TCEFORM.tt_content.header.disabled`

    table and record type level, example:
        `TCEFORM.tt_content.header.types.textpic.disabled`

    Flex form sheet level. If set, the entire tab is not rendered, example:
        `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.disabled`

        Where `sDEF` is the sheet name. For a description
        see the section :ref:`tceformApplyPropertiesFlexForm` on this page.

    Flex form field level, example:
        `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.settings\.myfield.disabled`

        Where `sDEF` is the sheet name. For a description
        see the section :ref:`tceformApplyPropertiesFlexForm` on this page.

..  _tceform-disabled-example:

Example: Disable editing of the page title
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.pages.title {
        # The title field of the pages table is not editable
        disabled = 1
    }

..  index::
    Records; select items  disable "INVALID VALUE"
..  _pageFormEngineDisableNoMatchingElement:

disableNoMatchingValueElement
-----------------------------

..  confval:: disableNoMatchingValueElement
    :name: tceform-disableNoMatchingValueElement
    :type: boolean

    This property applies only to items in :ref:`TCA type=select <t3tca:columns-select>` fields.
    If a selector box value is not available among the options in the box, the default behavior
    of TYPO3 is to preserve the value and to show a label which warns about this special state:

    ..  figure:: /Images/ManualScreenshots/List/SelectInvalidValue.png
        :alt: A missing selector box value is indicated by a warning message

        A missing selector box value is indicated by a warning message

    If disableNoMatchingValueElement is set, the element "INVALID VALUE" will not be added to the list.

    This property is available for various levels:

    table level, example:
        `TCEFORM.tt_content.header_layout.disableNoMatchingValueElement`

    table and record type level, example:
        `TCEFORM.tt_content.header_layout.types.textpic.disableNoMatchingValueElement`

    Flex form field level, example:
        `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.settings\.myfield.disableNoMatchingValueElement`

        Where `sDEF` is the sheet name. For a description
        see the section :ref:`tceformApplyPropertiesFlexForm` on this page.

..  _pageFormEngineDisableNoMatchingElement-example:

Example: Disable "INVALID VALUE ..." label
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.pages.doktype {
        # "INVALID VALUE ..." label will never show up
        disableNoMatchingValueElement = 1
    }

Now the selector box will default to the first element in the selector box:

..  figure:: /Images/ManualScreenshots/List/SelectNoInvalidValue.png
    :alt: Instead of show a warning message the system choose the first element in the selector box

    Instead of show a warning message the system choose the first element in the selector box


..  index::
    Records; fileFolderConfig
..  _fileFolderConfig:

fileFolderConfig
----------------

..  confval:: fileFolderConfig
    :name: tceform-fileFolderConfig
    :type: array

    The special :ref:`fileFolder configuration options
    <t3tca:columns-select-properties-fileFolderConfig>`
    for TCA columns of type :ref:`TCA type=select <t3tca:columns-select>` can
    be used to fill a select field with files (images / icons) from a defined
    folder.

    The `fileFolderConfig` TCA configuration can be overridden with page
    TSconfig, allowing administrators to use different folders or different file
    extensions, per site.

    The same sub properties as in the `fileFolderConfig` TCA configuration are
    available:

    ..  code-block:: typoscript
        :caption: EXT:site_package/Configuration/page.tsconfig

        fileFolderConfig {
            folder = 'EXT:styleguide/Resources/Public/Icons'
            allowedExtensions = 'svg'
            depth = 1
        }

    This property is available for various levels:

    table level:
        `TCEFORM.[tableName].[fieldName].fileFolderConfig.folder`

    table and record type level:
        `TCEFORM.[tableName].[fieldName].types.[typeName].fileFolderConfig.folder`

    Flex form field level, example:
        `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.settings\.myfield.fileFolderConfig.folder`

        Where `sDEF` is the sheet name. For a description
        see the section :ref:`tceformApplyPropertiesFlexForm` on this page.

..  index::
    Records; select items user function
..  _itemsProcFunc:

itemsProcFunc
-------------

..  confval:: itemsProcFunc
    :name: tceform-itemsProcFunc
    :type: custom

    This property applies only to items in :ref:`TCA type=select <t3tca:columns-select>` fields. The properties of
    this key is passed on to the :ref:`itemsProcFunc <t3tca:columns-select-properties-itemsprocfunc>` in the
    parameter array by the key "TSconfig".

    This property is available for various levels:

    table level:
        `TCEFORM.[tableName].[fieldName].itemsProcFunc`

    table and record type level:
        `TCEFORM.[tableName].[fieldName].types.[typeName].itemsProcFunc`

    Flex form field level, example:
        `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.settings\.myfield.itemsProcFunc`

        Where `sDEF` is the sheet name. For a description
        see the section :ref:`tceformApplyPropertiesFlexForm` on this page.

..  index::
    Records; select items remove
..  _tceform-keepItems:

keepItems
---------

..  confval:: keepItems
    :name: tceform-keepItems
    :type: list of values

    Change the list of items in :ref:`TCA type=select <t3tca:columns-select>` fields. Using this property,
    all items except those defined here are removed.

    This property is available for various levels:

    table level, example:
        `TCEFORM.tt_content.header_layout.keepItems`

    table and record type level, example:
        `TCEFORM.tt_content.header_layout.types.textpic.keepItems`

    Flex form field level, example:
        `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.settings\.myfield.keepItems`

        Where `sDEF` is the sheet name. For a description
        see the section :ref:`tceformApplyPropertiesFlexForm` on this page.

..  _tceform-keepItems-example:

Example: Show only standard and spacer pages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.pages.doktype {
        # Show only standard and "Spacer" page types
        keepItems = 1, 199
    }

..  index::
    Records; Field label

..  _tceform_label:

label
-----

..  confval:: label
    :name: tceform-label
    :type: localized string

    This allows you to enter alternative labels for any field. The value can be a `LLL:` reference
    to a localization file, the system will then look up the selected backend user language and tries
    to fetch the localized string if available. However, it is also possible to override these by
    appending the language key and hard setting a value, for example `label.de = Neuer Feldname`.

    This property is available for various levels:

    table level, example:
        `TCEFORM.[tableName].[fieldName].label`

    table and record type level, example:
        `TCEFORM.[tableName].[fieldName].types.[typeName].label`

    Flex form field level, example:
        `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.settings\.myfield.label`

        Where `sDEF` is the sheet name. For a description
        see the section :ref:`tceformApplyPropertiesFlexForm` on this page.

..  _tceform_label-example:

Example: Override the label of a field
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.pages.title {
        label = LLL:EXT:my_ext/Resources/Private/Language/locallang.xlf:table.column
        label.default = New Label
        label.de = Neuer Feldname
    }


..  index::
    Records; label for no matching value
..  _tceform-noMatchingValue_label:

noMatchingValue_label
---------------------

..  confval:: noMatchingValue_label
    :name: tceform-noMatchingValue_label
    :type: localized string

    This property applies only to items in :ref:`TCA type=select <t3tca:columns-select>` fields, it allows defining
    a different label of the :ref:`noMatchingValue <pageFormEngineDisableNoMatchingElement>` element.

    It is possible to use the placeholder `%s` to insert the value. If the property is set to empty,
    the label will be blank.

    This property is available for various levels:

    table level, example:
        `TCEFORM.tt_content.header_layout.noMatchingValue_label`

    table and record type level, example:
        `TCEFORM.tt_content.header_layout.types.textpic.noMatchingValue_label`

    Flex form field level, example:
        `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.settings\.myfield.noMatchingValue_label`

        Where `sDEF` is the sheet name. For a description
        see the section :ref:`tceformApplyPropertiesFlexForm` on this page.

..  _tceform-noMatchingValue_label-example:

Example: Replace "INVALID VALUE ..." label with another string
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.pages.doktype {
        # Different "INVALID VALUE ..." label:
        noMatchingValue_label = VALUE "%s" was not available!
    }

..  figure:: /Images/ManualScreenshots/List/SelectInvalidValueDifferentLabel.png
    :alt:  An invalid selector box value is indicated by a warning message

    An invalid selector box value is indicated by a warning message


..  index::
    Records; select items remove
..  _tceform-removeItems:

removeItems
-----------

..  confval:: removeItems
    :name: tceform-removeItems
    :type: list of values

    Change the list of items in :ref:`TCA type=select <t3tca:columns-select>` fields. Using this property,
    single items can be removed, leaving all others.

    This property is available for various levels:

    table level, example:
        `TCEFORM.tt_content.header_layout.removeItems`

    table and record type level, example:
        `TCEFORM.tt_content.header_layout.types.textpic.removeItems`

    Flex form field level, example:
        `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.settings\.myfield.removeItems`

        Where `sDEF` is the sheet name. For a description
        see the section :ref:`tceformApplyPropertiesFlexForm` on this page.

..  _tceform-removeItems-example:

Example: Remove "Recycler" and "Spacer" page types
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.pages.doktype {
        # Remove "Recycler" and "Spacer" page types
        removeItems = 199, 255
    }

..  index::
    FlexForm; Sheet description
..  _tceform-sheetDescription:

sheetDescription
----------------

..  confval:: sheetDescription
    :name: tceform-sheetDescription
    :type: localized string

    Specifies a description for the sheet shown in the FlexForm.

    This property is only available on flex form sheet level, for example
    `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.sheetDescription`.

    Where `sDEF` is the sheet name. For a description
    see the section :ref:`tceformApplyPropertiesFlexForm` on this page.


..  index::
    FlexForm; Sheet short description
..  _tceform-sheetShortDescr:

sheetShortDescr
---------------

..  confval:: sheetShortDescr
    :name: tceform-sheetShortDescr
    :type: localized string

    Specifies a short description of the sheet used as link title in the tab-menu.

    This property is only available on flex form sheet level, example:
    `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.sheetShortDescription`.

    Where `sDEF` is the sheet name. For a description
    see the section :ref:`tceformApplyPropertiesFlexForm` on this page.

..  index::
    FlexForm; Sheet title
..  _tceform-sheetTitle:

sheetTitle
----------

..  confval:: sheetTitle
    :name: tceform-sheetTitle
    :type: localized string

    Set the title of the sheet / tab in a FlexForm configuration.

    This property is only available on flex form sheet level, example:
    `TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF.sheetTitle`.

    Where `sDEF` is the sheet name. For a description
    see the section :ref:`tceformApplyPropertiesFlexForm` on this page.

..  _tceform-sheetTitle-example:

Example: Rename the first tab of the FlexForm plugin
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  code-block:: typoscript
    :caption: EXT:site_package/Configuration/page.tsconfig

    TCEFORM.tt_content.pi_flexform.myext_pi1.sDEF {
        # Rename the first tab of the FlexForm plug-in configuration
        sheetTitle = LLL:my_ext/Resource/Private/Language/locallang.xlf:tt_content.pi_flexform.myext_pi1.sDEF
    }

suggest
-------

Configuration of the suggest wizard that is available and often enabled
for :ref:`TCA type=group <t3tca:columns-group>` fields. See
:ref:`property suggest <pagetceformsuggest>` for more information.

..  toctree::
    :glob:
    :hidden:

    TceForm/*
