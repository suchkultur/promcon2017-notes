# PromCon 2017 in munich

## About

From the [PromCon website][1]:

**PromCon 2017 will be the second conference around the Prometheus monitoring system.
It will take place from August 17 - 18 at Google Munich and will be a single-track
event with space for 200 attendants. All talks will be recorded and published after
the event to create maximum exposure.**

**PromCon aims to connect Prometheus users and developers from around the world in
order to exchange knowledge, best practices, and experience gained around using Prometheus.
We also want to collaborate to build a community and grow professional connections around
systems and service monitoring.**

## Schedule

The schedule can be found [here][2] and will be linked in the following notes.

## The conference in general

... tell about people. companies, problems & solution or use-cases, general mood, the microservice and distributed world of computing, 

* Prometheus is a swiss army knive for all things gathering metrics and querying them with statistical functions
  * Server monitoring
  * Service monitoring
  * IoT and sensor monitoring
  * Load Test monitoring
* Specially white box monitoring
* General idea: gather lots of metrics quite often and model easy to (very) complex queries to get valuable insight (and react automatically if needed)
  * Give 2-3 queries as examples
* Prometheus and Grafana are best friends => Grafana allows for eyecandy dashboards, aggregation and making sense of data visually or even alert
* brian brazil gets his fett weg

## Welcome

200 people

1 year:
360->650 contributors
50->200+ third party integrations

CERN, NYT, DB (all linux with node exporter and prometheus),
google, redhat, digitalocean,...)

##  https://promcon.io/2017-munich/talks/monitoring-cloudflares-planet-scale-edge-network-with-prometheus

* @mattbostock
* cdn
* 185 prometheus servers
* 4 top level servers (federating)
* 15 days data retention
* more interesting data on the slides
* benutzen mtail für logging to metrics
* jeder prom node monitored die anderen im datacenter
* coole mentionings von diversen tools in den slides weiter hinten
* lesson learned: standardise metric labels early
* alertmanager quite unreliable at their site

## https://promcon.io/2017-munich/talks/start-your-engines-white-box-monitoring-for-load-tests

* Prometheus als TSDB für load testing
* add the same metrics in test and prod
* jmeter, gatling, 
* USE und RED method
  * utilization, saturation, errors for cpu, disk, ...
  * i. e. for endpoints: request rate, error rate, duration (distribution)

## Best Practices and Beastly Pitfalls

* Talks about good and bad practices
* Lots of examples and explanations
* Some details and rules of thumbs
* Important: Metrics and their labels should not overlap
* Every unique set of labels creates a new series
  * dont i. e. labels never should contain ids or io addresses or whatever can "explode" in terms of the sum of time series generated
* labels should be quite static
* sometimes it is a good idea to add another metric with a label which can be JOINed at query time
* Rob Ewaschuk "My Philosophy on Alerting"
* dont alert on timeseries only, ALSO alert always if stuff is up or down in general!!
* rate() von counter werten kommen mit counter resets klar. sums nicht. 

## https://promcon.io/2017-munich/talks/prometheus-as-a-internal-service

* promgen web ui to generate and maintain prometheus configurations
* Does also query shards for federation (proxy function)
* Should be checked out

## https://promcon.io/2017-munich/talks/grafana-and-prometheus

* Grafana + Prometheus
* Update-Tool zu neuen Features rund um Grafana
* Grafana PromQL has now syntax highlighting, function docs etc. - sau cool
* checkout diagram plugin
* Development is rapid
* 92000 Grafana installs have 16000 prometheus datasources enabled

## https://promcon.io/2017-munich/talks/why-we-love-prometheus-even-though-i-hate-it

* vpn provider
* trying to like prometheus but hit every problem they could
* nice talk to watch if you think all things are great in prom world
* https://www.anchorfree.com
* Several thousand nodes
* 200 countries

## https://promcon.io/2017-munich/talks/analyze-prometheus-metrics-like-a-data-scientist

* pushing the boundaries from the perspective of datascience
* some examples like prediction of latency in http requests

## https://promcon.io/2017-munich/talks/alertmanager-and-high-availability

* coreos origin
* crreating ha alertmanager 
* they use gossip (like consul, cassandra) for HA between alertmanagers
* internally they use mesh from weaveworks
* ha is now directly in alertmanager 

## https://promcon.io/2017-munich/talks/play-with-prometheus

* dev driven (no testing, canary deployment)
* all cloud
* all containers and aws

## https://promcon.io/2017-munich/talks/the-uninstrumentable-getting-apache-spark-and-prometheus-to-play-nicely

* FUNNY talk. two peole + british humor
* Apache Spark + PySpark
* multiple short lived workers push to the push gateway
* quite big project

## https://promcon.io/2017-munich/talks/social-aspects-of-change

* social challenges in big environments for monitoring
* all about change
* Remove toil (mühevolle arbeit)

## https://promcon.io/2017-munich/talks/cortex-prometheus-as-a-service-one-year-on

missed that one.

## https://promcon.io/2017-munich/talks/prometheus-everything-observing-kubernetes-in-the-cloud

missed that one, too.

## https://promcon.io/2017-munich/talks/integrating-prometheus-and-influxdb

* Influx-DB has fields
* Generischere Abfragesprache
  * Sql artig; will be replaced by IFQL in the future
  * a [directed A graph (DAG)](https://en.m.wikipedia.org/wiki/Directed_acyclic_graph) will be used to support multiple query languages by the engine
* "Process" kapacitor product
* More general use case compared to the TSDB prom already includes
* Influx and Prometheus share code and (want) to work together

## https://promcon.io/2017-munich/talks/a-worked-example-of-monitoring-a-queue-based-application

* to be honest: not so intersting talk about just using prometheus
* OTOH: Good real life examples for queue monitoring code, promql queries and grafana dashboards
* Good examples for usage at QuoScient

## https://promcon.io/2017-munich/talks/storing-16-bytes-at-scale

* prometheus: 8 byte timestamp + 8 byte data per TSDB entry
* Compression! Unix timestamps can be written short by using offsets and even these can be compressed
* In the end: 16 bytes per sample => 1.37 bytes per sample on Prometheus 2 by implementing all compression
* 7TB => ~0.8TB
* Churn is a problem in timeseries. This will be solved and the slides explain how in a graphical way. Also there is a blog post from [Fabian](https://twitter.com/fabxc)
* Lots of more improvements in terms of hardware usage and performance + efficiency

Great blogpost: https://fabxc.org/blog/2017-04-10-writing-a-tsdb/

## https://promcon.io/2017-munich/talks/improving-user-and-developer-experience-of-the-alertmanager-ui

* Old alert manager ui could be improved or rewritten
  * Grouping, Filtering, Create/Preview alerts
* New UI uses elm. It is s functional language which compiles to javascript. Reasons: Maintainable and usable.  
* statically typed, pure functions, great compiler, no runtime exceptions, no front end regressions, etc.
* routing tree is missing (will be back soon)
* Talks about how to work with elm
* 183 commits => merge replaces old ui with new ui

## https://promcon.io/2017-munich/talks/using-tsdb-as-a-library

* FUNNY talk. Nice guy. 
* PromFlux - prometheus with PUSH
* Simple
* Showed go code which uses prom tsdb as a library for pushing ts data

## https://promcon.io/2017-munich/talks/staleness-in-prometheus-2-0

* Staleness is an old problem since 2014 which leads into some - at least - inconvenient behaviour(s).
  * Brian gives some examples in his slides
* A lot of technical insight on the changes

## https://promcon.io/2017-munich/talks/lightning-talks-day2

* Many nice little pet projects and use cases

[1]: https://promcon.io/2017-munich/
[2]: https://promcon.io/2017-munich/schedule/