## Availability SLI
### The percentage of successful requests over the last 5m
sum (rate(flask_http_request_total{status!~"5.."}[5m]))
/
sum (rate(flask_http_request_total[5m]))



## Latency SLI
### 90% of requests finish in these times

histogram_quantile(0.90,sum(rate(flask_http_request_duration_seconds_bucket{status=~"2.."}[5m])) by (le))



## Throughput
### Successful requests per second
sum(rate(flask_http_request_total{status=~"2.."}[5m]))


## Error Budget - Remaining Error Budget
### The error budget is 20%
1 - ((1 - (sum(increase(flask_http_request_total{status="200"})) by (status)) / sum(increase(flask_http_request_total) by (status)) / (1 - .80))

1 - (1 - (sum(increase(flask_http_request_total{status=~"2.."}[5m]))
/
sum(increase(flask_http_request_total[5m])))
/
(1 - 0.20))
