# Docker ELK stack + grafana

Run the ELK stack (Elasticseach, Logstash, Kibana) + grafana stack with Docker.

It will give you the ability to analyze any data set by using the searching/aggregation capabilities of Elasticseach and the visualization power of Kibana and Grafana (which now supports elasticsearch as a datastore).

Based on the official images:

* [elasticsearch](https://registry.hub.docker.com/_/elasticsearch/)
* [logstash](https://registry.hub.docker.com/_/logstash/)
* [kibana](https://registry.hub.docker.com/_/kibana/)
* [grafana](https://hub.docker.com/r/grafana/grafana/)

# Requirements

## Setup

1. Install [Docker](http://docker.io) and [Docker-compose](http://docs.docker.com/compose/install/). For OSX and Windows users the most straightforward way is to use [Docker Toolbox](https://www.docker.com/products/docker-toolbox).
2. Clone this repository

# Usage

Start the ELK stack + grafana using *docker-compose* (run in background - detached mode):

```bash
$ docker-compose up -d
```

Now that the stack is running, you'll want to inject logs in it. The shipped logstash configuration allows you to send content via tcp:

```bash
$ nc localhost 5000 < /path/to/logfile.log
```

Access Kibana UI by hitting [http://localhost:5601](http://localhost:5601) with a web browser.
Access Grafana UI by hitting [http://localhost:3000](http://localhost:3000) with a web browser.

By default, the stack exposes the following ports:
* 5000: Logstash TCP input 1 (logs are indexed into index with pattern "logs_5000-index-%{+YYYY.MM.dd}").
* 6000: Logstash TCP input 2 (logs are indexed into index with pattern "logs_6000-index-%{+YYYY.MM.dd}").
* 9200: Elasticsearch HTTP
* 9300: Elasticsearch TCP transport
* 5601: Kibana
* 3000: Grafana

*WARNING*: If you're using *boot2docker*, you must access it via the *boot2docker* IP address instead of *localhost*.

*WARNING*: If you're using *Docker Toolbox*, you must access it via the *docker-machine* IP address instead of *localhost*.