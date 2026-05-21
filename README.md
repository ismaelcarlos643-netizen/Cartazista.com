<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>

<title>Cartazista Offline PRO</title>

<link href="https://fonts.googleapis.com/css2?family=Anton&family=Montserrat:wght@400;700;900&display=swap" rel="stylesheet">

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    font-family:'Montserrat',sans-serif;
    background:#e9e9e9;
    overflow:hidden;
}

.app{
    display:flex;
    height:100vh;
}

/* ===================================
   MENU LATERAL
=================================== */

.sidebar{
    width:390px;
    min-width:390px;
    background:#111;
    color:#fff;
    padding:20px;
    display:flex;
    flex-direction:column;
    gap:15px;
    border-right:5px solid #ffd000;
}

.logo{
    font-size:30px;
    font-weight:900;
    color:#ffd000;
}

.sub{
    font-size:13px;
    color:#bbb;
    line-height:1.5;
}

textarea{
    flex:1;
    resize:none;
    width:100%;
    border:none;
    outline:none;
    border-radius:12px;
    background:#1f1f1f;
    color:#fff;
    padding:15px;
    font-size:15px;
    line-height:1.6;
    font-family:monospace;
}

.controls{
    display:flex;
    flex-direction:column;
    gap:10px;
}

select,
button{
    height:52px;
    border:none;
    border-radius:10px;
    font-size:15px;
    font-weight:700;
}

select{
    padding:0 10px;
}

button{
    background:#ffd000;
    cursor:pointer;
    transition:0.2s;
}

button:hover{
    transform:scale(1.02);
}

/* ===================================
   PREVIEW
=================================== */

.preview{
    flex:1;
    overflow:auto;
    padding:30px;
    display:grid;
    grid-template-columns:repeat(auto-fill,minmax(330px,1fr));
    gap:25px;
}

/* ===================================
   CARTAZ
=================================== */

.cartaz{
    background:#fff;
    border-radius:20px;
    overflow:hidden;
    display:flex;
    flex-direction:column;
    aspect-ratio:1/1.35;
    box-shadow:0 10px 25px rgba(0,0,0,0.15);
    page-break-inside:avoid;
    break-inside:avoid;
}

/* TOPO */

.topo{
    text-align:center;
    padding:14px;
    font-size:28px;
    font-weight:900;
    letter-spacing:2px;
}

/* PRODUTO */

.produto{
    flex:1;
    display:flex;
    align-items:center;
    justify-content:center;
    text-align:center;
    padding:20px;
    font-size:44px;
    font-weight:900;
    line-height:1.1;
    text-transform:uppercase;
}

/* PREÇO */

.preco-area{
    display:flex;
    align-items:flex-end;
    justify-content:center;
    gap:8px;
    padding:20px;
}

.cifrao{
    font-size:42px;
    font-weight:900;
    margin-bottom:18px;
}

.preco{
    font-family:'Anton',sans-serif;
    font-size:110px;
    line-height:0.9;
}

/* RODAPÉ */

.rodape{
    text-align:center;
    padding:12px;
    font-size:15px;
    font-weight:700;
}

/* ===================================
   TAMANHO 4 POR FOLHA
=================================== */

.pequeno{
    aspect-ratio:1/1.1;
}

.pequeno .produto{
    font-size:28px;
}

.pequeno .preco{
    font-size:70px;
}

.pequeno .cifrao{
    font-size:28px;
}

.pequeno .topo{
    font-size:20px;
}

.pequeno .rodape{
    font-size:12px;
}

/* ===================================
   TEMAS
=================================== */

/* VERMELHO */

.tema-vermelho{
    background:#fff;
}

.tema-vermelho .topo{
    background:#d60000;
    color:#fff;
}

.tema-vermelho .produto{
    color:#111;
}

.tema-vermelho .preco,
.tema-vermelho .cifrao{
    color:#d60000;
}

.tema-vermelho .rodape{
    background:#111;
    color:#fff;
}

/* CONFIRA */

.tema-confira{
    background:#ffffff;
}

.tema-confira .topo{
    background:#0057d8;
    color:#fff;
}

.tema-confira .produto{
    color:#003e99;
}

.tema-confira .preco,
.tema-confira .cifrao{
    color:#0057d8;
}

.tema-confira .rodape{
    background:#0057d8;
    color:#fff;
}

/* HORTIFRUTI */

.tema-horti{
    background:#ffffff;
}

.tema-horti .topo{
    background:#1c9b31;
    color:#fff;
}

.tema-horti .produto{
    color:#0f5d1d;
}

.tema-horti .preco,
.tema-horti .cifrao{
    color:#1c9b31;
}

.tema-horti .rodape{
    background:#0f5d1d;
    color:#fff;
}

/* AÇOUGUE */

.tema-acougue{
    background:#fff5f5;
}

.tema-acougue .topo{
    background:#8b0000;
    color:#fff;
}

.tema-acougue .produto{
    color:#5a0000;
}

.tema-acougue .preco,
.tema-acougue .cifrao{
    color:#c40000;
}

.tema-acougue .rodape{
    background:#5a0000;
    color:#fff;
}

/* ===================================
   IMPRESSÃO
=================================== */

@page{
    size:A4;
    margin:8mm;
}

@media print{

    body{
        background:#fff;
        overflow:visible;
    }

    .sidebar{
        display:none;
    }

    .preview{
        display:grid;
        gap:0;
        padding:0;
    }

    /* GRANDE */

    .grande-print{
        grid-template-columns:1fr;
    }

    .grande-print .cartaz{
        width:190mm;
        height:277mm;
        border-radius:0;
        box-shadow:none;
        margin:auto;
        page-break-after:always;
    }

    .grande-print .produto{
        font-size:72px;
    }

    .grande-print .preco{
        font-size:190px;
    }

    /* 4 POR FOLHA */

    .quatro-print{
        grid-template-columns:1fr 1fr;
    }

    .quatro-print .cartaz{
        width:95mm;
        height:135mm;
        border-radius:0;
        box-shadow:none;
        margin:0;
        break-inside:avoid;
    }

}

</style>
</head>
<body>

<div class="app">

    <!-- MENU -->
    <div class="sidebar">

        <div class="logo">
            CARTAZISTA OFFLINE PRO
        </div>

        <div class="sub">
            Digite:
            <br><br>
            Nome do Produto ; preço
        </div>

<textarea id="entrada">
Tomate KG;8.99
Batata KG;6.49
Banana Prata;4.99
Picanha KG;49.90
Frango KG;12.99
</textarea>

        <div class="controls">

            <select id="tema">

                <option value="tema-vermelho">
                    Promoção Vermelha
                </option>

                <option value="tema-confira">
                    Confira Azul
                </option>

                <option value="tema-horti">
                    Hortifruti Verde
                </option>

                <option value="tema-acougue">
                    Açougue Vermelho
                </option>

            </select>

            <select id="modo">

                <option value="grande">
                    1 Cartaz Grande por Folha
                </option>

                <option value="pequeno">
                    4 Cartazes Pequenos por Folha
                </option>

            </select>

            <button onclick="imprimirCartazes()">
                Imprimir Cartazes
            </button>

        </div>

    </div>

    <!-- PREVIEW -->
    <div class="preview grande-print" id="preview"></div>

</div>

<script>

const entrada = document.getElementById("entrada");
const preview = document.getElementById("preview");
const tema = document.getElementById("tema");
const modo = document.getElementById("modo");

function formatarPreco(valor){

    let numero = parseFloat(
        valor.replace(",", ".")
    );

    if(isNaN(numero)){
        numero = 0;
    }

    return numero.toFixed(2).replace(".", ",");
}

function gerarCartazes(){

    preview.innerHTML = "";

    if(modo.value === "pequeno"){
        preview.className = "preview quatro-print";
    }else{
        preview.className = "preview grande-print";
    }

    const linhas = entrada.value
        .split("\n")
        .filter(linha => linha.trim() !== "");

    linhas.forEach(linha => {

        const partes = linha.split(";");

        const produto = partes[0]
            ? partes[0].trim()
            : "PRODUTO";

        const preco = partes[1]
            ? formatarPreco(partes[1])
            : "0,00";

        const cartaz = document.createElement("div");

        let tamanhoClasse = "";

        if(modo.value === "pequeno"){
            tamanhoClasse = "pequeno";
        }

        cartaz.className =
            `cartaz ${tema.value} ${tamanhoClasse}`;

        let titulo = "PROMOÇÃO";

        if(tema.value === "tema-confira"){
            titulo = "CONFIRA";
        }

        if(tema.value === "tema-horti"){
            titulo = "HORTIFRUTI";
        }

        if(tema.value === "tema-acougue"){
            titulo = "AÇOUGUE";
        }

        cartaz.innerHTML = `

            <div class="topo">
                ${titulo}
            </div>

            <div class="produto">
                ${produto}
            </div>

            <div class="preco-area">

                <div class="cifrao">
                    R$
                </div>

                <div class="preco">
                    ${preco}
                </div>

            </div>

            <div class="rodape">
                OFERTA ESPECIAL
            </div>

        `;

        preview.appendChild(cartaz);

    });

}

function imprimirCartazes(){
    window.print();
}

entrada.addEventListener("input", gerarCartazes);
tema.addEventListener("change", gerarCartazes);
modo.addEventListener("change", gerarCartazes);

gerarCartazes();

</script>

</body>
</html>
