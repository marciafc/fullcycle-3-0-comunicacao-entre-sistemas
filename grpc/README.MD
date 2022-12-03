# gRPC

## Aula 1 - Iniciando com gRPC

## Aula 2 - Código-fonte
  
  - [goexpert/14-gRPC](https://github.com/marciafc/goexpert/tree/main/14-gRPC)
  
    - Fork deste repo: [goexpert/14-gRPC](https://github.com/devfullcycle/goexpert/tree/main/14-gRPC)
	
## Aula 3 - Conceitos iniciais

  - framework, comunicação entre sistemas, rápido, leve e independente de linguagem
  
  - ideal para microsserviços
  
  - mobile, browsers e backend
  
  - geração automática de código
  
  - streaming bidirecional com HTTP/2 (trafega binário, comunicação bidirecional)
  
    - HTTP1.1 -> 1 request e 1 response
	
	- HTTP/2 -> mantém 1 request, manter o canal de comunicação atualizado (aberto) e receber diversas responses OU enviar diversas requests em uma única conexão
	
  - Linguagens com suporte oficial	
  
    - gRPC-GO
	- gRPC-JAVA
	- gRPC-C
	  - C++
	  - Python
	  - Ruby
	  - Objective C
	  - PHP
	  - C#
	  - Node.js
	  - Dart
	  - Kotlin / JVM
  
## Aula 4 - gRPC HTTP2 e Protocol Buffers

  - RPC - Remote Procedure Call
  
  - gRPC trafega através do protocolo HTTP/2
  
  - Protocol Buffers
  
    - linguagem neutra com mecanismos de extensibilidade e serialização de dados estruturados
	
	- como um XML, mas muito menor, muito mais rápido e muito mais simples
	
	- formato binário (mais rápido, mas precisa serializar e deserializar)
	
	- precisa de um contrato, um schema
	
  - Protocol Buffers Vs JSON
  
    - Arquivos binários < JSON
	
	- Processo de serializar é mais leve (CPU) do que em JSON, menos recurso de rede, mais rápido
  	
  - Protobuf -> sigla de Protocol buffers
  
  - Proto file - arquivo de schema do Protocol Buffers
  
  - HTTP/2
  
    - nome original SPDY
	
	- dados trafegados são binários e não texto (HTTP 1.1)
	
	- utiliza mesma conexão TCP para enviar e receber dados do cliente e do servidor -> Multiplex
	
	- server push
	
	- headers são comprimidos
	
	- gasta menos recursos de rede
	
	- processo mais rápido
	
  
# Aula 5 - Formatos de comunicação    

  - API "unary" 
    - 1 request, 1 response
	
  - API "Server streaming"	
    - 1 request, várias responses
	
  - API "client streaming"  
    - várias requests, 1 response
	
  - API "Bi directional streaming"  
    - várias requests, várias responses
	
	
## Aula 6 - REST vs gRPC

  - REST: 
    - texto / JSON
	- unidirecional
	- alta latência
	- sem contrato rígido (aumenta chances de erros) - pode enviar um número no formato de String
	- não tem suporte a streaming ->  1 request e 1 response
	- precisa ter design pré-definido -> padrão de URL, CRUD
	- bibliotecas de terceiros - depende de implementação para ler http
	
  - gRPC
    - Protocol Buffers
	- bidirecional e assíncrono
	- baixa latência
	- Proto files - contrato bem definido (.proto)
	- suporte a streaming
	- design livre - uma única chamada pode fazer diversas coisas
	- geração de código - evita menos erros, bibliotecas nativas
	
## Aula 7 - gRPC vs Protocol Buffers	

  - gRPC -> [https://grpc.io](https://grpc.io/)
  
    - Quick start gRPC -> [https://grpc.io/docs/languages/go/quickstart/](https://grpc.io/docs/languages/go/quickstart/)
  
  - Protocol Buffers -> [https://developers.google.com/protocol-buffers](https://developers.google.com/protocol-buffers)
  
    - Guide proto3 -> [https://developers.google.com/protocol-buffers/docs/proto3](https://developers.google.com/protocol-buffers/docs/proto3)
      - gRPC com proto3
	
    - Style Guide -> [https://developers.google.com/protocol-buffers/docs/style](https://developers.google.com/protocol-buffers/docs/style)	
  
  
## Aula 8 - Instalando compilador e plugins 

  - Instalação para trabalhar com gRPC em Go ->  [https://grpc.io/docs/languages/go/quickstart/](https://grpc.io/docs/languages/go/quickstart/). Basicamente 3 passos:
  
  - (1) Instalar Go -> [Download and install](https://go.dev/doc/install)
  
  - (2) Instalar [protoc](https://grpc.io/docs/protoc-installation/) -> compilador do protocol buffer
  
    - $ protoc --version 
	
	  - Versão tem que ser maior que 3
  
  - (3) [Plugins](https://grpc.io/docs/languages/go/quickstart/)

    - protoc-gen-go -> gera as entidades / mensagens
  
    - protoc-gen-go-grpc -> gera as interfaces de comunicação usando gRPC
  
## Aula 9 - Fazendo setup do projeto  
  
```  
$ mkdir GRPC-GO
$ cd GRPC-GO

$ go mod init github.com/marciafc/14-gRPC

Criar estrutura internal/database e dentro dois files: category.go e course.go

$ go mod tidy

```

## Aula 10 - Criando nosso protofile

  - Instalar extensão do VS Code -> vscode-proto3 - zxh404.vscode-proto3

  - Criar pasta proto, file course_category.proto
  
## Aula 11 - Fazendo geração de código com protoc

  - [protoc-gen-go: unable to determine Go import path for...](https://stackoverflow.com/questions/70586511/protoc-gen-go-unable-to-determine-go-import-path-for-simple-proto)


```
$ protoc --go_out=. --go-grpc_out=. proto/course_category.proto

// Agora temos a pasta 'pb' em 'internal' e esses dois arquivos 'course_category_grpc.pb.go' e 'course_category.pb.go'

// Baixar os pacotes
$ go mod tidy


```

## Aula 12 - Implementando CreateCategory

  - Na pasta 'internal' criar pasta 'service' e dentro file category.go


## Aula 13 - Criando servidor gRPC

  - criar estrutura 'cmd/grpcServer' e dentro arquivo main.go
  
```

grpcServer := grpc.NewServer()
pb.RegisterCategoryServiceServer(grpcServer, categoryService)

reflection.Register(grpcServer)

lis, err := net.Listen("tcp", ":50051")
if err != nil {
	panic(err)
}

if err := grpcServer.Serve(lis); err != nil {
	panic(err)
}

```
  
## Aula 14 - Interagindo com evans

  - [evans](https://github.com/ktr0731/evans)
  
```  

// Versão corrente do Go
$ go version

  go version go1.19.3 linux/amd64

=====================

// Instalar evans a partir da versão do Go 1.16
$ go install github.com/ktr0731/evans@latest  

=====================

// No projeto Go
$ go run cmd/grpcServer/main.go 

=====================

// Baixar o go-sqlite3 -> foi incluso nos imports do main.go isso "github.com/mattn/go-sqlite3"
cmd/grpcServer/main.go:13:2: no required module provides package github.com/mattn/go-sqlite3; to add it: go get github.com/mattn/go-sqlite3
    		
// Baixar os pacotes
$ go mod tidy

// Rodar app Go
$ go run cmd/grpcServer/main.go 

=====================

// Em outra aba...

// Tem que estar rodar na porta 50051, ou especificar a porta via parâmetro
$ evans -r repl

  ______
 |  ____|
 | |__    __   __   __ _   _ __    ___
 |  __|   \ \ / /  / _. | | '_ \  / __|
 | |____   \ V /  | (_| | | | | | \__ \
 |______|   \_/    \__,_| |_| |_| |___/

 more expressive universal gRPC client


// Especificando serviço
pb.CategoryService@127.0.0.1:50051> service CategoryService

// Chamada gRPC
pb.CategoryService@127.0.0.1:50051> call CreateCategory
name (TYPE_STRING) => X
description (TYPE_STRING) => X

// Erro porque ainda não tem o banco de dados
command call: rpc error: code = Unknown desc = no such table: categories


=====================

// Em outra aba...

$ ls
cmd  db.sqlite  go.mod  go.sum  internal  proto


// Instalar sqlite
$ sqlite3 db.sqlite
  Command 'sqlite3' not found, but can be installed... 
$ sudo apt install sqlite3

// Acessando o sqlite
$ sqlite3 db.sqlite

// Criar tabela
sqlite> create table categories (id string, name string, description string);


=====================

// Na aba do evans, fazer a chamada: selecionar o Service e depois chamar o criar serviço que cria a categoria

pb.CategoryService@127.0.0.1:50051> service CategoryService

pb.CategoryService@127.0.0.1:50051> call CreateCategory
name (TYPE_STRING) => Cat 1
description (TYPE_STRING) => Cat 1 Desc
{
  "description": "Cat 1 Desc",
  "id": "6ff08c03-ce38-4bb5-9d3d-fecbcf2e5ba5",
  "name": "Cat 1"
}

pb.CategoryService@127.0.0.1:50051> call CreateCategory
name (TYPE_STRING) => Cat 2
description (TYPE_STRING) => Cat 2 Desc
{
  "description": "Cat 2 Desc",
  "id": "9e5c90b1-0737-48b5-b31c-62a5794b7be9",
  "name": "Cat 2"
}

```
  
## Aula 15 - Criando categoryList no protofile

  - Obter várias categorias
  
    - CategoryList em 'course_category.proto'
	
	- rpc ListCategories(blank) returns (CategoryList) {} em 'course_category.proto'
	
  - Gerar código
  
    - ```$ protoc --go_out=. --go-grpc_out=. proto/course_category.proto ```

## Aula 16 - Listando categories

  - Implementação do ListCategories (da aula 15)
  
    - database/category.go -> ```func (c *Category) FindAll() ([]Category, error) ```
	
	- service/category.go 
	  - ```func (c *CategoryService) ListCategories(ctx context.Context, in *pb.Blank) (*pb.CategoryList, error) ```

    - Rodar servidor -> ``` $ go run cmd/grpcServer/main.go ```
	
	- Abrir aba evans -> ``` $ evans -r repl ```
	
	- Chamar serviço para listar categorias
	
		```				
		pb.CategoryService@127.0.0.1:50051> call ListCategories
		{
		  "categories": [
			{
			  "description": "Cat 1 Desc",
			  "id": "6ff08c03-ce38-4bb5-9d3d-fecbcf2e5ba5",
			  "name": "Cat 1"
			},
			{
			  "description": "Cat 2 Desc",
			  "id": "9e5c90b1-0737-48b5-b31c-62a5794b7be9",
			  "name": "Cat 2"
			}
		  ]
		}
		
		```
		
## Aula 17 - Buscando uma categoria

  - Buscar uma categoria em específico
  
  
	

