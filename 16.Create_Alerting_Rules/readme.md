## Scenerio:

After deploying a Prometheus environment to our Kubernetes cluster, the team has decided to test its monitoring capabilities by configuring alerting of our Redis deployment. We have been tasked with writing two alerting rules. The first rule will fire an alert if any of the Redis pods are down for 10 minutes. The second alert will fire if there are no pods available for 1 minute.

## Tasks:

* Use `prometheus-rules-config-map.yml` located in `/root/prometheus`  to create a configuration map for the Redis alerting rules

* Under the data section, add a new file called `redis-alerts.yml`.

* Create an alerting group called `redis_alerts`. This group will contain two rules: `RedisServerGone` and `RedisServerDown`.

* In The `RedisServerDown` alert, the expression uses the redis_up metric and is filtered using the label app with media-redis as the value. The condition will equal 0. The alert will fire if the condition remains true for 10 minutes. The alert has a severity of critical.

* Add a summary in annotations that says `“Redis Server <SERVER_NAME> is down!”`

* Replace `<SERVER_NAME>` with the templating syntax that displays the instance label.

* In The RedisServerGone alert; For the expression, use the absent function to evaluate the redis_up metric. Filter using the app label with a value of media-redis. The alert will fire if the condition remains true for 1 minute. The alert has a severity of critical.

* Add a summary in annotations that says `“No Redis servers are reporting!”`

* Apply the changes made in prometheus-rules-config-map.yml. Make sure the rules propagate into Prometheus.

* Delete the Prometheus pod to make the rules propagate.

* Verify the rules are showing up by clicking on Alerts.

![](./img/Prometheus%20labs%20-%20Lab3.png)