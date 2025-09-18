🚀 Caso de Estudo NoSQL - Amazonas E-commerce

## Integrantes do Grupo
- Gabriel Morais Simonini Sussmann, Bruno Boggio, Nelson Reis e Denis Varela

## Decisões de Arquitetura

### Estrutura de Collections

Optamos por **três collections separadas** para otimizar as consultas e manter a flexibilidade:

1. **customers** - Dados dos clientes
2. **products** - Catálogo de produtos
3. **events** - Eventos de cliques e compras

### Justificativas das Decisões

#### 1. Por que Collections Separadas?

**Customers Collection:**
- Dados relativamente estáveis dos clientes
- Facilita consultas específicas sobre clientes
- Permite normalização de dados geográficos (estado)

**Products Collection:**
- Catálogo de produtos com informações específicas por categoria
- Estrutura flexível para diferentes tipos de produtos (livros, CDs, eletrodomésticos)
- Facilita manutenção do catálogo

**Events Collection:**
- Armazena tanto cliques quanto compras
- Estrutura otimizada para análises temporais
- Permite rastreamento detalhado do comportamento do usuário

### Vantagens da Abordagem

1. **Escalabilidade:** Collections separadas permitem indexação e sharding independentes
2. **Flexibilidade:** Fácil adição de novos tipos de produtos
3. **Performance:** Consultas otimizadas para cada tipo de dados
4. **Manutenibilidade:** Estrutura clara e organizada

### Consulta escolhida
- Valor médio de vendas por estado(visitar arquivo command_mongo.sh)

### Passo a passo VSCode

- Para construir a imagem, navegue para a pasta impacta-labs/nosql-databases/mongodb e execute o seguinte comando:
docker build -t case_mongodb .

- Para iniciar o container, execute o seguinte comando:
docker run -d -p 27017:27017 --name mongodb_case case_mongodb

- Importando os Documentos
- Copie o arquivo para o docker dentro da pasta mongodb/
docker cp customers.json mongodb_case:/customers.json
docker cp events.json mongodb_case:/events.json
docker cp products.json mongodb_case:/products.json

- Importe o arquivo
docker exec -it mongodb_case mongoimport --db test --collection customers --file /customers.json --type json --legacy
docker exec -it mongodb_case mongoimport --db test --collection events --file /events.json --type json --legacy
docker exec -it mongodb_case mongoimport --db test --collection products --file /products.json --type json --legacy


- Acesse o mongosh(docker exec -it mongodb_case mongosh) e excute a query do arquivo command_mongo.sh

