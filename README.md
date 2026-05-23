<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Cartazista PRO</title>

<style>

/* IMPORTAÇÃO DAS FONTES GROSSAS */
@import url('https://fonts.googleapis.com/css2?family=Anton&family=Bebas+Neue&display=swap');

/* RESET */
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    font-family:Arial, sans-serif;
    background:#2b2b2b;
    display:flex;
    height:100vh;
    overflow:hidden;
}

/* PAINEL */
#painel-controle{
    width:400px;
    background:#1e1e24;
    color:#fff;
    padding:20px;
    overflow-y:auto;

    display:flex;
    flex-direction:column;
    gap:15px;

    box-shadow:4px 0 10px rgba(0,0,0,.5);
}

h2{
    color:#ffcc00;
    border-bottom:2px solid #ffcc00;
    padding-bottom:5px;
}

label{
    font-size:.9rem;
    font-weight:bold;
    color:#ccc;
}

select,
textarea{
    width:100%;
    padding:12px;
    border:none;
    border-radius:8px;

    background:#2d2d34;
    color:#fff;

    font-size:1rem;
}

textarea{
    min-height:180px;
    resize:none;
    font-family:monospace;
}

button{
    padding:14px;
    border:none;
    border-radius:8px;

    background:#28a745;
    color:#fff;

    font-size:1rem;
    font-weight:bold;

    cursor:pointer;
}

button:hover{
    background:#218838;
}

/* VISUALIZAÇÃO */
#area-visualizacao{
    flex:1;
    overflow:auto;
    padding:30px;

    display:flex;
    flex-direction:column;
    align-items:center;
    gap:40px;
}

/* CARTAZ */
.cartaz-a4{
    width:210mm;
    height:297mm;

    background:#ffde00;

    border:18px solid #e63946;

    padding:30px;

    display:flex;
    flex-direction:column;
    justify-content:space-between;
    align-items:center;

    box-shadow:0 10px 25px rgba(0,0,0,.5);
}

/* TOPO */
.topo-oferta{
    width:105%;

    background:#e63946;
    color:#fff;

    text-align:center;

    padding:15px 0;

    text-transform:uppercase;

    font-family:'Anton', sans-serif;

    font-size:5rem;

    letter-spacing:3px;

    text-shadow:
    4px 4px 0 rgba(0,0,0,.25);
}

/* CORPO */
.corpo-produto{
    flex:1;

    width:100%;

    display:flex;
    flex-direction:column;
    justify-content:center;
    align-items:center;
}

/* NOME PRODUTO */
.nome-produto{
    font-family:'Anton', sans-serif;

    font-size:6.5rem;

    color:#111;

    text-transform:uppercase;

    line-height:.95;

    text-align:center;

    letter-spacing:2px;
}

/* DETALHE */
.detalhe-produto{
    margin-top:10px;

    font-family:'Bebas Neue', sans-serif;

    font-size:3rem;

    color:#444;

    letter-spacing:2px;

    text-align:center;
}

/* PREÇO */
.bloco-preco{
    display:flex;
    flex-direction:column;
    align-items:center;
}

.cifrão{
    font-family:'Anton', sans-serif;

    font-size:4rem;

    color:#e63946;

    margin-bottom:-20px;
}

.valor-principal{
    font-family:'Bebas Neue', sans-serif;

    font-size:16rem;

    color:#e63946;

    line-height:.8;

    letter-spacing:-4px;

    text-shadow:
    5px 5px 0 rgba(0,0,0,.15);
}

.valor-centavos{
    font-size:7rem;
    vertical-align:super;
}

/* IMPRESSÃO */
@media print{

    body{
        background:none;
        overflow:visible;
    }

    #painel-controle{
        display:none;
    }

    #area-visualizacao{
        padding:0;
        overflow:visible;
        display:block;
    }

    .cartaz-a4{
        box-shadow:none;
        page-break-after:always;

        -webkit-print-color-adjust:exact;
        print-color-adjust:exact;
    }

    @page{
        margin:0;
        size:A4;
    }

}

</style>
</head>

<body>

<div id="painel-controle">

    <h2>Cartazista PRO</h2>

    <label>Dados dos Produtos</label>

    <textarea id="entrada-dados">
ARROZ TIO JOÃO;PCT 5KG;24,99
FEIJÃO CAMIL;1KG;7,49
LEITE INTEGRAL;CX 1L;4,29
    </textarea>

    <button onclick="window.print()">
        🖨️ Imprimir Cartazes
    </button>

</div>

<div id="area-visualizacao"></div>

<script>

const inputDados = document.getElementById('entrada-dados');
const area = document.getElementById('area-visualizacao');

function quebrarPreco(valor){

    let limpo = valor.replace('.', ',');

    if(limpo.includes(',')){

        let p = limpo.split(',');

        return{
            r:p[0],
            c:p[1]
        };
    }

    return{
        r:limpo,
        c:'00'
    };
}

function renderizar(){

    area.innerHTML = '';

    const linhas = inputDados.value.trim().split('\n');

    linhas.forEach(linha=>{

        if(!linha.trim()) return;

        const partes = linha.split(';');

        const nome = partes[0] || 'PRODUTO';
        const detalhe = partes[1] || '';
        const preco = quebrarPreco(partes[2] || '0,00');

        area.innerHTML += `

        <div class="cartaz-a4">

            <div class="topo-oferta">
                OFERTA
            </div>

            <div class="corpo-produto">

                <div class="nome-produto">
                    ${nome}
                </div>

                <div class="detalhe-produto">
                    ${detalhe}
                </div>

            </div>

            <div class="bloco-preco">

                <div class="cifrão">
                    R$
                </div>

                <div class="valor-principal">
                    ${preco.r}<span class="valor-centavos">,${preco.c}</span>
                </div>

            </div>

        </div>

        `;
    });
}

inputDados.addEventListener('input', renderizar);

renderizar();

</script>

</body>
</html>
