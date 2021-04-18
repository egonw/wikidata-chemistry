# wikidata-chemistry

Cache of Chemistry in Wikidata

```shell
sudo apt install rename
curl -H "Accept: text/tab-separated-values" --data-urlencode query@wikidata/inchikeys.rq -G https://query.wikidata.org/bigdata/namespace/wdq/sparql -o tmp1.tsv
cat tmp1.tsv | sed -e "s/\"Q//" | sed -e "s/\"//g" | grep -v "wikidata" | sort -n | sed -e 's/^/Q/' | split -l 12500 -d -a 3 - inchikeys_
rm inchikeys/inchikeys*.tsv
rename 's/(.*)/$1.tsv/' inchikeys_*
mv inchikeys_* inchikeys/.
```

Making release is occassionaly done, upon request. Each release contains the full TSV file
as attachment for easy reuse.

```shell
cat tmp1.tsv | sed -e "s/\"Q//" | sed -e "s/\"//g" | grep -v "wikidata" | sort -n | sed -e 's/^/Q/' > inchikeys`date +"%Y%m%d"`.tsv
```
