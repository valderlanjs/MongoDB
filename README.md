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


### O que são relacionamentos entre os dados

- Alguns dados precisam estar linkados a outros para que possamos manipulá-los corretamente, por exemplo, se você possuir no seu bano de dados informações que representem missões espaciais e infrmações que representam os tripulantes de missões espaciasi, é interessant que você ppossua uma forma de relacionar quais tripulantes participaram de quais missões. 

**Tipos de associações**
- one-to-one --> um para um (um tripulante para uma missão).
- one-to-many --> um para muitos. (um tripulante para muitas missões espaciais).
- many-many --> muitos para muitos(muitos tripulantes para muitas missões).

**EXEMPLO:**
    - Imgine que você possui um conjunto de naves espacias e que cada uma delas possua tripulantes, como você representaria isso no banco de dados?

 - Utilizando o conceito de **documentos embutidos**.

- Todos os dados são englobados dentro o mesmo documento incluindo sub documentos.

        {
            "_id": "52ffc33cd584561d423410001",
            "nave": "apollo",
            "agencia": "nasa",
            "tripulantes": [
                { "nome": "Willian X" },
                { "nome": "Mark Y" }
            ]
        },
        {
            "_id": "45452114ddgc5ccc5csc10001",
            "nave": "Sputnik 1",
            "agencia": "Roskosmos",
            "tripulantes": [
                { "nome": "Mary J" },
                { "nome": "Josep K" }
            ]
        }

Nesse exeplo nós temos a nave um sendo um docuemnto e nave 2 sendo outro documento, além de subdocumentos, como os tripulantes.

**Possíveis problemas**
    - O que aconteceria se precisarmos atualizar um tripulante em comum?
    - O que aconteceria se tivessemos milhares de tripulantes?

**Quando usar** 

- Quando queremos devolver o documento inteiro com um array simples.

- Quando sabemos que o documento não vai atingir um tamanho muito grande(como uma nave com milhares de tripulantes).

- Quando os dados a serem associados só são úteis junto com o documento que queremos associar.

**Referencia**

- Um documento pode referenciar outros documentos em outras cellections através do seu ID.


<h1>Operadores do MongoDB</h1>

<h2>Introdução aos operadores</h2>

<p>Entender melhor o que são operadores e por que eles são importantes no MongoDB.</p>

<p>Operadores são ferramentas extras que nos permitem fazer queries mais complexas e poderosas no banco de dados MongoDB. Eles facilitam muito a nossa vida, trazendo mais recursos para filtrar, combinar e processar dados nas nossas consultas.</p>

<p>Alguns dos principais operadores:</p>

<h2>Operador $and</h2>
<p>O operador <code>$and</code> permite combinar filtros na query, fazendo uma interseção lógica &quot;E&quot; entre eles. Ou seja, os documentos precisam satisfazer <strong>todas</strong> as condições para serem retornados.</p>
<p>Por exemplo, se quisermos documentos onde o campo <code>name</code> contenha &quot;preparar&quot; E o campo <code>done</code> seja <code>false</code>:</p>
<pre><code>db.tasks.find({  $and: [    {name: /preparar/},     {done: false}  ]})</code></pre><p>Isso retornaria apenas os documentos que satisfazem ambos os filtros.</p>
<p>O <code>$and</code> aceita um array com diversos filtros dentro. O documento precisa bater com <strong>todos</strong> eles para ser considerado um match.</p>

<h2>Operador $or</h2>
<p>O operador <code>$or</code> funciona de forma parecida com o <code>$and</code>, mas faz uma comparação lógica &quot;OU&quot; entre os filtros. Ou seja, o documento só precisa bater com <strong>pelo menos um</strong> dos filtros para ser considerado um match e ser retornado.</p>
<p>Exemplo:</p>
<pre><code>db.tasks.find({  $or: [    {name: /preparar/},    {done: true}   ]})</code></pre>
<p>Isso retornaria documentos onde o campo <code>name</code> contém &quot;preparar&quot; OU o campo <code>done</code> é <code>true</code>. Precisa bater apenas uma das condições.</p>

<h2>Operador $exists</h2>
<p>O operador <code>$exists</code> verifica se um campo existe no documento, independente do valor.</p>
<p>Por exemplo, para retornar documentos que possuem o campo <code>checklist</code>:</p>
<pre><code>db.tasks.find({  checklist: {$exists: true} })</code></pre>
<p>E para retornar documentos que <strong>não</strong> possuem o campo <code>checklist</code>:</p>
<pre><code>db.tasks.find({  checklist: {$exists: false}})</code></pre>
<p>Muito útil para verificar a existência ou não de campos nos documentos.</p>

<h2>Operador $type</h2>
<p>O operador <code>$type</code> filtra por tipo de dados do campo.</p>
<p>Por exemplo, para retornar apenas documentos onde o campo <code>name</code> é do tipo string:</p>
<pre><code>db.tasks.find({  name: {$type: 'string'}})</code></pre>
<p>Alguns tipos suportados:</p>
<ul>
    <li>String</li>
    <li>Integer</li>
    <li>Boolean</li>
    <li>Object</li>
    <li>Array</li>
</ul>
<p>Ótimo para garantir consistência de dados.</p>

<h2>Operadores de Comparação</h2>
<p>Há também vários operadores de comparação, como:</p>
<ul>
    <li><code>$eq</code> - Igual</li>
    <li><code>$ne</code> - Diferente</li>
    <li><code>$gt</code> - Maior que</li>
    <li><code>$gte</code> - Maior ou igual</li>
    <li><code>$lt</code> - Menor que</li>
    <li><code>$lte</code> - Menor ou igual</li>
    <li><code>$in</code> - Incluído em um array</li>
    <li><code>$nin</code> - Não incluído em um array</li>
</ul>
<p>Por exemplo:</p>
<pre><code>// Maior que 5db.tasks.find({  priority: {$gt: 5} })// Menor ou igual a 10db.tasks.find({  priority: {$lte: 10}}) // Incluído nos IDs [1, 5, 8] db.tasks.find({  _id: {$in: [1, 5, 8]}})</code></pre>
<p>Estes operadores permitem comparar valores de forma simples e direta.</p>

<h2>Operadores de Avaliação</h2>
<p>Outros operadores muito úteis são os de avaliação, que permitem avaliar campos dentro de documentos:</p>
<ul>
    <li><code>$mod</code> - Resto de uma divisão</li>
    <li><code>$regex</code> - Expressões regulares</li>
    <li><code>$text</code> - Pesquisa textual em campos indexados</li>
    <li><code>$where</code> - JavaScript customizado</li>
</ul>
<p>Por exemplo:</p>
<pre><code>// Números pares (resto 0)db.values.find({  value: {$mod: [2, 0]} })// Corresponde à expressão regular  db.tasks.find({  name: {$regex: /preparar/i} })</code></pre>
<p>Estes operadores trazem recursos avançados de pesquisa e filtragem.</p>

<h2>Encadeando operadores</h2>
<p>Uma coisa muito legal no MongoDB é que podemos encadear vários operadores para criar queries super complexas e refinadas:</p>
<pre><code>db.tasks.find({  $and: [    {done: true},    {priority: {$gte: 4}},      {assignedTo: {$exists: true}},    {      checklist: {        $elemMatch: {checked: false}        }    }  ]})</code></pre>
<p>Aqui usamos <code>$and</code>, <code>$gte</code>, <code>$exists</code> e <code>$elemMatch</code> juntos!</p>
<p>As possibilidades são infinitas. Estudar bem cada operador e aprender a combiná-los para criar queries poderosíssimas.</p>
<h2>Conclusão</h2><p>Eles trazem muitos recursos extras para realizar queries, filtros e comparações de forma simples e direta.</p>
<p>Operadores facilitam muito a nossa vida, deixando as consultas muito mais poderosas. Portanto, invister em  tempo estudando-os e praticando.</p>