
Index Creation : 
  Index r1 - curl -XPUT "http://localhost:9200/r1?pretty" -H 'Content-Type: application/json' -d '{"mappings": {"properties": {"remip": {"type": "keyword"}}}}'
  
  Index r2 - curl -XPUT "http://localhost:9200/r2?pretty" -H 'Content-Type: application/json' -d '{"mappings": {"properties": {"remip": {"type": "ip"}}}}'

Indexing docs : (remote_ip_string_ip_datatype_change file added in this repo)
  curl -s -H "Content-Type: application/x-ndjson" -XPOST localhost:9200/r2/_bulk?pretty --data-binary "@remote_ip_string_ip_datatype_change"; echo

Search query : curl -X GET "localhost:9200/r*/_search?pretty" -H 'Content-Type: application/json' -d '{"aggs": {"genres": {"terms": { "field": "remip" }}}}'
