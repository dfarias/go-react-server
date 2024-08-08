# Criar arquivo de modulos do go
go mod init github.com/dfarias/go-react-server

# instalar modulo
go install github.com/jackc/tern/v2@latest

# configuar arquivo de migracao de banco
tern ./internal/store/pgstore/migrations

# criar arquivo para criacao das tabelas
term new --migrations ./internal/store/pgstore/migrations create_rooms_table

# Importar as dependencias no arquivo go.mod
go mod tidy

# Executar no terminal
go run cmd/tools/terndotenv/main.go

# Subir banco e ferramenta
docker compose start
go run cmd/tools/terndotenv/main.go

# sqlc - gerador de codigo

## Instalar
go install github.com/sqlc-dev/sqlc/cmd/sqlc@latest

## Generate
sqlc generate -f ./internal/store/pgstore/sqlc.yaml

## Gerando codigo das queries
go generate ./...



