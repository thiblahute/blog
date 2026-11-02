---
title: "{{ replace .File.ContentBaseName "-" " " | title }}"
date: {{ .Date }}
slug: {{ .File.ContentBaseName }}
tags: [planet]
draft: true
---

