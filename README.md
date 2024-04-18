# hsa-11-es
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
