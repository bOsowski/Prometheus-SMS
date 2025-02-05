![Alt text](./sms.png?raw=true "SMS")


# SMS Proxy API

## Motivation

Prometheus’s AlertManager receives the alerts send from Prometheus’ alerting rules, and then manages them accordingly. One of the action is to send out external notifications such as Email, SMS, Chats. Out of box, AlertManager provides a rich set of integrations for the notifications. However, in real life projects, these lists are always not enough. 
To overcome this problem,  we created this code to integrate SMS provider's API with webhook reciever.

SMS Proxy is a lightweight code, running in docker, which makes it easy to integrate with Prometheus' Alertmanager webhook receiver. [See Alertmanager Documentation](https://prometheus.io/docs/alerting/latest/configuration/#webhook_config)


### Clone

- Clone this repository `git clone git@github.com:Nandi-Ai/SMS-Proxy.git`

### Description

#### SMS Proxy using Python Flask

This webhook receiver supports the following SMS provider APIs:
* Nexmo
* Message Bird
* Telemessage
* World-Text

It integrates with Prometheus' AlertManager API.

The `config` file allows you to define all variables needed.

### How to use
> Docker
- Run `docker build -t sms-proxy -f Dockerfile .`
- Run `docker run --shm-size=256m --detach -p 8000:8000 sms-proxy:latest`

> Without Docker
- Run `pip3 install -r requirements.txt`
- Run `python3 sms.py`



### Testing

```
$ curl -H "Content-type: application/json" -X POST \
  -d '{"receiver": "team-sms", "status": "firing", "alerts": [{"status": "firing", "generatorURL":"127.0.0.1", "labels": {"alertname": "test-123"} }], "commonLabels": {"key": "value"}}' \
  http://localhost:9876/alert
```
