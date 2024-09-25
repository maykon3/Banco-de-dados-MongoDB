Momento
Contém a base de indicados da empresa Momento para treinar consultas complexas no MongoDB.
 Vamos fazer algumas perguntas para brincar de análise exploratória de dados com MongoDB.

* Quantos funcionarios da empresa Momento trabalham no departamento de vendas?
<pre>R: 10
Query:db.funcionarios.countDocuments({cargo: /Vendas/i})</pre>

* Inclua suas próprias informações no departamento de Tecnologia da empresa.
Query: <pre>db.funcionarios.insertOne({
            "nome": "Maykon Silva",
            "telefone": "(11)999999999",
            "email": "a@b.com.proa",
            "dataAdmissao": "2002-12-09",
            "cargo": "Web Developer",
            "salario": 4800,
            "departamento": ObjectId("85992103f9b3e0b3b3c1fe74")
            })</pre>

* Agora diga, quantos funcionários temos ao total na empresa?

<pre>R: 24
Query: db.funcionarios.countDocuments()</pre>

* E quanto ao Departamento de Tecnologia?

<pre>R: 6
Query: db.funcionarios.countDocuments({departamento: ObjectId("85992103f9b3e0b3b3c1fe74")})</pre>

* Qual a média salarial do departamento de tecnologia?

<pre>R: media = 4600 somaSalarios = 27600
Query: db.funcionarios.aggregate([
  {$match: {departamento: ObjectId("85992103f9b3e0b3b3c1fe74")}},
  {
    $group: {
      _id: null,
      totalSalarios: { $sum: "$salario" },
      totalFuncionarios: { $sum: 1 }
    }
  },
  {
    $project: {
      _id: 0,
      totalSalarios: 1,
      mediaSalarial: { $divide: ["$totalSalarios", "$totalFuncionarios"] },
    }
  }
]);</pre>

* Quanto o departamento de Vendas gasta em salários?

<pre>R: totalSalarios = 95100
Query:db.funcionarios.aggregate([
  {$match: {cargo: /Vendas/i}},
  {
    $group: {
      _id: null,
      totalSalarios: { $sum: "$salario" },
    }
  }
]);</pre> 

* Um novo departamento foi criado. O departamento de Inovações. Ele será locado no Brasil. Por favor,adicione-o no banco de dados da empresa colocando quaisquer informações que você achar relevantes.

<pre>Query:  db.departamentos.insertOne({
nome: "Inovacoes",
escritorio: ObjectId("5f8b3f3f9b3e0b3b3c1e3e3e")
})

* localização do escritorio 
Query: db.escritorios.insertOne({
  "_id": ObjectId("66f2d8d398cd410d23187eab"),
  "nome": "Aorp Industries",
  "endereco": "Central Station, Morro do Jacarézinho, Rio de Janiero, 100",
  "telefone": "+55 21 99999-9999",
  "pais": "BRA",
  "suprimentos": [
    {
      "produto": "Airsoft (unitário)",
      "quantidade": 143,
      "precoUnitario": 200
    },
    {
      "produto": "Cardeneta",
      "quantidade": 50,
      "precoUnitario": 752.85
    },
    {
      "produto": "Computadores",
      "quantidade": 29,
      "precoUnitario": 8000
    },
    {
      "produto": "Post-its",
      "quantidade": 50,
      "precoUnitario": 1000
    }
  ]
})</pre>


* O departamento de Inovações está sem funcionários. Inclua alguns colegas de turma nesse departamento.
<pre>Query: db.funcionarios.insertMany([
{
            "nome": "Mateus Oliveira",
            "telefone": "11 98080-8080",
            "email": "a@b.proa.br",
            "dataAdmissao": "2010-05-03",
            "cargo": "Web Developer",
            "salario": 3500,
            "departamento": ObjectId("66f2d3bc98cd410d23187eaa"),
        },{
            "nome": "Hudson de Souza",
            "telefone": "11 97070-7070",
            "email": "b@a.proa.br",
            "dataAdmissao": "2008-12-03",
            "cargo": "Web Developer",
            "salario": 4500,
            "departamento": ObjectId("66f2d3bc98cd410d23187eaa"),
        },{
            "nome": "Murilo Coelho",
            "telefone": "11 96060-6060",
            "email": "ab@cd.proa.br",
            "dataAdmissao": "2012-01-03",
            "cargo": "Web Developer",
            "salario": 3500,
            "departamento": ObjectId("66f2d3bc98cd410d23187eaa"),
        },{
            "nome": "Andressa Scrum",
            "telefone": "11 94040-4040",
            "email": "fe@hg.proa.br",
            "dataAdmissao": "2015-01-12",
            "cargo": "Web Developer",
            "salario": 4500,
            "departamento": ObjectId("66f2d3bc98cd410d23187eaa"),
        }
]);</pre>

* Quantos funcionarios a empresa Momento tem agora?
<pre>R: 28
Query: db.funcionarios.countDocuments()</pre>

* Quantos funcionários da empresa Momento possuem conjuges?

* Qual a média salarial dos funcionários da empresa Momento, excluindo-se o CEO?

* Qual a média salarial do departamento de tecnologia?

* Qual o departamento com a maior média salarial?

* Qual o departamento com o menor número de funcionários?

* Pensando na relação quantidade e valor unitario, qual o produto mais valioso da empresa?

* Qual o produto mais vendido da empresa?

* Qual o produto menos vendido da empresa?