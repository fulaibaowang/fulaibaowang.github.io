---
title: 'Non-Empty Files_2'
date: 2023-08-10
permalink: /posts/2023/08/bash-Non-Empty-Files_2/
tags:
  - bash

---
Finding Non-Empty Files

```
find *_report.output.tsv -type f -size +0 | wc -l
```

``find *_report.output.tsv -type f -size +0 | wc -l``