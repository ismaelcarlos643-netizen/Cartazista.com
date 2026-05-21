<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>

<title>Cartazista Offline</title>

<!-- Fonte estilo cartaz -->
<link href="https://fonts.googleapis.com/css2?family=Anton&family=Montserrat:wght@400;700;900&display=swap" rel="stylesheet">

<style>
    *{
        margin:0;
        padding:0;
        box-sizing:border-box;
    }

    body{
        font-family:'Montserrat',sans-serif;
        background:#ececec;
        color:#222;
        overflow:hidden;
    }

    .app{
        display:flex;
        height:100vh;
    }

    /* =========================
       PAINEL ESQUERDO
    ==========================*/
    .sidebar{
        width:380px;
        min-width:380px;
        background:#111;
        color:#fff;
        padding:20px;
        display:flex;
        flex-direction:column;
        gap:15px;
        border-right:4px solid #ffcc00;
    }

    .logo{
        font-size:28px;
        font-weight:900;
        color:#ffcc00;
    }

    .sub{
        font-size:13px;
        color:#ccc;
        line-height:1.5;
    }

    textarea{
        flex:1;
        width:100%;
        resize:none;
        border:none;
        outline:none;
        border-radius:10px;
        padding:15px;
        font-size:15px;
        font-family:monospace;
        background:#222;
        color:#fff;
        line-height:1.6;
    }

    .controls{
        display:flex;
        flex-direction:column;
        gap:10px;
    }

    select,
    button{
        height:50px;
        border:none;
        border-radius:10px;
        font-size:15px;
        font-weight:700;
    }

    select{
        padding:0 12px;
        background:#fff;
    }

    button{
        background:#ffcc00;
        cursor:pointer;
        transition:0.2s;
    }

    button:hover{
        transform:scale(1.02);
    }

    .tip{
        font-size:12px;
        color:#aaa;
    }

    /* =========================
       ÁREA PREVIEW
    ==========================*/
    .preview{
        flex:1;
        overflow:auto;
        padding:30px;
        display:grid;
        grid-template-columns:repeat(auto-fill,minmax(340px,1fr));
        gap:25px;
    }

    /* =========================
       CARTAZ BASE
    ==========================*/
    .cartaz{
        width:100%;
        aspect-ratio:1 / 1.35;
        background:#fff;
        border-radius:18px;
        overflow:hidden;
        box-shadow:0 10px 25px rgba(0,0,0,0.18);
        display:flex;
        flex-direction:column;
        position:relative;
        page-break-inside:avoid;
        break-inside:avoid;
    }

    .topo{
        padding:12px;
        text-align:center;
        font-size:26px;
        font-weight:900;
        letter-spacing:2px;
    }

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

    .preco-area{
        padding:20px;
        display:flex;
        align-items:flex-end;
        justify-content:center;
        gap:8px;
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

    .rodape{
        text-align:center;
        padding:10px;
        font-size:15px;
        font-weight:700;
    }

    /* =========================
       TEMAS
    ==========================*/

    /* Tema 1 */
    .tema1{
        background:#fff;
    }

    .tema1 .topo{
        background:#d60000;
        color:#fff;
    }

    .tema1 .produto{
        color:#111;
    }

    .tema1 .preco{
        color:#d60000;
    }

    .tema1 .rodape{
        background:#111;
        color:#fff;
    }

    /* Tema 2 */
    .tema2{
        background:#000;
    }

    .tema2 .topo{
        background:#ffcc00;
        color:#000;
    }

    .tema2 .produto{
        color:#fff;
    }

    .tema2 .cifrao,
    .tema2 .preco{
        color:#ffcc00;
    }

    .tema2 .rodape{
        background:#ffcc00;
        color:#000;
    }

    /* Tema 3 */
    .tema3{
        background:#0f3d91;
    }

    .tema3 .topo{
        background:#fff;
        color:#0f3d91;
    }

    .tema3 .produto{
        color:#fff;
    }

    .tema3 .cifrao,
    .tema3 .preco{
        color:#fff700;
    }

    .tema3 .rodape{
        background:#fff700;
        color:#000;
    }

    /* =========================
       IMPRESSÃO
    ==========================*/
    @page{
        size:A4 portrait;
        margin:8mm;
    }

    @media print{

        body{
            background:#fff;
            overflow:visible;
        }

        .sidebar{
            display:none !important;
        }

        .preview{
            display:block;
            padding:0;
            margin:0;
        }

        .cartaz{
            width:190mm;
            height:277mm;
            margin:0 auto;
            border-radius:0;
            box-shadow:none;
            page-break-after:always;
            break-after:page;
        }

        .cartaz:last-child{
            page-break-after:auto;
        }

        .produto{
            font-size:70px;
        }

        .preco{
            font-size:180px;
        }

        .topo{
            font-size:40px;
        }

        .rodape{
            font-size:24px;
        }

    }

</style>
</head>
<body>

<div class="app">

    <!-- LATERAL -->
    <div class="sidebar">

        <div>
            <div class="logo">
                CARTAZISTA OFFLINE
            </div>

            <div class="sub">
                Digite um produto por linha usando:
                <br><br>
                Nome do Produto ; preço
            </div>
        </div>

        <textarea id="entrada">
Arroz Tipo 1;25.99
Feijão Carioca;8.49
Óleo de Soja;6.99
Café Torrado;14.90
Açúcar Cristal;4.99
        </textarea>

        <div class="controls">

            <select id="tema">
                <option value="tema1">Tema Vermelho</option>
                <option value="tema2">Tema Preto</option>
                <option value="tema3">Tema Azul</option>
            </select>

            <button onclick="imprimirCartazes()">
                Imprimir Cartazes
            </button>

        </div>

        <div class="tip">
            Exemplo:
            <br>
            Refrigerante 2L;9.99
        </div>

    </div>

    <!-- PREVIEW -->
    <div class="preview" id="preview"></div>

</div>

<script>

const entrada = document.getElementById("entrada");
const preview = document.getElementById("preview");
const tema = document.getElementById("tema");

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

        cartaz.className = `cartaz ${tema.value}`;

        cartaz.innerHTML = `
            <div class="topo">
                PROMOÇÃO
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

gerarCartazes();

</script>

</body>
</html>
