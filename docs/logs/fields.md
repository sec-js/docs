title: Fields
description: Sematext Logs App looks for special fields in logs, namely os.host, source, facility, severity, syslog-tag, tags, message, and @timestamp

Every log event shipped to Sematext Logs has its structure - it is divided into fields. Each field has a [type](/docs/logs/field-types/), for example [string](/docs/logs/field-types/#string), [date](/docs/logs/field-types/#date), or [integer](/docs/logs/field-types/#integerlong). It can even be an object holding structured data.  We do everything we can to ensure that log event field types are inferred correctly. However, you may also want to set field types explicitly. This can be done using the Field Editor accessible via a Logs App settings or using the [Templates and Mappings](/docs/logs/mappings-templates) APIs.

## Common Schema
Fields in log events are also referred to as Tags in Sematext. They are used for searching and filtering, but also for pivoting from Logs to other observability data in Sematext, such as performance metrics in [Monitoring](/docs/monitoring).  The [Common Schema for Logs](/docs/tags/common-schema/#logs-tags) lists special fields and their meaning.

## Fields Structure

The structure of your logs - their fields and types - is automatically created when you ship your logs to a Logs App in Sematext. There are two places where you can easily see your fields. The first one is the fields and filters section:

<img src="/docs/images/logs/logs_structure_fields_and_filters.png" alt="Logs Fields and Filters">

The second one is the [Field Editor](/docs/logs/fields/#field-editor):

<img src="/docs/images/logs/logs_structure_field_editor.png " alt="Logs Field Editor">

---
**Note:**
Fields shown in the fields and filters panel and fields shown in the Field Editor may differ. The Field Editor shows only fields that are included in your current [Logs App Mapping](/docs/logs/mappings-templates). On the other hand, fields and filters panel shows all fields that are still present in your Logs App. For example, if you used to ship logs with a `foo` field and then you deleted it, the Field Editor will not show it, while fields and filters panel will show it as long as there are log events that still contain it.
--- 

### Field Types

Each field has a field type. The following field types are supported:

 * [Integer/Long](/docs/logs/field-types/#integerlong) - numerical data without floating points
 * [Float/Double](/docs/logs/field-types/#floatdouble) - numerical, floating point data
 * [Boolean](/docs/logs/field-types/#boolean) - Boolean field
 * [Keyword/Not analyzed string](/docs/logs/field-types/#not-analyzed-string) - not analyzed text
 * [Text/Analyzed string](/docs/logs/field-types/#analyzed-string) - analyzed, full text searchable data
 * [Date](/docs/logs/field-types/#date) - date based data
 * [Geo](/docs/logs/field-types/#geo) - field type dedicated for spatial data
 * Object - nested structure holding structured data

### Modifying Fields

You can [add](/docs/logs/fields/#adding-fields), [remove](/docs/logs/fields/#removing-fields) or [edit](/docs/logs/fields/#editing-fields) existing fields by using the Field Editor accessible via a Logs App settings, by using the [Templates and Mappings](/docs/logs/mappings-templates) APIs or via "Edit Fields" in fields and filters:

<img src="/docs/images/logs/logs_field_and_fielters_edit_field.png " alt="Fields and Filters - Edit Fields">

Keep in mind that the modification is applied only to the data that is shipped after the adjustments, so you may need to re-index the data if you want the old data to be adjusted. 

## Field Editor

The Field Editor functionality allows adding, editing, and removing fields present in your logs [mappings](/docs/logs/mappings-templates).

<img src="/docs/images/logs/logs_field_editor_add.png " alt="Logs Field Editor - Adding Fields">

### Adding Fields

Field Editor lets you add a new field by providing its name and [type](/docs/logs/field-types/).   

### Editing Fields

Field Editor allows modifying a field type by changing its type. 

<img src="/docs/images/logs/logs_field_editor_edit.png " alt="Logs Field Editor - Editing Fields">

The changes done to a field are only applied to the logs shipped after the change was done. Once the changes are applied, the Field Editor will give you an option to re-index your old logs - [learn more](/docs/logs/fields/#re-indexing-data).

### Removing Fields

Field Editor lets you remove fields that are no longer present in your logs. You can mark multiple fields for deletion and apply the changes once everything is ready. 

<img src="/docs/images/logs/logs_field_editor_delete.png" alt="Logs Field Editor - Removing Fields">

Deleting a field removes it from the logs [mappings](/docs/logs/mappings-templates) and the logs already shipped to your Logs App will not be affected. If you continue to ship logs with such a field it will appear again. To fully delete the field from your Logs App first make sure the deleted field is no longer present in logs you ship to Sematext and then delete it with Field Editor.

Excluding a field makes the specific field inaccessible for search and visualizing operations. When a field is excluded, it is disabled in the logs [mappings](/docs/logs/mappings-templates) and effectively excluded from the index's search capabilities. This means that queries and aggregations will not consider or return results based on the excluded field.

### Re-indexing data

If you want your changes to apply to old data you can do that by re-indexing it. As you change fields, Field Editor will prompt you with the option to do that. If you start the indexing process all your old logs will be re-indexed in the background and the progress will be displayed on the Field Editor screen. 

Note that re-indexing counts towards your Logs App daily volume. Consider double-checking your usage data and temporarily increasing the [Daily Volume Limit](/docs/logs/faq/#are-logs-shipped-to-logs-app-ever-rejected) to avoiding hitting that limit during re-indexing.

<img src="/docs/images/logs/logs-field-editor-reindex.gif" alt="Logs Field Editor - Re-idexing">
