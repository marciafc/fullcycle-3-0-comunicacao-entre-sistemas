# GraphQL

## Aula 1

  - [Código-fonte](https://github.com/devfullcycle/goexpert/tree/main/13-GraphQL) 
  
  - [Código-fonte - fork](https://github.com/marciafc/goexpert/tree/main/13-GraphQL) 
  
## Aula 2 - Introdução ao GraphQL

  - BFF

## Aula 3- Gerando esqueleto do servidor GraphQL

  - [gqlgen](https://gqlgen.com/) -> gera esqueleto
  
  - [github graphiql](https://github.com/graphql/graphiql)
  
  
## Aula 4 - Criando Schema GraphQL  
  
  - Deletar todo conteúdo do arquivo 'graph\schema.graphqls' gerado pela ferramenta gqlgen
  
    - Criar Category e Course neste arquivo
  
  - commit hash 1ed8e1975033a1226ffca534bbdefb642a8fab92 

## Aula 5 - Gerando esqueleto de nossa aplicação

  - Após definir e gerar schema em 'graph\schema.graphqls' (realizado na aula 4), rodar comando:

```
go run github.com/99designs/gqlgen generate
```
  
  - Subir a app:
```  
go run cmd/server/server.go
```

  - Acessar no navegador: [http://localhost:8080/](http://localhost:8080/)

    - Consulta: ainda vai dar erro porque falta implementação
  
```
query queryCategories {
  categories {
    id
    name    
    description
  }
}
```

  - Response

```
{
  "errors": [
    {
      "message": "internal system error",
      "path": [
        "courses"
      ]
    }
  ],
  "data": null
}
```
  - commit hash fbeabddfc0a374767b85a0d684b12b57a3ad1cfc

## Aula 6 - Criando resolver para Category

  - Alterar graph/**schema.resolvers.go**    
    - commit hash faf709cc65f6d126aa297adbc33c698d1f4ace74

  - commit hash e6cd17e7dcf7a43892e2359c99449fba83ffe074
  
    - Injetar a dependência da CategoryDB no Resolver em **resolver.go**  
	
    - Arquivo internal/database/**category.go**
  

## Aula 7 - Persistindo Category via Playground

  - Baixar as dependências: ``` $ go mod tidy ```

  - Alterar server.go
  
    - Desenvolver parte do acesso ao BD  
    - Incluir o driver do sqlite nos imports -> ```_ "github.com/mattn/go-sqlite3"```
	- Baixar as dependências: ``` $ go mod tidy ```

  - Rodar app ``` go run cmd/server/server.go ```
  
  - localhost:8080
  
  - Chamada para inserir category:

```
mutation createCategory {
  createCategory(input: {name: "Tecnologia", description: "Cursos de Tecnologia"}) {
   id
   name
   description  
  }
}
```  
  
  - commit hash	2b0ce9ac34fb83cea93b42c8ed93ecd5c8beb0ec
 

## Aula 8 - Fazendo queries de Category

  - internal/database/**category.go**
  
  - schema.resolvers.go
  
  - go run cmd/server/server.go
  
  - http://localhost:8080
  
  - Chamada para listar categories:

```  
query queryCategories {
  categories {
    id
    name    
    description
  }
}  

```

- commit hash 16f085a13fc25921a86bed151fb00e1254a77e03
  
## Aula 9 - Implementando CourseDB

  - internal/database/course.go
  
  - commit hash deef20d33295e4173c81710ce102c31e169c1d1d

## Aula 10 - Criando resolver de CreateCourse

  - Injetar a dependência da CourseDB no Resolver em **resolver.go**
  
  - schema.resolvers.go    
  
  - server.go
  
  - Subir a app ```$ go run cmd/server/server.go```
  
  - Chamada para inserir course:

```
mutation createCourse {
  createCourse(input: {name: "Full Cyclle", description: "The best", categoryId: "d3e21990-5430-4550-8c38-3a81630d3b53"}) {
   id
   name
  }
}  
```

  - commit hash c31d70c4566733723acfc5fb84773d976d2bbb2e

## Aula 11 - Implementando QueryCourses

  - schema.resolvers.go
  
  - Subir a app ```$ go run cmd/server/server.go```
  
  - Chamada para listar courses:

```
query queryCourses {
  courses {
    id 
    name
  }
}
```  
  
  - commit hash 75ce818f415c182240796910b92f6884c687abe5
  
## Aula 12 - Dados encadeados

  - Nested informations
  
  - Separação dos structs em 'models_gen.go' para model específicos
    - ```type Course struct``` PARA graph/model/course.go
    - ```type Category struct``` PARA graph/model/category.go
  
  - Organizar no gqlgen.yml os model

  - Executar o generate novamente: ```$ go run github.com/99designs/gqlgen generate```
  
  - internal/database/course.go  
  
  - Implementar no 'schema.resolvers.go' o método Courses que é resolver de category -> categoryResolver
  
  - Subir a app ```$ go run cmd/server/server.go```
  
  - Chamada para listar as categorias com os respectivos cursos

```  
query queryCategoriesWithCourses {
  categories {
    id
    name    
    description
    courses {
      id
      name      
      description
    }
  }
}

```

  - commit hash c915006ccb0c10638dc1ff7830450f46419d5fbd

## Aula 13 - Finalizando encadeamento de categorias

  - model\course.go -> remover referência para Category

  - Executar o generate novamente ```$ go run github.com/99designs/gqlgen generate```

  - Implmentar no 'schema.resolvers.go' o método Category que é resolver de course -> courseResolver

  - internal/database/category.go  
  
  - Subir a app ```$ go run cmd/server/server.go```
  
  - Chamada para listar os cursos com a respectiva categoria

```  
query queryCoursesWithCategory {
  courses {
    id 
    name
    category{
      id
      name      
      description            
    }
  }
}
```   
  - commit hash 47ef13eb602819a7661d0aacf2aef58af32206db

## Aula 14 

  - [gqlgen](https://gqlgen.com/)