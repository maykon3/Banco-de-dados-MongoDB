# Banco de Dados MongoDB

<h1>Atividade Banco de dados Oscar</h1>

<h2>Nessa atividade utilizamos as pesquisas no banco de dados MongoDB</h2>

<h3>1- Quantas vezes Natalie Portman foi indicada ao Oscar?</h3>
R: 3
<br><br> 
Query: <pre>db.indicados.countDocuments({ nome_do_indicado: /Natalie Portman/i })</pre>

<h3>2- Quantos Oscars Natalie Portman ganhou?</h3>
R: 1
<br><br> 
Query: 
<pre>db.indicados.countDocuments({ nome_do_indicado: /Natalie Portman/i , vencedor: "true" })</pre>

<h3>3- Amy Adams já ganhou algum Oscar?</h3>
R: Não 
<br><br> 
Query: 
<pre>db.indicados.find({ nome_do_indicado: /Amy Adams/i , vencedor: "true" })</pre>

<h3>4- A série de filmes Toy Story ganhou um Oscar em quais anos?</h3>
R: Toy Story 3: 2011(2), Toy Story 4: 2020(1) 
<br><br> 
Query: 
<pre>db.indicados.find({nome_do_filme: /Toy Story/i, vencedor: "1" })</pre>

<h3>5- A partir de que ano a categoria "Actress" deixa de existir?</h3>
R: 1976  
<br><br> 
Query: 
<pre>db["indicados"].find({categoria: "ACTRESS"}).sort({cerimonia: -1})</pre>

<h3>6- O primeiro Oscar para melhor Atriz foi para quem? Em que ano?</h3>
R: "Janet Gaynor", 1928 
<br><br> 
Query: 
<pre>db.indicados.find({categoria: "ACTRESS", vencedor: "1"})</pre>

<h3>7- Na campo "Vencedor", altere todos os valores com "Sim" para 1 e todos os valores "Não" para 0.</h3>
<br><br> 
Query: 
<pre>
db.indicados.updateMany({
    vencedor: 'true'},{ 
    $set: { vencedor: "1"}
}) // para mudança do "true"
db.indicados.updateMany({
    vencedor: 'false'},{ 
    $set: { vencedor: "0"}
}) // para mudança do "false"
</pre>

<h3>8- Em qual edição do Oscar "Crash" concorreu ao Oscar?</h3>
R: 2006  
Query: 
<pre>db.indicados.find({ nome_do_filme: "Crash" })</pre>

<h3>9- Bom... dê um Oscar para um filme que merece muito, mas não ganhou.</h3>
R: Filme: Taxi Driver 
- Categoria: 'BEST PICTURE'  
- Nome do indicado: 'Michael Phillips and Julia Phillips, Producers'  
- Nome do filme: 'Taxi Driver'  
- Vencedor: '1' 
<br><br> 
Query: 
<pre>db.indicados.updateMany({nome_do_filme: "Taxi Driver", categoria: 'BEST PICTURE'},{$set: {vencedor: "1"}})</pre>

<h3>10- O filme Central do Brasil aparece no Oscar?</h3>
R: Sim  
<br><br> 
Query: 
<pre>db.indicados.find({nome_do_filme: "Central Station"})</pre>

<h3>11- Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser.</h3>
<br><br> 
Query: 
<pre>
db.indicados.insertMany([
    {
        'id_registro': 21092024,
        'ano_filmagem': 2003,
        'ano_cerimonia': 2004,
        'cerimonia': 76,
        'categoria': 'FILME PROA',
        'nome_do_indicado': 'Christina Milian',
        'nome_do_filme': 'Love Dont Cost a Thing',
        'vencedor': '1'
    }, 
    {
        'id_registro': 21092024,
        'ano_filmagem': 2024,
        'ano_cerimonia': 2025,
        'cerimonia': 97,
        'categoria': 'FILME PROA',
        'nome_do_indicado': 'Ryan Reynolds',
        'nome_do_filme': 'Deadpool & Wolverine',
        'vencedor': '1'
    },
    {
        'id_registro': 21092024,
        'ano_filmagem': 2004,
        'ano_cerimonia': 2005,
        'cerimonia': 77,
        'categoria': 'FILME PROA',
        'nome_do_indicado': 'Wesley Snipes',
        'nome_do_filme': 'Blade Trinity',
        'vencedor': '1'
    }
])
</pre>

<h3>14 - Pensando no ano em que você nasceu: Qual foi o Oscar de melhor filme, Melhor Atriz e Melhor Diretor?</h3>
R:  
- Categoria: 'BEST PICTURE' = 'A Beautiful Mind'  
- Categoria: 'DIRECTING' = 'A Beautiful Mind'  
- Categoria: 'ACTRESS IN A LEADING ROLE' = 'Monster's Ball'
<br><br> 
Query: 
<pre>db.indicados.find({ ano_cerimonia: 2002 , vencedor: "1" , categoria: { $in: [/BEST/i, /Actress/i, "DIRECTING"] }})</pre>
