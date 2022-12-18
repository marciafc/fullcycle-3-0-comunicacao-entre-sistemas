# Service discovery e Consul

## Aula 1 - Código-fonte
  
    - [Consul Example - Github](https://github.com/marciafc/consul-example)
	
## Aula 2 - Introdução ao capítulo

  - Service Discovery 
  
  - Consul (HashiCorp)
  
## Aula 3 - Entendendo o contexto

  - Service Discovery 
  
    - qual máquina, qual IP de cada instância, qual porta, permissão de acesso, saber se instância está saudável
	
	- descobre quais máq estão disponíveis para acesso
	
	- segmentação de máquinas para garantir segurança
	
	- resolução via DNS
	
	- health check ativo
	
	  - desregistra máquinas que não estão saudáveis
	  
    - garantir permissão de acesso
	
## Aula 4 - Visão geral do Consul

  - HashiCorp Consul
  
    - Service Discovery 
	
	- agnóstico a linguagem de aplicação
	
	- Service Segmentation
	
	- Load Balancer na borda (layer 7)
	
	- Key / value Configuration (variável de ambiente, de configuração de BD, etc)
	
	- Opensource / Enterprise
	
	- Recursos na parte de segurança
	
	
## Aula 5 - Service registry

  - Consul server - sabe todos serviços que estão rodando
  
  - Consul local - o health check roda e Consul local envia dados da saúde da app para o Consul server
  
  - Gossip protocol - comunicação sobre serviços para saber quem está de pé
  
  - Consul tem um servidor de DNS próprio
  
  - Consul tem API para consultar e obter infos do registry
  
## Aula 6 - Health check e Multicloud

  - Health check ativo -> agent, client do Consul verifica se instância está saudável, senao estiver, avisa o Consul server e o Consul server tira do registry caso a instância esteja fora do ar
  
  - Multi-região e multi-cloud
  
  
## Aula 7 - Agent, Client e Server

  - agent: processo, pode ser client ou server
  
  - client: registra os serviços localmente
  
    - roda health check 
	
	- encaminha as infos e configurações dos serviços para server
	
  - server: mantém estado do cluster, stateless, registra os serviços
  
    - membership (quem é client e quem é server)
	
	- vários server, inclusive o líder
	
	- retorno de queries (DNS ou API)
	
	- troca as infos entre datacenters
	
  - dev mode
  
    - simula os servers do Consul
	
	- roda como server
	
	- nao escala
	
	- registra tudo em memória
	
	- não usar em prod
  
## Aula 8 - Iniciando um agente consul

  - Consul é também uma ferramenta de service mesh
  
  - 

	