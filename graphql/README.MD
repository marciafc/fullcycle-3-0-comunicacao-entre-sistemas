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

## Aula 10 - Criando resolver de CreateCourse

  - schema.resolvers.go
  
```
func (r *mutationResolver) CreateCourse(ctx context.Context, input model.NewCourse) (*model.Course, error)
```
  - Injetar a dependência da CourseDB no Resolver em **resolver.go**
  
```  
type Resolver struct{
	CategoryDB *database.Category	
	CourseDB *database.Course
}
```  

  - server.go
```  
courseDb := database.NewCourse(db)

// ...

// Injetar no resolver de CourseDB
srv := handler.NewDefaultServer(generated.NewExecutableSchema(generated.Config{Resolvers: &graph.Resolver{
		CategoryDB: categoryDb,
		CourseDB:   courseDb,
	}}))


```  

- Criar tabela de courses

```  
sqlite> create table courses (id string, name string, description string, category_id string);
```  

## Aula 11 - Implementando QueryCourses

  - schema.resolvers.go
  
```
func (r *categoryResolver) Courses(ctx context.Context, obj *model.Category) ([]*model.Course, error) 
```

## Aula 12 - Dados encadeados

  - Nested informations
  
  - Separação dos structs em 'models_gen.go' para model específicos
    - ```type Course struct``` PARA graph/model/course.go
    - ```type Category struct``` PARA graph/model/category.go
  
  - Organizar no gqlgen.yml os model
  
```
models:
  Category:
    model:
      - github.com/marciafc/graphql/graph/model.Category
  Course:
    model:
      - github.com/marciafc/graphql/graph/graph/model.Course
```

  - Executar o generate novamente
  
```
$ go run github.com/99designs/gqlgen generate
```
  - Implmentar no 'schema.resolvers.go' o método Courses que é resolver de category -> categoryResolver
  
```  
func (r *categoryResolver) Courses(ctx context.Context, obj *model.Category) ([]*model.Course, error)
```

  - internal/database/course.go  
```  
func (c *Course) FindByCategoryID(categoryID string) ([]Course, error)   
``` 

## Aula 13 - Finalizando encadeamento de categorias

  - model\course.go -> remover referência para Category

  - Executar o generate novamente
  
```
$ go run github.com/99designs/gqlgen generate
```

  - Implmentar no 'schema.resolvers.go' o método Category que é resolver de course -> courseResolver
  
```  
func (r *courseResolver) Category(ctx context.Context, obj *model.Course) (*model.Category, error)
```

  - internal/database/category.go  
```  
func (c *Category) FindByCourseID(courseID string) (Category, error) 
```

## Aula 14 

  - [gqlgen](https://gqlgen.com/)