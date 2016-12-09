# pubmedtrending

NCBI pubmed trending data


Pierre Lindenbaum PhD @yokofakun

## Notes to self

```
#!/bin/bash
date +%Y-%m-%d | tr "\n" "\t" && \
curl -s -x "proxy-upgrade.univ-nantes.prive:3128" "http://www.ncbi.nlm.nih.gov/pubmed/trending/"  |\
xsltproc --html /commun/data/users/lindenb/src/xslt-sandbox/stylesheets/bio/ncbi/pubmedtrending2rss.xsl - 2> /dev/null |\
grep "<guid " | cut -d '>' -f 2 | cut -d '<' -f 1 | sed 's%http://www.ncbi.nlm.nih.gov/pubmed/%%' | tr "\n" "," | sed 's/,$//' && echo


in cron:

```bash
#!/bin/bash
date +%Y-%m-%d | tr "\n" "\t" && \
curl -s -x "(host):(port)" "https://www.ncbi.nlm.nih.gov/pubmed/trending/"  |\
xsltproc --html /path/to/xslt-sandbox/stylesheets/bio/ncbi/pubmedtrending2rss.xsl - 2> /dev/null |\
grep "<guid " | cut -d '>' -f 2 | cut -d '<' -f 1 | sed 's%http://www.ncbi.nlm.nih.gov/pubmed/%%' | tr "\n" "," | sed 's/,$//' && echo
```

visualize:


https://cdn.rawgit.com/lindenb/pubmedtrending/master/data.html
