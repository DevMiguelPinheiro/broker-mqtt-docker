# Broker MQTT Docker - Mosquitto Local

Este repositório demonstra como subir um broker Mosquitto MQTT local usando Docker Desktop para testes.

## Características

- ✅ Broker Mosquitto local
- ✅ Sem credenciais de acesso (`allow_anonymous true`)
- ✅ Porta MQTT: 1883
- ✅ Porta WebSocket: 9001
- ✅ Configuração simples para testes

## Pré-requisitos

- Docker Desktop instalado e rodando
- Docker Compose (geralmente já vem com Docker Desktop)

## Como usar

### 1. Iniciar o broker

```bash
docker-compose up -d
```

### 2. Verificar se está rodando

```bash
docker-compose ps
```

Você deve ver o container `mosquitto-broker` com status "Up".

### 3. Ver os logs

```bash
docker-compose logs -f mosquitto
```

### 4. Testar o broker

#### Usando mosquitto_sub e mosquitto_pub (se tiver instalado localmente):

Terminal 1 - Subscriber:
```bash
mosquitto_sub -h localhost -p 1883 -t "teste/#" -v
```

Terminal 2 - Publisher:
```bash
mosquitto_pub -h localhost -p 1883 -t "teste/mensagem" -m "Olá, MQTT!"
```

#### Usando Docker (sem precisar instalar nada):

Terminal 1 - Subscriber:
```bash
docker run -it --rm --network host eclipse-mosquitto mosquitto_sub -h localhost -p 1883 -t "teste/#" -v
```

Terminal 2 - Publisher:
```bash
docker run -it --rm --network host eclipse-mosquitto mosquitto_pub -h localhost -p 1883 -t "teste/mensagem" -m "Olá, MQTT!"
```

### 5. Parar o broker

```bash
docker-compose down
```

## Estrutura do Projeto

```
.
├── docker-compose.yml          # Configuração do Docker Compose
├── mosquitto/
│   ├── config/
│   │   └── mosquitto.conf     # Configuração do Mosquitto
│   ├── data/                  # Dados persistentes
│   └── log/                   # Logs do broker
└── README.md
```

## Configuração

O arquivo `mosquitto/config/mosquitto.conf` contém:
- `allow_anonymous true` - Permite conexões sem autenticação
- Listener MQTT na porta 1883
- Listener WebSocket na porta 9001
- Persistência de dados habilitada
- Logs detalhados

## Conexão

Para conectar ao broker a partir de qualquer aplicação:

- **Host**: `localhost` (ou `127.0.0.1`)
- **Porta**: `1883` (MQTT) ou `9001` (WebSocket)
- **Usuário**: Não necessário (allow_anonymous)
- **Senha**: Não necessário (allow_anonymous)

## Troubleshooting

### Porta já em uso
Se você receber erro de porta já em uso, você pode:
1. Parar o serviço que está usando a porta
2. Ou modificar as portas no `docker-compose.yml`

### Permissões
Se tiver problemas de permissão nas pastas `data` ou `log`:
```bash
sudo chmod -R 755 mosquitto/
```

## Notas

⚠️ **ATENÇÃO**: Esta configuração é para ambiente de desenvolvimento/teste local apenas. 
Para produção, sempre use autenticação e criptografia (TLS/SSL).