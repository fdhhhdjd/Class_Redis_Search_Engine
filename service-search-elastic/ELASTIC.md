# This is command to create an index
```cmd
PUT product_info
```

# This is creating a document
```cmd
POST product_info/_doc
{
  "@timestamp": "2024-05-08",
  "fullname": "Nguyen Vo Tien",
  "url_profile": "https://tien.com"
}
```

# This is creating a document with a specific ID
```cmd
POST product_info/_doc/0001
{
  "@timestamp": "2021-01-08",
  "fullname": "Nguyen Van D",
  "url_profile": "https://d.com"
}
```

# This is creating a document with a specific ID (alternative method)
```cmd
PUT product_info/_doc/0002
{
  "@timestamp": "2021-01-08",
  "fullname": "Nguyen Vo Tien",
  "url_profile": "https://tien.com"
}
```

# Adding multiple documents using bulk API
```cmd
POST _bulk
{ "index": { "_index": "product_info" }}
{ "@timestamp": "2024-05-08", "fullname": "Nguyen Van A", "url_profile": "https://vanA.com" }
{ "index": { "_index": "product_info" }}
{ "@timestamp": "2020-06-23", "fullname": "Nguyen Van B", "url_profile": "https://vanB.com" }
{ "index": { "_index": "product_info" }}
{ "@timestamp": "2021-02-23", "fullname": "Nguyen Van C", "url_profile": "https://vanC.com" }
```

# Check index
```cmd
GET _cat/indices
```

# Retrieve all documents
```cmd
GET product_info/_search
```

# Delete a document
```cmd
DELETE product_info/_doc/7mPWWI8Bp27zrf6omSeA
```

# Update a document
```cmd
PUT product_info/_doc/7WPWWI8Bp27zrf6omSeA
{
  "@timestamp": "2020-02-02",
  "fullname": "Nguyen Van A",
  "url_profile": "https://a.com"
}
```

# Update a single field in a document
```cmd
POST /product_info/_update/6WPHWI8Bp27zrf6ojCeo
{
  "doc": {
      "fullname": "Nguyen Tien Tai 1"
  }
}
```

# Sort documents in descending order
```cmd
GET product_info/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "@timestamp": {
        "order": "desc"
      }
    }
  ]
}
```

# Retrieve a specific field from documents
```cmd
GET product_info/_search
{
  "query": {
    "match_all": {}
  },
  "fields": [
    "fullname"
  ], 
  "_source": false,
  "sort": [
    {
      "@timestamp": {
        "order": "desc"
      }
    }
  ]
}
```

# Retrieve document details
```cmd
GET product_info/_doc/6WPHWI8Bp27zrf6ojCeo?_source=fullname
GET product_info/_doc/6WPHWI8Bp27zrf6ojCeo?filter_path=_source
```
# Retrieve multiple documents with different IDs
```cmd
GET _mget
{
  "docs": [
    {
      "_index": "product_info",
      "_id": "6WPHWI8Bp27zrf6ojCeo",
      "_source": [
        "fullname"
      ]
    },
    {
      "_index": "product_info",
      "_id": "0002",
      "_source": [
        "fullname"
      ]
    }
  ]
}
```

# Check if a document exists
```cmd
HEAD product_info/_doc/0002
```

# Get total count of documents
```cmd
GET product_info/_count
```

# Search documents with a condition
```cmd
GET product_info/_search
{
  "query": {
    "match": {
      "fullname": "Tai"
    }
  },
  "fields": [
    "fullname"
  ], 
  "_source": false,
  "sort": [
    {
      "@timestamp": {
        "order": "desc"
      }
    }
  ]
}
```

# Search documents with true conditions
```cmd
GET product_info/_search
{
  "query": {
    "match": {
      "fullname": {
          "query": "Tien Tai",
          "operator": "and"
      }
    }
  },
  "fields": [
    "fullname"
  ], 
  "_source": false,
  "sort": [
    {
      "@timestamp": {
        "order": "desc"
      }
    }
  ]
}
```

# Search for documents with only one true word
```cmd
GET product_info/_search
{
  "query": {
    "match": {
      "fullname": {
          "query": "Tien Taia",
          "minimum_should_match": 1
      }
    }
  },
  "fields": [
    "fullname"
  ], 
  "_source": false,
  "sort": [
    {
      "@timestamp": {
        "order": "desc"
      }
    }
  ]
}
```

# Search flow sentence
```cmd
POST product_info/_search
{
  "query": {
    "match_phrase": {
      "fullname": "Van"
    }
  }
}
```

# Search flow prefix - sunfix
```cmd
POST product_info/_search
{
  "query": {
    "match_phrase_prefix": {
      "fullname": {
        "query": "ag"
      }
    }
  }
}
```

```cmd
POST product_info/_search
{
  "query": {
    "match_phrase_prefix": {
      "fullname": {
        "query": "nguy",
        "max_expansions": 2
      }
    }
  }
}
```