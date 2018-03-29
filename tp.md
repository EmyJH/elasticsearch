# ElasticSearch
```windows
bin\elasticsearch.bat
bin\plugin install mobz/elasticsearch-head
```
http://localhost:9200/_plugin/head/

sourcee : corps du document
must
must not
should

term, wildcard, prefix, fuzzy, range, query-string, text, missing
zenika/produit/_search?q=classic   GET
zenika/produit/_search?q=titre:rune   GET

recherche sur plusieurs champs
bibli/_search?q=auteur.nom:poe OR acteur.nom:dalton   GET
bibli/_search?q=auteur.\*:poe
bibli/_search?q=\*.nom:d*

/_all/_search?q=titre:bye

/bib*,-bibli2/_search?q=venus
/bib*/_search?q=jul
/bibli2*,-bibli/_search?q=chatel

# sense
GET _search
{"query":{"bool":{"must":[{"query_string":{"default_field":"_all","query":"bye"}}],"must_not":[],"should":[]}},"from":0,"size":10,"sort":[],"aggs":{}}

# TP2 

*Creation index:
```
PUT data0
{"settings":{"index":{"number_of_shards":2,"number_of_replicas":0}}}
```
*Modif index:
```
PUT data0/_settings
{ "index" : {
"number_of_replicas": 6,
"refresh_interval": "30s"
}}
```
*Creation d'alias:
```
POST /_aliases
{
    "actions" : [
        { "add" : { "index" : "test1", "alias" : "alias1" } },
        { "add" : { "index" : "test2", "alias" : "alias1" } }
    ]
}
```

*Suppression de tout :
}
```
DELETE /_all
}
```
*Mapping :
}
```
{
  "mappings": {
    "produit": {
      "properties": {
        "code": {
          "type": "string",
          "index": "not_analyzed",
          "store": true
        },
        "name": {
          "properties": {
            "nom": {
              "type": "string",
              "index": "analyzed",
              "store": "true"
            },
            "original": {
              "type": "string",
              "index": "not_analyzed",
              "store": "true"
            }
          }
        },
        "echelle": {
          "type": "string",
          "index": "not_analyzed"
        },
        "fournisseur": {
          "type": "string",
          "index": "analyzed",
          "null_value": "unknow",
          "store": true
        },
        "stock": {
          "type": "integer"
        },
        "prix": {
          "type": "float"
        },
        "devise": {
          "type": "string",
          "index": "not_analyzed"
        }
      }
    }
  }
}
*vérification de l'existance GET /data/_mapping
*à rajouter "include_in_all": true,

