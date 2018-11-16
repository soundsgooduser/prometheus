INFO:
https://prometheus.io/docs/introduction/overview/
https://kjanshair.github.io/2018/07/26/prometheus-alert-manager/
https://daenney.github.io/2018/04/21/setting-up-alertmanager
https://github.com/prometheus/alertmanager/issues/437
https://api.slack.com/apps/AE370HKMW/incoming-webhooks?success=1

ON MAC:
Steps to run target with prometheus exporters, prometheus, alertmanager, and slack:

1. clone and start target app:
	cd /Users/mykhaylo_hrytsiv/workspaces/
	git clone https://github.com/prometheus/client_golang.git
	cd client_golang/examples/random
	go get -d
	go build
	./random -listen-address=:8080
    http://localhost:8080/metrics

2. run prometheus:
    docker run -d -p 9090:9090 -v /Users/mykhaylo_hrytsiv/data/prometheus.yml:/etc/prometheus/prometheus.yml -v /Users/mykhaylo_hrytsiv/data/alerts.yml:/etc/prometheus/alerts.yml prom/prometheus
    http://localhost:9090/alerts

3. run slack

4. run alertmanager:
    cd /usr/local/go/src/github.com/prometheus/alertmanager
    sudo ./alertmanager --config.file=/Users/mykhaylo_hrytsiv/workspaces/alertmanager/doc/examples/simple.yml
    http://localhost:9093/#/status
    curl -H "Content-Type: application/json" -d '[{"labels":{"alertname":"MyTestAlert"}}]' localhost:9093/api/v1/alerts
    check slack channel if "MyTestAlert" arrived to channel

5. go to http://localhost:9090/alerts and check if alert has been firing and check if notification exists in slack channel