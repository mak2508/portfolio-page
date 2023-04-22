---
layout: page
title: Tasrif
description: open-source wearable health data processing library
# img: assets/img/3.jpg
importance: 2
category: work
---

[Tasrif](https://tasrif.qcri.org) is an open source data processing package for health data primarily collected through wearables built by QCRI alongside the [SIHA](https://siha.qcri.org) project. The project was built as a convenience utility package to make it easier to process data collected by SIHA by health professionals of varying technical ability.

My [tasks](https://github.com/qcri/tasrif/pulls?q=is%3Apr+is%3Aclosed+author%3Amak2508) in this project mainly revolved around creating a YAML based specification for tasrif pipelines, allowing for preprocessing to be done with minimal coding.

You can read more about how tasrif pipelines work on the [docs](https://tasrif.qcri.org/pipelines.html). To give an example of how you would use YAML configs for the same example, it would look as follows:

`example.yaml`
{% raw %}
```yaml
modules:
  - tasrif.processing_pipeline: [sequence]
  - tasrif.processing_pipeline.pandas: [drop_na, concat, mean]

pipeline:
  $sequence:
    - $drop_na
    - $concat
    - $mean
```
{% endraw %}

\\
`examply.py`
{% raw %}
```python
import tasrif.yaml_parser as yaml_parser
import yaml 

df1 = pd.DataFrame({
    'Date':   ['05-06-2021', '06-06-2021', '07-06-2021', '08-06-2021'],
    'Steps':  [        4500,         None,         5690,         6780]
})

df2 = pd.DataFrame({
    'Date':   ['12-07-2021', '13-07-2021', '14-07-2021', '15-07-2021'],
    'Steps':  [        2100,         None,         None,         5400]
})

with open("example.yaml", "r") as stream:
    try:
        p = yaml_parser.from_yaml(stream)
    except yaml.YAMLError as exc:
        print(exc)

df = p.process()
```
{% endraw %}

\\
This is a small pipeline example, and perhaps the usefulness of the YAML spec is not so apparent here. We have larger examples of YAML config files and their corresponding python equivalent that can be found in the [examples folder in the Tasrif GitHub repo](https://github.com/qcri/tasrif/tree/master/examples).

