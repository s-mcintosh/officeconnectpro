---
title: {{ .Title | jsonify }}
url: "{{ .Permalink }}"
{{ with .Description }}description: {{ . | jsonify }}
{{ end -}}
{{ with .Params.tags }}tags: {{ . | jsonify }}
{{ end -}}
date: "{{ .Date.Format "2006-01-02" }}"
lastmod: "{{ .Lastmod.Format "2006-01-02" }}"
---

{{ .RawContent }}
