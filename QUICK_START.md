# Quick Start Guide

## Start the broker
```bash
docker-compose up -d
```

## Check if it's running
```bash
docker-compose ps
docker-compose logs mosquitto
```

## Test with Docker (no installation needed)

### Terminal 1 - Subscribe to messages
```bash
docker run -it --rm --network host eclipse-mosquitto mosquitto_sub -h localhost -p 1883 -t "test/#" -v
```

### Terminal 2 - Publish a message
```bash
docker run -it --rm --network host eclipse-mosquitto mosquitto_pub -h localhost -p 1883 -t "test/message" -m "Hello MQTT!"
```

## Stop the broker
```bash
docker-compose down
```

## Connection Details
- **Host**: localhost
- **Port**: 1883 (MQTT) or 9001 (WebSocket)
- **Authentication**: None (anonymous allowed)
- **Credentials**: Not required
