<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Cartazista</title>

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    background:#1b1b1b;
    font-family:Arial, sans-serif;
}

/* =========================================
PAINEL
========================================= */

.painel{
    width:100%;
    max-width:420px;
    margin:20px auto;
    background:#fff;
    padding:20px;
    border-radius:12px;
}

.campo{
    margin-bottom:15px;
}

.campo label{
    display:block;
    margin-bottom:5px;
    font-weight:bold;
}

.campo input,
.campo select{

    width:100%;
    padding:14px;
    border:1px solid #ccc;
    border-radius:8px;
    font-size:16px;

}

button{

    width:100%;
    padding:16px;
    border:none;
    border-radius:10px;
    background:#00b85c;
    color:#fff;
    font-size:18px;
    font-weight:bold;

}

/* =========================================
ÁREA
========================================= */

.area{
    display:flex;
    justify-content:center;
    padding:20px;
}

/* =========================================
FOLHA A4
========================================= */

.cartaz{

    width:210mm;
    height:297mm;

    background:#fff;
    overflow:hidden;
    position:relative;

}

/* =========================================
CORES
========================================= */

.vermelho{

    --topo:#d91f11;
    --textoTopo:#ffd84d;
    --preco:#e31b12;
    --pincel:#ffd400;

}

.azul{

    --topo:#005eff;
    --textoTopo:#ffffff;
    --preco:#005eff;
    --pincel:#8cc8ff;

}

.verde{

    --topo:#00a651;
    --textoTopo:#ffffff;
    --preco:#00a651;
    --pincel:#9cff9c;

}

.amarelo{

    --topo:#ffcc00;
    --textoTopo:#000;
    --preco:#ff9900;
    --pincel:#fff27a;

}

/* =========================================
TOPO
========================================= */

.topo{

    height:24%;
    background:var(--topo);

    position:relative;

    display:flex;
    align-items:center;
    justify-content:center;

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

    font-size:90px;
    font-family:Georgia, serif;
    font-weight:bold;

    z-index:2;

}

/* =========================================
CONTEÚDO
========================================= */

.conteudo{

    text-align:center;
    padding:40px 25px;

}

.produto{

    font-size:70px;
    font-weight:900;
    font-style:italic;
    line-height:0.95;
    text-transform:uppercase;

}

/* =========================================
PINCEL
========================================= */

.pincel{

    position:relative;

    margin:15px auto;

    width:100%;
    max-width:85%;

    padding:10px;

}

.pincel::before{

    content:"";

    position:absolute;
    inset:0;

    background:
    repeating-linear-gradient(
        0deg,
        var(--pincel) 0px,
        var(--pincel) 12px,
        #ffffff44 12px,
        #ffffff44 20px
    );

    transform:skew(-4deg);

    z-index:-1;

}

/* =========================================
PREÇO
========================================= */

.preco{

    font-size:220px;
    font-weight:900;
    line-height:0.85;
    color:var(--preco);

    letter-spacing:-10px;

    white-space:nowrap;

}

/* =========================================
UNIDADE
========================================= */

.unidade{

    margin-top:10px;

    font-size:50px;
    font-weight:900;

}

/* =========================================
RODAPÉ
========================================= */

.rodape{

    position:absolute;
    bottom:0;

    width:100%;
    height:90px;

    background:var(--topo);

    display:flex;
    align-items:center;
    justify-content:center;

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

    font-size:50px;
    font-family:Georgia, serif;

    z-index:2;

}

/* =========================================
MOBILE PREVIEW
========================================= */

@media(max-width:900px){

    .cartaz{

        transform:scale(.45);
        transform-origin:top center;

    }

    .area{

        height:1400px;

    }

}

/* =========================================
IMPRESSÃO
========================================= */

@media print{

    body{
        background:#fff;
    }

    .painel{
        display:none;
    }

    .area{
        padding:0;
        margin:0;
    }

    .cartaz{

        transform:none;

    }

}

</style>
</head>

<body>

<!-- =========================================
PAINEL
========================================= -->

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

        <select id="tema" onchange="trocarTema()">

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

<!-- =========================================
ÁREA
========================================= -->

<div class="area">

    <div class="cartaz vermelho" id="cartaz">

        <!-- TOPO -->

        <div class="topo">

            <h1 id="viewOferta">
                OFERTA
            </h1>

        </div>

        <!-- CONTEÚDO -->

        <div class="conteudo">

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

            <!-- PREÇO -->

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
