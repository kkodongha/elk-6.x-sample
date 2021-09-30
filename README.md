```
PUT /news
{
  "settings" : {
    "number_of_shards" : "3",
    "number_of_replicas" : "1",
    "analysis": {
      "analyzer": {
        "nori_analyzer": {
          "tokenizer": "nori_tokenizer",
          "type": "custom"
        }
      },
      "filter": {},
      "tokenizer": {
        "nori_tokenizer": {
          "type": "nori_tokenizer",
          "decompound_mode": "mixed"
        }
      }
    }
  },
  "mappings": {
    "properties": {
			"language": {
        "type": "keyword"
      },
      "category": {
        "type": "keyword"
      },
      "copyright": {
        "type": "text",
        "fields": {
          "keyword": {
            "type": "keyword",
            "ignore_above": 256
          }
        }
      },
			"title": {
        "type": "text",
        "fields": {
          "keyword": {
            "type": "keyword",
            "ignore_above": 256
          },
          "nori_analyzer": {
            "type": "text",
            "analyzer": "nori_analyzer"
          }
        }
      },
      "link": {
        "type": "text",
        "fields": {
          "keyword": {
            "type": "keyword",
            "ignore_above": 256
          }
        }
      },
      "description_summary": {
        "type": "text",
        "fields": {
          "keyword": {
            "type": "keyword",
            "ignore_above": 256
          },
          "nori_analyzer": {
            "type": "text",
            "analyzer": "nori_analyzer"
          }
        }
      },
      "pubDate": {
        "type": "keyword"
      }
    }
  }
}
```
