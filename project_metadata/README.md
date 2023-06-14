# Metadata on CorrelAid Data4Good Projects

## License
 
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Dataset" property="dct:title" rel="dct:type">Metadata on CorrelAid Data4Good Projects</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://correlaid.org" property="cc:attributionName" rel="cc:attributionURL">CorrelAid e.V.</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.<br />Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="https://raw.githubusercontent.com/CorrelAid/open-data/main/project_metadata/correlaid_project_metadata.json" rel="dct:source">https://raw.githubusercontent.com/CorrelAid/open-data/main/project_metadata/correlaid_project_metadata.json</a>.

See LICENSE for the full license text. The text above can be used for attribution purposes. 


## Simple analysis with jq

You can use the [tool `jq`](https://jqlang.github.io/jq/) in the terminal to get a quick impression of the data. For example:

Get metadata: 

```
curl https://raw.githubusercontent.com/CorrelAid/open-data/main/project_metadata/correlaid_project_metadata.json | jq '.meta'
```

Title and duration of each project:

```
curl https://raw.githubusercontent.com/CorrelAid/open-data/main/project_metadata/correlaid_project_metadata.json | jq '.projects[] | {title: .translations[] | select(.language == "en-US") | .title, duration: (.start_date + " - " +  .end_date) }'
```

Number of projects per type: 

```
curl https://raw.githubusercontent.com/CorrelAid/open-data/main/project_metadata/correlaid_project_metadata.json | jq '.projects| map(.type[] | ascii_downcase) | group_by(.) | map({"type": .[0], "count": length})'
```

Number of projects per language: 

```
curl https://raw.githubusercontent.com/CorrelAid/open-data/main/project_metadata/correlaid_project_metadata.json | jq '.projects| map(.language[] | ascii_downcase) | group_by(.) | map({"lang": .[0], "count": length})'
```

