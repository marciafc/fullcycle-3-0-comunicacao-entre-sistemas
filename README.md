# Comunicação entre sistemas

  - Código-fonte
  
    - [GraphQl](https://github.com/marciafc/fc-graphql)
	
	- [gRPC](https://github.com/marciafc/fc-grpc)
	
  - [REST](rest/README.MD)
  
    - Características e níveis de Maturidade
	
	- HAL: Hypermedia Application Language
	
	  - Media type ```application/hal+json``` e ```application/vnd.nome-da-api.v1+json``` (passando a versão da api)
	  
	  - ``` _links.self.href ```
	  
	  - ``` _embedded ```
	
    - Method Negotiation
	
	  - OPTIONS
	
	- Content Negotiation
	
	  - Accept
	  
	  - Content-Type
	
	- Laminas API Tools
	
  - [gRPC](grpc/README.MD)	
  
    - Conceitos, motivações para utilizar gRPC
	
	- Linguagens com suporte oficial	
	
	- HTTP/2
	
	- Protocol Buffers -> Protobuf
	
	- Proto file
	
	- Formatos de comunicação  
	
	- REST vs gRPC
	
	- Preparar ambiente de desenvolvimento
	
	- Setup do projeto
	
	- Criar protofile
	
	- Gerar arquivos de código com protoc
	
	- Criação dos serviços
	
	- Criar servidor gRPC
	
	- Client evans
	
	- [Projeto desenvolvido de server gRPC em Go](https://github.com/marciafc/grpc-go/tree/main)
	- [Projeto desenvolvido de server gRPC em Go - full, com código autogerado](https://github.com/marciafc/grpc-go/tree/full)
	
  - [GraphQL](graphql/README.MD)
  
    - [Projeto desenvolvido de server GraphQL em Go](https://github.com/marciafc/graphql-go)
	
	- type
	- input	
	- mutation
	- resolvers
	- query

  - [Service discovery e Consul](service-discovery-e-consul/README.MD)
