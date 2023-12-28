## Jinja2 Setting Variables Within the Loop is Suprising

Jinja2 says having variables set with-in the loop would never supposed to work. See the issue here: https://github.com/pallets/jinja/issues/641 the entertaining part is this was opened as a regression, and contributors commented this was never supposed to work 😅 

> While the current behavior is incorrect, the old behavior is definitely incorrect as well. The `{% set %}` tag was never intended to override outer scopes. I'm surprised it did in some cases. Not sure what to do here.
(https://github.com/pallets/jinja/issues/641#issuecomment-271114019).


Anyway for my needs I discovered there is a feature called namespaces, so I used them...

`venue['status']` as pre-determined values that're ordered, and I was trying to create sections. So..
```jinja
{% set ns = namespace(status='Open') %}
{% set gap = False %}
{% for venue in venues %}
  {% if ns.status != venue['status'] -%}
    {% set gap = True -%}
  {% endif -%}
  {% set ns.status = venue['status'] -%}
  {% if gap %}
  ...
```

If you know any cleaner solution, I'm all ears.
