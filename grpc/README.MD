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

  - RPC - Remove Procedure Call
  
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
	
  
    
	