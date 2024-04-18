# hsa-11-es
Раніще не працював з ES, тому трішки було складнувати - не до кінця зробив так як вимагалось в домашньому завданні, але вдалось погратись з ES \
Додаток не створював, вигрузив записив за допомогою балк реквесту та інші запити, також надсилав з постамана \
<img width="1440" alt="image" src="https://github.com/VitalikMatvieiev/hsa-11-es/assets/77060767/8283490d-5741-4a13-9e18-c2b6cc7ccf25">

## Bulk
curl -XPOST localhost:9200/movies/_bulk -d

## fuzziness
```
http://localhost:9200/first_index_search/_search
{
    "query": {
      "fuzzy": {
        "suggest_field": {
          "value": "googlee",
          "fuzziness": 2
        }
      }
    }
  }
```
## N-gram
```
PUT http://localhost:9200/movies3
{
    "settings": {
            "analysis": {
                "analyzer": {
                    "custom_edge_ngram_analyzer": {
                        "type": "custom",
                        "tokenizer": "customized_edge_tokenizer",
                        "filter": [
                            "lowercase"
                        ]
                    }
                },
                "tokenizer": {
                    "customized_edge_tokenizer": {
                        "type": "edge_ngram",
                        "min_gram": 2,
                        "max_gram": 10,
                        "token_chars": [
                            "letter",
                            "digit"
                        ]
                    }
                }
            }
        },
        "mappings": {
            "properties": {
                "title": {
                    "type": "text",
                    "analyzer": "custom_edge_ngram_analyzer"
                }
            }
      }
}
```
