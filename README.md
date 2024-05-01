# O que é um Banco de Dados

- Se formos até o wikipedia, veremos que banco de dados são:
    - "Coleções organizadas de dados que se relacionam de forma a criar algum sentido (informação) e dar mais eficiência durante uma pesquisa ou estudo.

- São operados pelos **SGBDs**
    - Sistemas Gerenciadores de Banco de Dados.

- Resumidamente os Bancos de Dados hoje são sistemas onde conseguimos organizar e armazenar os nossos dados.

## Bancos Relacionais

- Os bancos relacionais possuem os dados organizados em forma de tabela.

- Toda a estrutura deve ser criada antes do armazanamento dos dados.
    - Tabelas, colunas, chaves de associação, etc.
    - Os dados são armazenados como linhas destas tabelas.

- Os dados se relacionam entre as tabelas.

- Tem maior confiabilidade e consistência dos daddos.
    - Como tem uma estrutura fixa, sabemos exatamente como os dados vão ser inseridos e se relacionar.

- A criação da estrutura e armazenamento dos dados é feito por meio de uma linguagem chamada SQL.   
    - Structured Query Language

- Exemplos de bancos de dados relacionais.
    - Postgres
    - MySQL
    - MariaDB
    - Oracle

## Bancos Não-Relacionais

- Conhecidos como bancos de dados NoSQL (Not Only SQL)
    - Como o intuito era uma nova forma de armazenamento de dados que não fosse a estrutura dos relacionais
    o correto deveria ser NoRel.

- Dentre os bancos NoSQL, temos várias forma de organização
    - **Documento**: que armazenam os dados em formato de documents(JSON, XML, etc)
    - **Chave-Valor**: armazenam os dados em formato chave-valor.

- São mais escaláveis e com melhor perfomance, mas possuem menos consistência de dados, já que não existe uam estrutura pré-definida.

- **Exemplos**
    - MongoDB (documento)
    - Redis (chave-valor)
    - DynamoDB (chave-valor)
    - Cassandra


## O que é MongoDB

- É um banco de dados orientado a documentos.
- Ele armazena documentos em formataod similar a JSON´s que não precisam ter uma estrutura previamente definida.

**Exemplo de um documento**:

        {
            "nave": "apollo",
            "agencia": "nasa",
            "data": "1969",
            "tripulantes": [
                {
                    "nome": "William X",
                    "idade": "49"
                },
                {
                    "nome": "Mark Y",
                    "idade": "39"
                }
            ]
        }

**BSON**

- O mongoDB internamente representa os documentos json em um formato chamado BSON que é uma versão binária-encodada do json para incluir alguns tipos extra de formatos de dados e para codificação e decodificação em linguagem diferentes.

**Comparando o MongoDB com um banco relacional**

        | SQL Terms/Concepts  |  MongoDB Terms/Concepts           |
        | :------------------ | :---------------------------------|
        | database            |  database                         |
        | table               |  collection                       |
        | row                 |  document or BSON document        |
        | column              |  field                            |
        | index               |  index                            |
        | table joins         |  References or embedded documents |

- Porque usar o MongoDB?
    - Sem esquema fixo.
    - Alta perfomance.
    - Alta disponibilidade.
    - Fácil escalabilidade.