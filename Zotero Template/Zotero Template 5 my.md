---
year:
  "{ date | format (\"YYYY\") }": 
tags: []
authors:
  "{ authors }":
---
# [{{title}}]({{desktopURI}})
# Key Points

# Notes
{% if annotations.length > 0 %}
*Imported on {{importDate | format("YYYY-MM-DD HH:mm")}}*
{%- endif %}

{% for annotation in annotations -%}
{%- if annotation.annotatedText -%}
>[!Highlight]+ 
>*« {{annotation.annotatedText}} »*([{{annotation.page}}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}}))
{% endif %}
{% if annotation.imageRelativePath %}
>[!Image]+ [(p. {{annotation.pageLabel}})](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.pageLabel}}&annotation={{annotation.id}})
>![[{{annotation.imageRelativePath}}]]{% endif %}
{% if annotation.comment %}
>[!Comment]+ [(p. {{annotation.pageLabel}})](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.pageLabel}}&annotation={{annotation.id}})
>{{annotation.comment}}{%- endif %}
{% endfor %}