<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gerador de Cartaz Profissional</title>

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
    display:flex;
    gap:30px;
    padding:20px;
    min-height:100vh;
}

/* =========================================================
PAINEL
========================================================= */

.painel{
    width:330px;
    background:#fff;
    padding:20px;
    border-radius:12px;
    height:max-content;
    box-shadow:0 10px 25px rgba(0,0,0,.25);
}

.painel h2{
    margin-bottom:20px;
    color:#111;
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

.campo input,
.campo select{
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
    font-size:16px;
    font-weight:bold;
    cursor:pointer;
    transition:.2s;
}

.btn:hover{
    background:#00994d;
}

/* =========================================================
PREVIEW
========================================================= */

.preview{
    flex:1;
    display:flex;
    justify-content:center;
    align-items:flex-start;
}

/* =========================================================
CARTAZ
========================================================= */

.cartaz{
    background:#fff;
    position:relative;
    overflow:hidden;
    transition:.3s;
}

/* =========================================================
TEMAS
========================================================= */

.cartaz.vermelho{

    --corPrincipal:#d91f11;
    --corTexto:#ffd84d;
    --corPreco:#e12216;
    --corPincel:#ffd400;

}

.cartaz.azul{

    --corPrincipal:#005eff;
    --corTexto:#ffffff;
    --corPreco:#005eff;
    --corPincel:#7dc7ff;

}

.cartaz.verde{

    --corPrincipal:#00a651;
    --corTexto:#ffffff;
    --corPreco:#00a651;
    --corPincel:#98ff98;

}

.cartaz.amarelo{

    --corPrincipal:#ffcc00;
    --corTexto:#000000;
    --corPreco:#ff8800;
    --corPincel:#fff27a;

}

/* =========================================================
TAMANHOS
========================================================= */

.cartaz.mini{
    width:300px;
    height:500px;
}

.cartaz.medio{
    width:430px;
    height:760px;
}

.cartaz.grande{
    width:520px;
    height:920px;
}

.cartaz.a4{
    width:210mm;
    height:297mm;
}

/* =========================================================
TOPO
========================================================= */

.topo{
    width:100%;
    height:170px;
    background:var(--corPrincipal);
    position:relative;
    display:flex;
    justify-content:center;
    align-items:center;
}

.topo::after{
    content:"";
    position:absolute;
    bottom:-40px;
    left:-5%;
    width:110%;
    height:90px;
    background:#fff;
    border-radius:50%;
}

.topo h1{
    color:var(--corTexto);
    font-size:78px;
    font-family:Georgia, serif;
    letter-spacing:2px;
    z-index:2;
}

/* =========================================================
CONTEÚDO
========================================================= */

.conteudo{
    position:relative;
    z-index:2;
    padding:20px;
    text-align:center;
}

.produto{
    font-size:64px;
    font-weight:900;
    font-style:italic;
    line-height:0.95;
    text-transform:uppercase;
    color:#000;
}

/* =========================================================
PINCEL
========================================================= */

.pincel{
    position:relative;
    margin:10px auto;
    width:100%;
    max-width:360px;
    padding:10px 20px;
}

.pincel::before{
    content:"";
    position:absolute;
    inset:0;

    background:
    repeating-linear-gradient(
        0deg,
        var(--corPincel) 0px,
        var(--corPincel) 10px,
        #ffffff55 10px,
        #ffffff55 18px
    );

    transform:skew(-4deg);
    border-radius:6px;
    z-index:-1;
}

/* =========================================================
PREÇO
========================================================= */

.preco-box{
    margin-top:20px;
}

.preco{
    font-size:170px;
    font-weight:900;
    line-height:0.9;
    color:var(--corPreco);
    letter-spacing:-8px;

    display:flex;
    justify-content:center;
    align-items:flex-end;

    width:100%;
    overflow:hidden;
}

.unidade{
    margin-top:10px;
    font-size:42px;
    font-weight:900;
}

/* =========================================================
RODAPÉ
========================================================= */

.rodape{
    position:absolute;
    bottom:0;
    width:100%;
    height:90px;
    background:var(--corPrincipal);

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
    color:var(--corTexto);
    font-size:42px;
    font-family:Georgia, serif;
    z-index:2;
}

/* =========================================================
RESPONSIVO
========================================================= */

@media(max-width:900px){

    body{
        flex-direction:column;
        align-items:center;
    }

}

/* =========================================================
IMPRESSÃO
========================================================= */

@media print{

    body{
        margin:0;
        padding:0;
        background:#fff;
    }

    .painel{
        display:none;
    }

}

</style>
</head>

<body>

<!-- =========================================================
PAINEL
========================================================= -->

<div class="painel">

    <h2>Gerador de Cartaz</h2>

    <div class="campo">
        <label>Oferta</label>
        <input
            type="text"
            id="oferta"
            value="OFERTA"
            oninput="atualizar()"
        >
    </div>

    <div class="campo">
        <label>Produto</label>
        <input
            type="text"
            id="produto"
            value="COXÃO MOLE"
            oninput="atualizar()"
        >
    </div>

    <div class="campo">
        <label>Complemento</label>
        <input
            type="text"
            id="complemento"
            value="BOVINO KG"
            oninput="atualizar()"
        >
    </div>

    <div class="campo">
        <label>Preço</label>
        <input
            type="text"
            id="preco"
            value="35,90"
            oninput="atualizar()"
        >
    </div>

    <div class="campo">
        <label>Loja</label>
        <input
            type="text"
            id="loja"
            value="IC ART'S"
            oninput="atualizar()"
        >
    </div>

    <div class="campo">
        <label>Cor do Cartaz</label>

        <select id="tema" onchange="trocarTema()">

            <option value="vermelho">Vermelho</option>
            <option value="azul">Azul</option>
            <option value="verde">Verde</option>
            <option value="amarelo">Amarelo</option>

        </select>
    </div>

    <div class="campo">
        <label>Tamanho do Cartaz</label>

        <select id="tamanho" onchange="trocarTamanho()">

            <option value="medio">Médio</option>
            <option value="mini">Mini</option>
            <option value="grande">Grande</option>
            <option value="a4">A4</option>

        </select>
    </div>

    <button class="btn" onclick="window.print()">
        IMPRIMIR CARTAZ
    </button>

</div>

<!-- =========================================================
PREVIEW
========================================================= -->

<div class="preview">

    <div class="cartaz vermelho medio" id="cartaz">

        <!-- TOPO -->

        <div class="topo">

            <h1 id="viewOferta">
                OFERTA
            </h1>

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

            <div class="preco-box">

                <div class="pincel">

                    <div class="preco">
                        <span id="viewPreco">
                            35,90
                        </span>
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

<!-- =========================================================
JAVASCRIPT
========================================================= -->

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

/* =========================================================
TEMA
========================================================= */

function trocarTema(){

    const tema =
    document.getElementById("tema").value;

    const cartaz =
    document.getElementById("cartaz");

    cartaz.classList.remove(
        "vermelho",
        "azul",
        "verde",
        "amarelo"
    );

    cartaz.classList.add(tema);

}

/* =========================================================
TAMANHO
========================================================= */

function trocarTamanho(){

    const tamanho =
    document.getElementById("tamanho").value;

    const cartaz =
    document.getElementById("cartaz");

    cartaz.classList.remove(
        "mini",
        "medio",
        "grande",
        "a4"
    );

    cartaz.classList.add(tamanho);

}

</script>

</body>
</html>
