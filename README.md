<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Cartazista Pro</title>

<style>

/* =========================================================
RESET
========================================================= */

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{

    background:#111;
    font-family:Arial, sans-serif;

}

/* =========================================================
PAINEL
========================================================= */

.painel{

    width:100%;
    max-width:420px;

    margin:20px auto;

    background:#fff;

    padding:20px;

    border-radius:14px;

}

.campo{

    margin-bottom:15px;

}

.campo label{

    display:block;

    margin-bottom:6px;

    font-weight:bold;

}

.campo input,
.campo select{

    width:100%;

    padding:14px;

    border-radius:8px;

    border:1px solid #ccc;

    font-size:16px;

}

button{

    width:100%;

    border:none;

    background:#00b85c;

    color:#fff;

    padding:16px;

    border-radius:10px;

    font-size:18px;

    font-weight:bold;

    cursor:pointer;

}

/* =========================================================
ÁREA
========================================================= */

.area{

    display:flex;

    justify-content:center;

    padding:20px;

}

/* =========================================================
CARTAZ
========================================================= */

.cartaz{

    width:210mm;
    height:297mm;

    background:#fff;

    position:relative;

    overflow:hidden;

}

/* =========================================================
TEMAS
========================================================= */

.vermelho{

    --topo:#df140a;
    --textoTopo:#ffd84d;
    --preco:#ef1b12;
    --pincel:#ffd400;

}

.azul{

    --topo:#005eff;
    --textoTopo:#ffffff;
    --preco:#005eff;
    --pincel:#7dc7ff;

}

.verde{

    --topo:#00a651;
    --textoTopo:#ffffff;
    --preco:#00a651;
    --pincel:#98ff98;

}

.amarelo{

    --topo:#ffcc00;
    --textoTopo:#000;
    --preco:#ff9900;
    --pincel:#fff27a;

}

/* =========================================================
TOPO
========================================================= */

.topo{

    height:24%;

    background:var(--topo);

    position:relative;

    display:flex;

    justify-content:center;
    align-items:center;

}

.topo::after{

    content:"";

    position:absolute;

    bottom:-45px;
    left:-5%;

    width:110%;
    height:90px;

    background:#fff;

    border-radius:50%;

}

.topo h1{

    color:var(--textoTopo);

    font-size:95px;

    font-family:
    Georgia,
    serif;

    font-weight:bold;

    z-index:2;

}

/* =========================================================
CONTEÚDO
========================================================= */

.conteudo{

    height:76%;

    display:flex;

    flex-direction:column;

    justify-content:space-between;

    text-align:center;

    padding:20px 20px 0;

}

/* =========================================================
DESCRIÇÃO METADE
========================================================= */

.descricao{

    height:45%;

    display:flex;

    flex-direction:column;

    justify-content:center;

}

/* =========================================================
PRODUTO
========================================================= */

.produto{

    font-size:82px;

    font-weight:999;

    font-family:
    Impact,
    Arial Black,
    sans-serif;

    font-style:italic;

    line-height:0.88;

    letter-spacing:-3px;

    text-transform:uppercase;

    color:#111;

}

/* =========================================================
PINCEL
========================================================= */

.pincel{

    position:relative;

    width:100%;

    max-width:90%;

    margin:14px auto;

    padding:12px;

}

.pincel::before{

    content:"";

    position:absolute;

    inset:0;

    background:
    repeating-linear-gradient(

        0deg,

        var(--pincel) 0px,
        var(--pincel) 14px,

        #ffffff55 14px,
        #ffffff55 22px

    );

    transform:skew(-5deg);

    z-index:-1;

}

/* =========================================================
PREÇO METADE
========================================================= */

.preco-area{

    height:55%;

    display:flex;

    flex-direction:column;

    justify-content:center;

    align-items:center;

}

/* =========================================================
PREÇO GIGANTE
========================================================= */

.preco{

    font-size:300px;

    font-family:
    Impact,
    Arial Black,
    sans-serif;

    font-weight:999;

    line-height:0.8;

    color:var(--preco);

    letter-spacing:-18px;

    white-space:nowrap;

}

/* =========================================================
UNIDADE
========================================================= */

.unidade{

    margin-top:10px;

    font-size:58px;

    font-family:
    Impact,
    Arial Black,
    sans-serif;

    font-weight:999;

    letter-spacing:-2px;

}

/* =========================================================
RODAPÉ
========================================================= */

.rodape{

    position:absolute;

    bottom:0;

    width:100%;
    height:90px;

    background:var(--topo);

    display:flex;

    justify-content:center;
    align-items:center;

}

.rodape::before{

    content:"";

    position:absolute;

    top:-35px;
    left:-5%;

    width:110%;
    height:70px;

    background:#fff;

    border-radius:50%;

}

.loja{

    color:var(--textoTopo);

    font-size:52px;

    font-weight:bold;

    font-family:
    Georgia,
    serif;

    z-index:2;

}

/* =========================================================
MOBILE
========================================================= */

@media(max-width:900px){

    .cartaz{

        transform:scale(.42);

        transform-origin:top center;

    }

    .area{

        height:1400px;

    }

}

/* =========================================================
IMPRESSÃO
========================================================= */

@media print{

    body{
        background:#fff;
    }

    .painel{
        display:none;
    }

    .area{
        padding:0;
    }

    .cartaz{
        transform:none;
    }

}

</style>
</head>

<body>

<!-- =========================================================
PAINEL
========================================================= -->

<div class="painel">

    <div class="campo">

        <label>Oferta</label>

        <input
        type="text"
        id="oferta"
        value="OFERTA"
        oninput="atualizar()">

    </div>

    <div class="campo">

        <label>Produto</label>

        <input
        type="text"
        id="produto"
        value="COXÃO MOLE"
        oninput="atualizar()">

    </div>

    <div class="campo">

        <label>Complemento</label>

        <input
        type="text"
        id="complemento"
        value="BOVINO KG"
        oninput="atualizar()">

    </div>

    <div class="campo">

        <label>Preço</label>

        <input
        type="text"
        id="preco"
        value="35,90"
        oninput="atualizar()">

    </div>

    <div class="campo">

        <label>Loja</label>

        <input
        type="text"
        id="loja"
        value="IC ART'S"
        oninput="atualizar()">

    </div>

    <div class="campo">

        <label>Cor</label>

        <select
        id="tema"
        onchange="trocarTema()">

            <option value="vermelho">
                Vermelho
            </option>

            <option value="azul">
                Azul
            </option>

            <option value="verde">
                Verde
            </option>

            <option value="amarelo">
                Amarelo
            </option>

        </select>

    </div>

    <button onclick="window.print()">
        SALVAR PDF / IMPRIMIR
    </button>

</div>

<!-- =========================================================
ÁREA
========================================================= -->

<div class="area">

<div
class="cartaz vermelho"
id="cartaz">

    <!-- TOPO -->

    <div class="topo">

        <h1 id="viewOferta">
            OFERTA
        </h1>

    </div>

    <!-- CONTEÚDO -->

    <div class="conteudo">

        <!-- DESCRIÇÃO -->

        <div class="descricao">

            <div
            class="produto"
            id="viewProduto">

                COXÃO MOLE

            </div>

            <div class="pincel">

                <div
                class="produto"
                id="viewComplemento">

                    BOVINO KG

                </div>

            </div>

        </div>

        <!-- PREÇO -->

        <div class="preco-area">

            <div class="pincel">

                <div
                class="preco"
                id="viewPreco">

                    35,90

                </div>

            </div>

            <div class="unidade">
                UNIDADE
            </div>

        </div>

    </div>

    <!-- RODAPÉ -->

    <div class="rodape">

        <div
        class="loja"
        id="viewLoja">

            IC ART'S

        </div>

    </div>

</div>

</div>

<script>

/* =========================================================
ATUALIZAÇÃO
========================================================= */

function atualizar(){

    document.getElementById("viewOferta").innerText =
    document.getElementById("oferta").value;

    document.getElementById("viewProduto").innerText =
    document.getElementById("produto").value;

    document.getElementById("viewComplemento").innerText =
    document.getElementById("complemento").value;

    document.getElementById("viewPreco").innerText =
    document.getElementById("preco").value;

    document.getElementById("viewLoja").innerText =
    document.getElementById("loja").value;

}

/* =========================================================
TEMA
========================================================= */

function trocarTema(){

    const tema =
    document.getElementById("tema").value;

    const cartaz =
    document.getElementById("cartaz");

    cartaz.className =
    "cartaz " + tema;

}

</script>

</body>
</html>
