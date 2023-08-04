---
title: Barravar Helm Charts
permalink: /helm-charts/
---

## {{ title }}

### Getting Started

This repository stores Helm charts customized by Barravar. Run the following commands to include it in your environment:

```bash
$ helm repo add {{ config.repo_name }} {{ config.repo_url }}{{ permalink }}
$ helm repo update
```

### Charts

{% for charts in entries %}
{% set chart_name = charts | capitalize %}
{% set all_charts = entries["%s" % (charts)] |sort(attribute='created', reverse = true) %}
{% set latest_chart = all_charts[0] %}

<html>
  {% if latest_chart.icon %}
  <img src="{{ latest_chart.icon }}" style="height: 1.2em; vertical-align: text-top;" />
  {% endif %}
  <b>{{ chart_name }}</b>
</html>

[Home]({{ latest_chart.home }}) \| [Source]({{ latest_chart.sources[0] }})

{{ latest_chart.description }}

```console
$ helm install {{ config.repo_name }}/{{ latest_chart.name }} --name <release-name> --version {{ latest_chart.version }}
```

| Chart Version    | App Version  | Date  |
| ---------------- | ------------ | ------|
{% for chart in all_charts -%}
{% if "-" not in chart.version -%}
| [{{ chart.name }}-{{ chart.version}}](.{{ permalink }}{{ chart.urls[0] }}) | {{ chart.appVersion }} | {{ chart.created }} |
{% endif -%}
{% endfor -%}

{% endfor %}