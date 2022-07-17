# 뉴스 데이터 저장소 (with. ELK Stack)

### 프로젝트 진행 이유

신문 데이터의 형태소 분석, 자소 분석, 동의어 등을 이용한 통합 검색과 유사도 검색을 통한 복사 뉴스 추출 등의 기능

### **Version**

Elasticsearch : 7.13.2  
Logstash : 7.13.2  
Kibana : 7.13.2

### 프로젝트 단계

step1. ELK Stack 구성  
step2. 신문 제목, 내용에 Nori-형태소 분석기 사용한 검색  
step3. 신문 제목에 자소 분석기 사용한 검색  
step4. 신문사명의 동의어를 이용한 검색  
step5. 전체 기사별 유사도 검색  
step6. 그 외 통계 정보 추출(일자별 가장 많이 나온 단어 등)

### **사용 분석기**

형태소 분석기 : nori-analyzer  
자소 분석기 : elasticsearch-jaso-analyzer

### **news index 생성 구문**

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
      "description": {
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
