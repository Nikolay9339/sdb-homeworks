# Домашнее задание к занятию «ELK»

**Захарян Николай Артурович** 

## Задание 1. Elasticsearch

**1. Команда проверки состояния кластера:**
```bash
curl -X GET 'localhost:9200/_cluster/health?pretty'

<img width="738" height="348" alt="2026-10-02_09-58-49" src="https://github.com/user-attachments/assets/75371404-47eb-438f-a3d0-ecd6728f1112" />

## Задание 2. Kibana

1. URL для доступа:
http://192.168.111.133:5601/app/dev_tools#/console
2. Выполненный запрос в Dev Tools:
GET /_cluster/health?pretty
<img width="1920" height="496" alt="2026-10-02_11-31-40" src="https://github.com/user-attachments/assets/272b6b81-59a1-4281-97d4-68c0a38f7d2a" />

## Задание 3. Logstash
1. Фрагмент конфигурации Logstash (logstash.conf):

input {
  file {
    path => "/var/log/nginx/access.log"
    start_position => "beginning"
    sincedb_path => "/dev/null"
  }
}
filter {
  grok {
    match => { "message" => "%{COMBINEDAPACHELOG}" }
  }
}
output {
  elasticsearch {
    hosts => ["http://elasticsearch:9200"]
    index => "nginx-logs-%{+YYYY.MM.dd}"
  }
}

<img width="1920" height="739" alt="2026-10-02_11-38-02" src="https://github.com/user-attachments/assets/0be62da7-f841-402d-a855-ba235960801d" />

## Задание 4. Filebeat
1. Фрагмент конфигурации Filebeat (filebeat.yml):

filebeat.inputs:
- type: log
  enabled: true
  paths:
    - /var/log/nginx/access.log

output.elasticsearch:
  hosts: ["http://elasticsearch:9200"]
  indices:
    - index: "filebeat-nginx-logs-%{+yyyy.MM.dd}"

<img width="1920" height="898" alt="2026-10-02_11-43-18" src="https://github.com/user-attachments/assets/1816cb3f-bf64-44a6-aa3c-4015a55b9a35" />

