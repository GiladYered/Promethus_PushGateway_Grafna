docker network create monitoring
docker run -d --network monitoring --name=grafana -p 3000:3000 grafana/grafana
docker run -d -p 9091:9091 --network monitoring prom/pushgateway
docker run --rm -p 9090:9090 --network monitoring -v C:\prometheus\prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus:latest

echo "env_version{project = \"example\", version=\"0.0.2\" }" 1 | curl --data-binary @- http://localhost:9091/metrics/job/example_job
