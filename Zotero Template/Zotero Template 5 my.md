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
{% if annotations.length > 0 %}*Imported on {{importDate | format("YYYY-MM-DD HH:mm")}}*{% endif %}
{% for annotation in annotations %}{% if annotation.imageRelativePath %}> [!cite]+ Image [(p. {{annotation.pageLabel}})](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.pageLabel}}&annotation={{annotation.id}})
> ![[{{annotation.imageRelativePath}}]]
> {{annotation.comment}}{% endif %}
{% if annotation.annotatedText %}> [!cite]+ Text [(p.{{annotation.page}})](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}}))
> *" {{annotation.annotatedText}} "*
> {{annotation.comment}}{% endif %}
{% if annotation.comment and not annotation.annotatedText and not annotation.imageRelativePath %}- [(p. {{annotation.pageLabel}})](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.pageLabel}}&annotation={{annotation.id}}) {{annotation.comment}}{% endif %}{% endfor %}