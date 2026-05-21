HTML
<!DOCTYPE html>
<html lang="pt-br">

<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>IC ARTES Comunicação Visual</title>

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial, Helvetica, sans-serif;
}

body{
    background:#050505;
    color:white;
    overflow:hidden;
}

.container{
    display:flex;
    height:100vh;
}

/* SIDEBAR */

.sidebar{
    width:390px;
    background:linear-gradient(180deg,#0a0a0a,#111827);
    border-right:1px solid #222;
    padding:20px;
    overflow:auto;
}

.logo h1{
    font-size:45px;
    font-weight:900;
}

.logo span{
    color:#ffd000;
}

.logo p{
    color:#aaa;
    margin-top:5px;
}

.titulo{
    margin-top:25px;
    margin-bottom:20px;
    color:#ffd000;
    font-size:28px;
    font-weight:bold;
}

.label{
    display:block;
    margin-top:15px;
    margin-bottom:8px;
    font-size:16px;
}

.sidebar input,
.sidebar textarea,
.select{
    width:100%;
    padding:14px;
    border:none;
    border-radius:12px;
    font-size:16px;
    background:#1f2937;
    color:white;
}

.sidebar textarea{
    min-height:180px;
    resize:none;
}

.btn{
    width:100%;
    padding:15px;
    border:none;
    border-radius:12px;
    margin-top:15px;
    cursor:pointer;
    font-size:17px;
    font-weight:bold;
    transition:0.2s;
}

.btn:hover{
    transform:scale(1.02);
}

.btn-add{
    background:#ffd000;
    color:black;
}

.btn-clear{
    background:#374151;
    color:white;
}

.btn-print{
    background:#0f9d58;
    color:white;
}

/* LISTA */

.lista-titulo{
    margin-top:30px;
    margin-bottom:15px;
    color:#ffd000;
    font-size:24px;
    font-weight:bold;
}

.lista{
    display:flex;
    flex-direction:column;
    gap:12px;
}

.item{
    background:#111827;
    border:1px solid #333;
    border-radius:14px;
    padding:12px;
    display:flex;
    align-items:center;
    gap:12px;
}

.thumb{
    width:70px;
    height:100px;
    background:white;
    border-radius:8px;
    overflow:hidden;
    flex-shrink:0;
}

.thumb-top{
    background:red;
    color:#ffe066;
    text-align:center;
    font-size:13px;
    font-weight:bold;
    padding:5px;
}

.thumb-preco{
    text-align:center;
    color:red;
    font-size:24px;
    font-weight:900;
    margin-top:25px;
}

.info{
    flex:1;
}

.info h3{
    font-size:18px;
    margin-bottom:5px;
}

.info p{
    color:#ffd000;
    font-size:22px;
    font-weight:bold;
}

.info span{
    color:#aaa;
    font-size:14px;
}

.acoes{
    display:flex;
    flex-direction:column;
    gap:8px;
}

.icon{
    width:38px;
    height:38px;
    background:#1f2937;
    border-radius:10px;
    display:flex;
    justify-content:center;
    align-items:center;
    cursor:pointer;
}

/* PREVIEW */

.preview{
    flex:1;
    padding:20px;
    overflow:auto;
}

.preview h2{
    color:#ffd000;
    margin-bottom:20px;
    font-size:34px;
}

.grid{
    display:flex;
    flex-wrap:wrap;
    gap:20px;
    justify-content:center;
}

/* CARTAZ */

.cartaz{
    background:white;
    position:relative;
    overflow:hidden;
    border-radius:18px;
    box-shadow:0 0 30px rgba(0,0,0,0.5);
}

/* TAMANHOS */

.a4-retrato{
    width:850px;
    height:1200px;
}

.a4-paisagem{
    width:1200px;
    height:850px;
}

.tamanho-11x15{
    width:390px;
    height:560px;
}

.tamanho-20x27{
    width:560px;
    height:780px;
}

/* TOPO */

.topo-cartaz{
    width:100%;
    height:180px;
    display:flex;
    justify-content:center;
    align-items:center;
}

.topo-cartaz h1{
    color:#ffe066;
    font-size:95px;
    font-weight:900;
}

/* PRODUTO */

.nome-produto{
    text-align:center;
    margin-top:35px;
    padding:0 20px;
    font-size:95px;
    line-height:95px;
    font-weight:900;
    color:black;
}

/* DESCRIÇÃO */

.pincel{
    width:88%;
    min-height:220px;
    margin:40px auto;
    border-radius:120px;
    display:flex;
    justify-content:center;
    align-items:center;
    text-align:center;
    padding:30px;
    font-size:85px;
    font-weight:900;
    color:black;
}

/* PREÇO */

.area-preco{
    text-align:center;
    margin-top:0;
}

.rs{
    font-size:120px;
    font-weight:bold;
    vertical-align:top;
}

.valor{
    font-size:430px;
    line-height:360px;
    font-weight:900;
}

/* RODAPÉ */

.rodape{
    width:100%;
    height:70px;
    position:absolute;
    bottom:0;
}

/* ===================================== */
/* TEMAS */
/* ===================================== */

/* PROMOÇÃO */

.tema-promocao{
    border:10px solid #d40000;
    background:white;
}

.tema-promocao .topo-cartaz,
.tema-promocao .rodape{
    background:#d40000;
}

.tema-promocao .pincel{
    background:#ffd000;
}

.tema-promocao .valor,
.tema-promocao .rs{
    color:#d40000;
}

/* CONFIRA */

.tema-confira{
    border:10px solid #004aad;
    background:#f8fbff;
}

.tema-confira .topo-cartaz,
.tema-confira .rodape{
    background:#004aad;
}

.tema-confira .pincel{
    background:#9fd3ff;
}

.tema-confira .valor,
.tema-confira .rs{
    color:#004aad;
}

/* HORTIFRUTI */

.tema-hortifruti{
    border:10px solid #0f9d58;
    background:#f5fff8;
}

.tema-hortifruti .topo-cartaz,
.tema-hortifruti .rodape{
    background:#0f9d58;
}

.tema-hortifruti .pincel{
    background:#c6ffd9;
}

.tema-hortifruti .valor,
.tema-hortifruti .rs{
    color:#0f9d58;
}

/* LIMPEZA */

.tema-limpeza{
    border:10px solid #00aaff;
    background:#f3fcff;
}

.tema-limpeza .topo-cartaz,
.tema-limpeza .rodape{
    background:#00aaff;
}

.tema-limpeza .pincel{
    background:#c8f3ff;
}

.tema-limpeza .valor,
.tema-limpeza .rs{
    color:#00aaff;
}

/* BLACK */

.tema-black{
    border:10px solid black;
    background:#111;
}

.tema-black .topo-cartaz,
.tema-black .rodape{
    background:black;
}

.tema-black .topo-cartaz h1{
    color:#ffd000;
}

.tema-black .nome-produto{
    color:white;
}

.tema-black .pincel{
    background:#ffd000;
}

.tema-black .valor,
.tema-black .rs{
    color:#ffd000;
}

/* ===================================== */
/* NOVO MODELO OFERTÃO */
/* ===================================== */

.tema-ofertao{
    border:12px solid #d91e18;
    background:#ffffff;
}

.tema-ofertao .topo-cartaz{
    background:#d91e18;
    height:220px;
    border-bottom-left-radius:50% 80px;
    border-bottom-right-radius:50% 80px;
}

.tema-ofertao .topo-cartaz h1{
    color:#ffd84d;
    font-size:120px;
    letter-spacing:5px;
}

.tema-ofertao .nome-produto{
    font-size:92px;
    line-height:90px;
    margin-top:50px;
    font-weight:900;
    font-style:italic;
    text-transform:uppercase;
}

.tema-ofertao .pincel{
    width:92%;
    min-height:170px;
    background:
    repeating-linear-gradient(
        -5deg,
        #ffd400,
        #ffd400 18px,
        #ffe95c 18px,
        #ffe95c 36px
    );
    border-radius:0;
    font-size:95px;
    font-style:italic;
    font-weight:900;
    color:black;
    transform:rotate(-2deg);
}

.tema-ofertao .rs{
    display:none;
}

.tema-ofertao .valor{
    font-size:520px;
    line-height:430px;
    color:#e1251b;
    font-weight:900;
    letter-spacing:-20px;
}

.tema-ofertao .rodape{
    background:#d91e18;
    height:90px;
    border-top-left-radius:50% 80px;
    border-top-right-radius:50% 80px;
}

.tema-ofertao .rodape::after{
    content:'IC ARTS';
    position:absolute;
    left:50%;
    top:15px;
    transform:translateX(-50%);
    color:#ffd84d;
    font-size:55px;
    font-weight:900;
}

/* MOBILE */

@media(max-width:900px){

    body{
        overflow:auto;
    }

    .container{
        flex-direction:column;
        height:auto;
    }

    .sidebar{
        width:100%;
    }

    .cartaz{
        transform:scale(0.42);
        transform-origin:top center;
        margin:-320px auto;
    }
}

/* IMPRESSÃO */

@media print{

    body{
        background:white;
    }

    .sidebar,
    .preview h2,
    .lista-titulo,
    .lista{
        display:none;
    }

    .preview{
        padding:0;
    }

    .grid{
        gap:0;
    }

    .cartaz{
        border-radius:0;
        box-shadow:none;
        page-break-inside:avoid;
    }

    .a4-retrato{
        width:100%;
        height:100vh;
    }

    .a4-paisagem{
        width:100%;
        height:100vh;
    }

    .tamanho-11x15{
        width:48%;
        height:48vh;
    }

    .tamanho-20x27{
        width:48%;
        height:100vh;
    }
}

</style>

</head>

<body>

<div class="container">

<div class="sidebar">

<div class="logo">

<h1>
IC <span>ARTES</span>
</h1>

<p>
Comunicação Visual
</p>

</div>

<div class="titulo">
GERAR CARTAZES
</div>

<label class="label">
Tema do Cartaz
</label>

<select id="tema" class="select">

<option value="promocao">
Promoção Vermelho
</option>

<option value="confira">
Confira Azul
</option>

<option value="hortifruti">
Hortifruti Verde
</option>

<option value="limpeza">
Limpeza Azul Céu
</option>

<option value="black">
Black Friday
</option>

<option value="ofertao">
Ofertão Mercado
</option>

</select>

<label class="label">
Texto do topo
</label>

<input type="text"
id="tituloTopo"
value="OFERTA">

<label class="label">
Tamanho do Cartaz
</label>

<select id="tamanho" class="select">

<option value="a4-retrato">
A4 Retrato
</option>

<option value="a4-paisagem">
A4 Paisagem
</option>

<option value="11x15">
11x15 - 4 por folha
</option>

<option value="20x27">
20x27 - 2 por folha
</option>

</select>

<label class="label">
Lista de Produtos
</label>

<textarea id="listaTexto"
placeholder="Exemplo:

COXÃO MOLE BOVINO - 35,90 - KG
ARROZ TIO JOÃO - 24,99 - 5KG
FEIJÃO KICALDO - 8,99 - 1KG

"></textarea>

<button class="btn btn-add"
onclick="importarLista()">

+ GERAR CARTAZES

</button>

<button class="btn btn-clear"
onclick="limparTudo()">

🗑 LIMPAR TUDO

</button>

<button class="btn btn-print"
onclick="window.print()">

🖨 IMPRIMIR

</button>

<div class="lista-titulo">
PRODUTOS ADICIONADOS
</div>

<div class="lista"
id="listaProdutos">

</div>

</div>

<!-- PREVIEW -->

<div class="preview">

<h2>
PRÉ-VISUALIZAÇÃO
</h2>

<div class="grid"
id="todosCartazes">

</div>

</div>

</div>

<script>

let produtos = []

function importarLista(){

    let texto =
    document.getElementById('listaTexto').value

    let tema =
    document.getElementById('tema').value

    let tamanho =
    document.getElementById('tamanho').value

    let tituloTopo =
    document.getElementById('tituloTopo').value

    if(texto.trim() == ''){

        alert('Digite a lista de produtos')
        return
    }

    let linhas =
    texto.split('\n')

    linhas.forEach(linha=>{

        if(linha.trim() != ''){

            let partes =
            linha.split('-')

            let nome =
            partes[0] ? partes[0].trim() : ''

            let preco =
            partes[1] ? partes[1].trim() : ''

            let descricao =
            partes[2] ? partes[2].trim() : ''

            produtos.push({

                nome,
                preco,
                descricao,
                tema,
                tamanho,
                tituloTopo

            })
        }
    })

    atualizarLista()

    gerarCartazes()

    document.getElementById('listaTexto').value = ''
}

function atualizarLista(){

    let lista =
    document.getElementById('listaProdutos')

    lista.innerHTML = ''

    produtos.forEach((produto,index)=>{

        lista.innerHTML += `

        <div class="item">

            <div class="thumb">

                <div class="thumb-top">
                ${produto.tituloTopo}
                </div>

                <div class="thumb-preco">
                ${produto.preco}
                </div>

            </div>

            <div class="info">

                <h3>
                ${produto.nome}
                </h3>

                <p>
                R$ ${produto.preco}
                </p>

                <span>
                ${produto.descricao}
                </span>

            </div>

            <div class="acoes">

                <div class="icon"
                onclick="remover(${index})">

                🗑

                </div>

            </div>

        </div>
        `
    })
}

function gerarCartazes(){

    let area =
    document.getElementById('todosCartazes')

    area.innerHTML = ''

    produtos.forEach(produto=>{

        let classeTamanho = ''

        if(produto.tamanho == 'a4-retrato'){
            classeTamanho = 'a4-retrato'
        }

        if(produto.tamanho == 'a4-paisagem'){
            classeTamanho = 'a4-paisagem'
        }

        if(produto.tamanho == '11x15'){
            classeTamanho = 'tamanho-11x15'
        }

        if(produto.tamanho == '20x27'){
            classeTamanho = 'tamanho-20x27'
        }

        area.innerHTML += `

        <div class="cartaz tema-${produto.tema} ${classeTamanho}">

            <div class="topo-cartaz">

                <h1>
                ${produto.tituloTopo}
                </h1>

            </div>

            <div class="nome-produto">

                ${produto.nome}

            </div>

            <div class="pincel">

                ${produto.descricao}

            </div>

            <div class="area-preco">

                ${
                    produto.tema == 'ofertao'
                    ?
                    `
                    <span class="valor">
                    ${produto.preco}
                    </span>

                    <div style="
                    font-size:70px;
                    font-weight:900;
                    margin-top:-40px;
                    color:black;
                    ">
                    UNIDADE
                    </div>
                    `
                    :
                    `
                    <span class="rs">
                    R$
                    </span>

                    <span class="valor">
                    ${produto.preco}
                    </span>
                    `
                }

            </div>

            <div class="rodape"></div>

        </div>
        `
    })
}

function remover(index){

    produtos.splice(index,1)

    atualizarLista()

    gerarCartazes()
}

function limparTudo(){

    produtos = []

    atualizarLista()

    gerarCartazes()

    document.getElementById('listaTexto').value = ''
}

</script>

</body>

</html>
