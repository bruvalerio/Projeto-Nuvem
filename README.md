# Projeto Integrador – Cloud Developing 2025/1

> CRUD simples + API Gateway + Lambda /report + RDS + CI/CD

**Grupo**:


1. 10418640 - Bruna Sousa Valerio -
• Criou o backend Node.js com Express.
• Definiu as rotas REST (/filmes) e lógica de conexão com o PostgreSQL.
• Criou o Dockerfile e executou o deploy na instância EC2.
2. 10402374 - Danilo Ferreira Rocha
• Configurou o API Gateway com rotas /filmes, /filmes/{id} e /report.
• Realizou testes com curl, validou retornos HTTP.
3. 10417732 - Fernanda de Moraes Brazolin
• Criou e configurou o banco de dados no Amazon RDS.
• Criou tabela filmes e populou com dados de teste via psql.
• Garantiu que a instância ficasse em subnet privada com acesso via EC2.
4. 10419669 - Yasmin Toledo
• Criou a função Lambda em Node.js com https.get.
• Adaptou para consumir a rota /filmes e devolver as estatísticas.
• Integração da Lambda à rota /report no API Gateway.


## 1. Visão geral
O sistema é um **Catálogo de Filmes**, onde é possível:
- Listar todos os filmes (GET)
- Inserir novos filmes (POST)
- Atualizar dados de filmes existentes (PUT)
- Remover filmes (DELETE)
- Obter estatísticas com a rota `/report` via Lambda (ex: total de filmes e um exemplo aleatório)
- Escolhemos esse domínio por ser simples de entender e direto para demonstrar a integração dos serviços da AWS, mantendo o foco na arquitetura em nuvem.

## 2. Arquitetura
![Digrama](https://github.com/user-attachments/assets/23eed5b5-262c-4128-85ac-d5a05f436fdb)



| Camada | Serviço | Descrição |
|--------|---------|-----------|
| Backend | ECS Fargate (ou EC2 + Docker) | API REST Node/Spring/… |
| Banco   | Amazon RDS              | PostgreSQL / MySQL em subnet privada |
| Gateway | Amazon API Gateway      | Rotas CRUD → ECS · `/report` → Lambda |
| Função  | AWS Lambda              | Consome a API, gera estatísticas JSON |


## 3. Como rodar localmente

```bash
cp .env.example .env         # configure variáveis
docker compose up --build
# API em http://localhost:3000

````
##4. Scripts SQL


CREATE TABLE filmes (
  id SERIAL PRIMARY KEY,
  titulo TEXT NOT NULL,
  diretor TEXT NOT NULL,
  ano INT NOT NULL,
  genero TEXT NOT NULL
);
```
````
## 5. Endpoints

- `GET /filmes` - Lista todos os filmes
- `POST /filmes` - Adiciona novo filme
- `PUT /filmes/:id` - Atualiza filme existente
- `DELETE /filmes/:id` - Remove filme por ID
- `GET /report` - Função Lambda que retorna total de filmes, um exemplo e timestamp
``````
``````
## 6. Link do vídeo do Funcionamento

https://youtu.be/LXi4C88x9RI?si=YQYb1TSiWEWMZqzX 
