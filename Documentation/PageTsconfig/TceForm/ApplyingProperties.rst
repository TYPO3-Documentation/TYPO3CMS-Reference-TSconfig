
..  _tceform-apply-properties:

===================
Applying properties
===================

The properties listed below apply to various contexts which are explained per
property. The full property path thus depends on the property and where it should
apply. In general, a more specific property path overrides a less specific one:

Some properties apply to single fields, those can be usually set per table or
per table and record type. This leads to the property paths
`TCEFORM.[tableName].[fieldName].[propertyName]` to configure the field for all types
and `TCEFORM.[tableName].[fieldName].types.[typeName]` to configure a field for a specific
type, see the :ref:`TCA type section <t3tca:types>` for details on types.

While all that property path munging looks messy at first, it should become more
clear when reading through the single properties below and looking at the examples.

..  youtube:: B3IQq7pIJ_o
..  include:: /Includes.rst.txt
..  _tceformApplyPropertiesFlexForm:

Applying properties to FlexForm fields
======================================

Other properties also apply to :ref:`FlexForm <t3coreapi:flexforms>` fields, in this case the full property
path including the data structure key has to be set:

..  code-block:: typoscript

     # TCEFORM.[tableName].[fieldName].[dataStructureKey].[flexSheet].[flexFieldName with escaped dots].[propertyName]
     TCEFORM.tt_content.pi_flexform.sfregister_create.sDEF.settings\.fields\.selected.addItems.ZZZ = ZZZ

The sheet name (sDEF) must be given only if the FlexForm has a sheet.

The `[dataStructureKey]` represents the key of a FlexForm in
:php:`$GLOBALS['TCA'][<tableName>]['columns'][<field>]['config']['ds']`. This key will be split into up to
two parts. By default the first part will be used as identifier of the FlexForm in TSconfig. The second part
will override the identifier if it is not empty, `list` or `*`. For example the identifier of the key
`myext_pi1,list` will be `myext_pi1` and of the key `*,my_CType` it will be `my_CType`. See section
:ref:`Pointing to a data structure <t3tca:columns-flex-ds-pointer>` of the TCA reference for details.

The flexFieldName is the name of the property in the FlexForm. If it contains
dots ('.'), these must be escaped with backslash.

Some properties apply to whole FlexForm sheets, their property path is
`TCEFORM.[tableName].[fieldName].[dataStructureKey].[flexSheet].[propertyName]`.
