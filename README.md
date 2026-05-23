<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Gerador de Cartaz Mercado</title>

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
    font-family: Arial, Helvetica, sans-serif;
    display:flex;
    gap:30px;
    padding:20px;
    min-height:100vh;
}

/* =========================================================
   PAINEL
========================================================= */

.painel{
    width:320px;
    background:#fff;
    padding:20px;
    border-radius:14px;
    box-shadow:0 10px 25px rgba(0,0,0,.2);
    height:max-content;
}

.painel h2{
    margin-bottom:20px;
    font-size:24px;
}

.campo{
    margin-bottom:15px;
}

.campo label{
    display:block;
    margin-bottom:6px;
    font-weight:bold;
    color:#333;
}

.campo input{
    width:100%;
    padding:12px;
    border-radius:8px;
    border:1px solid #ccc;
    font-size:16px;
}

.btn{
    width:100%;
    padding:14px;
    border:none;
    border-radius:10px;
    background:#00b85c;
    color:#fff;
    font-size:17px;
    font-weight:bold;
    cursor:pointer;
    transition:.2s;
}

.btn:hover{
    background:#00994d;
}

/* =========================================================
   ÁREA CARTAZ
========================================================= */

.preview{
    flex:1;
    display:flex;
    justify-content:center;
}

.cartaz{
    width:420px;
    height:740px;
    background:#fff;
    overflow:hidden;
    position:relative;
}

/* =========================================================
   TOPO VERMELHO
========================================================= */

.topo{
    background:#d91c11;
    height:180px;
    position:relative;
    display:flex;
    justify-content:center;
    align-items:center;
}

.topo::after{
    content:"";
    position:absolute;
    bottom:-1px;
    left:0;
    width:100%;
    height:70px;
    background:#fff;
    border-radius:100% 100% 0 0;
}

.topo h1{
    color:#ffd84d;
    font-size:72px;
    z-index:2;
    font-weight:900;
    letter-spacing:2px;
}

/* =========================================================
   CONTEÚDO
========================================================= */

.conteudo{
    padding:20px;
    text-align:center;
}

.produto{
    font-size:52px;
    font-weight:900;
    font-style:italic;
    line-height:1.0;
    text-transform:uppercase;
    margin-top:20px;
    color:#000;
}

/* pincel amarelo */

.pincel{
    background:
        linear-gradient(
            90deg,
            #ffd400 0%,
            #ffe44d 50%,
            #ffd400 100%
        );
    margin:10px auto;
    padding:8px 20px;
    width:100%;
    max-width:340px;
    transform:skew(-3deg);
}

/* =========================================================
   PREÇO
========================================================= */

.preco-area{
    margin-top:30px;
}

.preco{
    font-size:180px;
    line-height:.8;
    font-weight:900;
    color:#e11b12;
    letter-spacing:-8px;
}

.unidade{
    font-size:36px;
    font-weight:900;
    margin-top:10px;
}

/* =========================================================
   RODAPÉ
========================================================= */

.rodape{
    position:absolute;
    bottom:0;
    left:0;
    width:100%;
    height:90px;
    background:#d91c11;
    display:flex;
    justify-content:center;
    align-items:center;
}

.rodape::before{
    content:"";
    position:absolute;
    top:-45px;
    left:0;
    width:100%;
    height:60px;
    background:#fff;
    border-radius:0 0 100% 100%;
}

.loja{
    color:#ffd84d;
    font-size:40px;
    font-weight:900;
    z-index:2;
}

/* =========================================================
   IMPRESSÃO
========================================================= */

@media print{

    body{
        padding:0;
        margin:0;
        background:#fff;
    }

    .painel{
        display:none;
    }

    .cartaz{
        width:210mm;
        height:297mm;
    }

}

</style>
</head>

<body>

<!-- ========================================
     PAINEL
======================================== -->

<div class="painel">

    <h2>Gerador de Cartaz</h2>

    <div class="campo">
        <label>Texto do topo</label>
        <input
            type="text"
            id="inputOferta"
            value="OFERTA"
            oninput="atualizar()"
        >
    </div>

    <div class="campo">
        <label>Produto</label>
        <input
            type="text"
            id="inputProduto"
            value="COXÃO MOLE"
            oninput="atualizar()"
        >
    </div>

    <div class="campo">
        <label>Complemento</label>
        <input
            type="text"
            id="inputComplemento"
            value="BOVINO KG"
            oninput="atualizar()"
        >
    </div>

    <div class="campo">
        <label>Preço</label>
        <input
            type="text"
            id="inputPreco"
            value="35,90"
            oninput="atualizar()"
        >
    </div>

    <div class="campo">
        <label>Rodapé</label>
        <input
            type="text"
            id="inputLoja"
            value="IC ART'S"
            oninput="atualizar()"
        >
    </div>

    <button class="btn" onclick="window.print()">
        Imprimir Cartaz
    </button>

</div>

<!-- ========================================
     CARTAZ
======================================== -->

<div class="preview">

    <div class="cartaz">

        <!-- TOPO -->

        <div class="topo">
            <h1 id="viewOferta">OFERTA</h1>
        </div>

        <!-- CONTEÚDO -->

        <div class="conteudo">

            <div class="produto" id="viewProduto">
                COXÃO MOLE
            </div>

            <div class="pincel">
                <div class="produto" id="viewComplemento">
                    BOVINO KG
                </div>
            </div>

            <!-- PREÇO -->

            <div class="preco-area">

                <div class="pincel">

                    <div class="preco" id="viewPreco">
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
            <div class="loja" id="viewLoja">
                IC ART'S
            </div>
        </div>

    </div>

</div>

<script>

function atualizar(){

    document.getElementById("viewOferta").innerText =
        document.getElementById("inputOferta").value;

    document.getElementById("viewProduto").innerText =
        document.getElementById("inputProduto").value;

    document.getElementById("viewComplemento").innerText =
        document.getElementById("inputComplemento").value;

    document.getElementById("viewPreco").innerText =
        document.getElementById("inputPreco").value;

    document.getElementById("viewLoja").innerText =
        document.getElementById("inputLoja").value;
}

</script>

</body>
</html>
