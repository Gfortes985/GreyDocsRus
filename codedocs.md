---
layout: default
title: "Документация Greyscript"
permalink: /api
---
# Документация Greyscript 
{% assign encrypt = site.data.encryption %}
<ul>
{% for type in site.data.typelist %}
  <li><details><summary><b>{{ type }}</b></summary><ul>
  {% for func in site.data.functions[type] %}
    {% assign args = site.data.arguments[type][func] %}
    {% assign desc = site.data.descriptions[type][func] %}
    {% assign examples = site.data.examples[type][func] %}
    {% assign returns = site.data.returns[type][func] %}
    {% capture argdata %}
        {% for a in args %}
            {% if a.optional %}
?{{ a.name }}:{{ a.type }}, 
            {% else %}
{{ a.name }}:{{ a.type }}, 
            {% endif %}
        {% endfor %}
    {% endcapture %}
    {% capture retdata %}
        {% for r in returns %}
            {% if r.subType %}
{{ r.type }}[{{ r.subType }}] | 
            {% else %}
{{ r.type }} | 
            {% endif %}
        {% endfor %}
    {% endcapture %}
    {% assign argdata = argdata | strip_newlines | strip %}
    {% assign retdata = retdata | strip_newlines | strip %}
    {% assign x = argdata | size | minus:1 %}
    {% assign y = retdata | size | minus:2 %}
    {% assign z = argdata | size %}
    {% if z > 1 %}
        {% assign p1 = "(" %}
        {% assign p2 = ")" %}
    {% endif %}
    {% if type != "General" %}
<li><details><summary>{{ type }}.{{ func }}{{ p1 }}{{ argdata | slice: 0, x}}{{ p2 }} : {{ retdata | slice: 0, y}}</summary>
    {% endif %}
    {% if type == "General" %}
<li><details><summary>{{ func }}{{ p1 }}{{ argdata | slice: 0, x}}{{ p2 }} : {{ retdata | slice: 0, y}}</summary>
    {% endif %}
{% if encrypt contains func %}
> **Note:** Этот метод нельзя использовать c включенным шифрованием.
{% endif %}
{{ desc }}
{% for ex in examples %}
```lua
{{ ex }}
```
{% endfor %}
</details></li>
  {% endfor %}
  </ul></details></li>
{% endfor %}
</ul>

#### Данные API из расширения vscode Greyscript, доступные по адресу https://github.com/WyattSL/greyscript.
