---
title: 'Non-Empty Files'
date: 2023-08-09
permalink: /posts/2023/08/bash-Non-Empty-Files/
tags:
  - bash

---
Finding Non-Empty Files

```
find *_report.output.tsv -type f -size +0 | wc -l
```

``find *_report.output.tsv -type f -size +0 | wc -l``