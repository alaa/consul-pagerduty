# Consul-Pagerduty

consul-pagerduty is a simple service that watches the health check's status on Consul
and notifies pagerduty upon failure.

## Usage
```
docker run -d \
           -e CONSUL_ADDR=<$CONSUL_ADDRESS:8500> \
           -e PAGERDUTY_SERVICE_KEY=<$PAGERDUTY_SERIVCE_KEY> \
           alaa/consul-pagerduty:latest
```

## Running consul-pagerduty on Marathon

The dockerized consul-pagerduty memory footprint is arount 8.0 mb.

```
[{
  "id": "notifier",
  "cpus": 0.1,
  "mem": 16.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "alaa/consul-pagerduty:latest",
      "forcePullImage": true
    }
  },
  "env": {
    "CONSUL_ADDR": "$CONSUL_ADDR",
    "PAGERDUTY_SERVICE_KEY": "$PAGERDUTY_SERVICE_KEY"
  }
}]
```

## TODO

- Split code into packges
- Write some tests
- Implement distributed locking to provide HA for multiple instances
