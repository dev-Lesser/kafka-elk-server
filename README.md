# Elastic stack docker

https://github.com/deviantony/docker-elk

## 실행
```
docker-compose build
docker-compose up -d
```

## logstash 설정
```
logstash/pipeline/logstash.conf

input {
 	kafka {
		client_id => "logstash-test-topic"
		group_id => "logstash-test-topic"
		topics => ["gt2100", "gt2600"] -> 토픽종류
		consumer_threads => 10
		decorate_events => true
		codec => "json" -> json 형식으로 변환하여 ES에 저장
		bootstrap_servers => "kafka:29092"
  	}
}

## Add your filters / logstash plugins configuration here

output {
	elasticsearch {
		hosts => "elasticsearch:9200"
		index => "factory" -> 인덱스 이름 (자동저장)
	}
}
```