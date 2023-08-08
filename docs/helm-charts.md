---
title: 'Helm Charts'
permalink: /helm-charts/
---
# Helm Charts

## Barravar Helm Charts

### Getting Started

This repository stores Helm charts customized by Barravar. Run the following commands to include it in your environment:

```console
helm repo add barravar {{ config.repo_url }}/helm-charts/
helm repo update
```

### Charts

{% for chart in helm_charts.entries %}
{% set title = chart |capitalize %}
{% set chart_list = helm_charts.entries[chart] | sort(attribute='created', reverse=true) %}
{% set latest_chart = chart_list[0] %}

<html><b>
{% if latest_chart.icon %}
<img src="{{ latest_chart.icon }}" style="height: 1.2em; vertical-align: text-top;" />
{% endif %}
{{ title }}
</b></html>

[Home]({{ latest_chart.home }}) \| [Source]({{ latest_chart.sources[0] }})

{{ latest_chart.description }}

```console
helm install {{ config.repo_name }}/{{ latest_chart.name }} --name {{ latest_chart.name }} --version {{ latest_chart.version }}
```

|  Chart Version  |  App Version  |     Date      |
|-----------------|---------------|---------------|
{% for item in chart_list -%}
{% if "-" not in item.version -%}
| [{{ item.name }}-{{ item.version }}]({{ item.urls[0] }}) | {{ item.appVersion }} | {{ item.created |truncate(19, true, '') |replace('T',' ')}} |
{% endif -%}
{% endfor -%}

{% endfor %}
