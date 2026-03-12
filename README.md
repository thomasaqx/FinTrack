# 💰 FinTrack — App de Finanças Pessoais em Go

> Sistema de finanças pessoais construído em **GoLang** para aprendizado prático de tecnologias back-end: REST, gRPC, GraphQL, Kafka, Redis, PostgreSQL e AWS Lambda.

---

## 🎯 Objetivo

Projeto pessoal focado em **fixar conceitos de programação**, e aplicar tecnologias usadas em ambientes profissionais.

---

## 🏗️ Arquitetura

```
┌──────────────┐     ┌──────────────────┐     ┌─────────────┐
│   CLI / API  │────▶│   Go Backend     │────▶│  PostgreSQL  │
│  (REST/gRPC) │     │                  │     └─────────────┘
└──────────────┘     │  ┌────────────┐  │     ┌─────────────┐
                     │  │ goroutines │  │────▶│    Redis     │
┌──────────────┐     │  │ channels   │  │     │   (cache)    │
│   GraphQL    │────▶│  │ workers    │  │     └─────────────┘
│  (consultas) │     │  └────────────┘  │     ┌─────────────┐
└──────────────┘     │                  │────▶│    Kafka     │
                     └──────────────────┘     │  (eventos)   │
                                              └─────────────┘
```

---

## 🛠️ Tech Stack

| Tecnologia | Uso no Projeto | Conceito |
|---|---|---|
| **Go** | Linguagem principal | Interfaces, composição, error handling |
| **Goroutines/Channels** | Import CSV, workers, pipelines | Concorrência, fan-out/fan-in |
| **Maps** | Categorização, roteamento | Strategy pattern, lookup tables |
| **PostgreSQL** | Persistência de dados | SQL, migrations, queries complexas |
| **Redis** | Cache de saldos e resumos | Cache-aside pattern, TTL |
| **Kafka** | Eventos de transações | Event-driven, producer/consumer |
| **gRPC** | Serviço de relatórios | Protobuf, comunicação entre serviços |
| **GraphQL** | Dashboard e consultas | Resolvers, queries flexíveis |
| **REST API** | CRUD principal | HTTP, middleware, JSON |
| **AWS Lambda** | Automações mensais | Serverless, triggers |

---

## 📁 Estrutura do Projeto

```
fintrack/
├── cmd/
│   ├── api/            # REST + GraphQL server
│   ├── grpc/           # gRPC server
│   ├── worker/         # Kafka consumers
│   └── lambda/         # AWS Lambda handlers
├── internal/
│   ├── domain/         # Entities, interfaces (Transaction, User, Budget)
│   ├── service/        # Business logic
│   ├── repository/     # Postgres, Redis implementations
│   ├── kafka/          # Producer/Consumer
│   ├── cache/          # Redis cache layer
│   └── api/
│       ├── rest/       # HTTP handlers
│       ├── grpc/       # gRPC handlers
│       └── graphql/    # GraphQL resolvers
├── pkg/                # Shared utilities
├── migrations/         # SQL migrations
├── docker-compose.yml
├── go.mod
└── Makefile
```

---

## 📅 Roadmap — 8 Semanas

### Semana 1-2: Core + REST API
- [ ] Setup do projeto (`go mod`, estrutura de pastas)
- [ ] Modelagem do banco (users, transactions, categories, budgets)
- [ ] CRUD de transações via REST API
- [ ] Conexão com PostgreSQL
- [ ] Aplicar interfaces — `TransactionRepository` com implementação Postgres

### Semana 3: Goroutines + Channels + Workers
- [ ] Worker pool pra processar transações em lote (import CSV)
- [ ] Pipeline com channels: ler → validar → salvar → notificar
- [ ] Cálculo de relatórios em paralelo com goroutines

### Semana 4: Kafka + Eventos Assíncronos
- [ ] Publicar evento no Kafka ao criar transação
- [ ] Consumer que atualiza cache no Redis
- [ ] Consumer que verifica orçamento e gera alertas

### Semana 5: Redis + Cache + gRPC
- [ ] Cache de saldo atual, gastos do mês, categorias mais usadas
- [ ] Invalidação de cache via eventos do Kafka
- [ ] Serviço gRPC interno de relatórios

### Semana 6: GraphQL
- [ ] Endpoint GraphQL pra consultas flexíveis
- [ ] Queries aninhadas: usuário → transações → categoria → resumo

### Semana 7: AWS Lambda + Automações
- [ ] Lambda de relatório mensal (todo dia 1º)
- [ ] Lambda de checagem de orçamento com alertas

### Semana 8: Polish + Patterns Avançados
- [ ] Maps pra roteamento dinâmico e strategy pattern
- [ ] Categorização automática de transações
- [ ] Testes nos fluxos críticos
- [ ] Docker Compose pra subir tudo local

---

## 🚀 Como Rodar

```bash
# Clone o repositório
git clone https://github.com/thomasaqx/FinTrack.git
cd FinTrack

# Suba a infraestrutura
docker-compose up -d

# Rode a API
go run cmd/api/main.go
```

---

## 📝 Licença

MIT
