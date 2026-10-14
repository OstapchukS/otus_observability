# otus_observability
GAP-1

На ВМ Ubuntu:
- развернута CMS Made Simple
- устновлены и запущены:
  - node_exporter
  - mysql_exporter
  - blackbox_exporter

На докер сервере в этой же сети запущен Prometheus с джобами:
  - сам prometheus
  - vm
  - mysql
  - blackbox_cms

GAP-2

На докер сервере 
- добавлен контейнер victoriametrics с хранением данных 14 дней
- на prometheus:
  - добавлен remote_write -- хранение данных в victoriametrics
  - для всех метрик через external_labels добавлен лейбл site: prod 

GAP-3
В докере установлен alertmanager 
- в настройках прометеус в alerting указан адрес:порт алертменеджера и подключен файл с правилами алертинга через rule_files
- в alert.rules.yml добалены два правила -- недоступность таргета мониторинга(critical) и высокая нагрузка на процессор инстанса(warning)
- в настройках alertmanager.yml отдельно для critical и warning указаны отдельные маршруты отправки уведомлений (два телеграм канала)
