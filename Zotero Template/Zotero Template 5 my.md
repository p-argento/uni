---
year:
  "{ date | format (\"YYYY\") }": 
tags: []
authors:
  "{ authors }":
---

### {{title}}
{{pdfZoteroLink}}

### Notes
{% for annotation in annotations -%}{%- if annotation.annotatedText -%}{% if 'Red' in annotation.colorCategory %} 
##### {{annotation.annotatedText | escape }}{% else %}
{% if annotation.color %}{{annotation.colorCategory}} {% endif %}"{{annotation.annotatedText | escape }} ([{{annotation.page}}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}}))

{% endif %}{%- endif %} {% if annotation.imageRelativePath %} ![[{{annotation.imageRelativePath}}]]{% endif %}{% if annotation.comment %} 
>{{annotation.comment}}
{% endif %}{% endfor -%}