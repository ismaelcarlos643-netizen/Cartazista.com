<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Gerador Multi-Modelos de Cartazes PRO</title>

<style>

/* FONTES MAIS GROSSAS */
@import url('https://fonts.googleapis.com/css2?family=Anton&family=Bebas+Neue&display=swap');

/* RESET */
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    font-family:'Segoe UI', sans-serif;
    background:#333;
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

    display:flex;
    flex-direction:column;
    gap:15px;

    overflow-y:auto;

    box-shadow:4px 0 10px rgba(0,0,0,.5);
    z-index:10;
}

h2{
    color:#ffcc00;
    font-size:1.2rem;
    border-bottom:2px solid #ffcc00;
    padding-bottom:5px;
}

label{
    font-size:.85rem;
    color:#aaa;
    font-weight:bold;
}

select,
textarea{
    width:100%;
    background:#2d2d34;
    color:#fff;
    border:1px solid #444;

    padding:10px;
    font-size:.9rem;

    border-radius:4px;
}

textarea{
    resize:none;
    min-height:180px;
    font-family:monospace;
}

button{
    background:#28a745;
    color:#fff;
    border:none;

    padding:14px;

    font-size:1rem;
    font-weight:bold;

    border-radius:4px;

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

/* CARTAZ PADRÃO */
.cartaz-a4{
    width:210mm;
    height:297mm;

    background:#ffde00;

    border:15px solid #e63946;

    padding:30px;

    display:flex;
    flex-direction:column;
    justify-content:space-between;
    align-items:center;

    box-shadow:0 10px 25px rgba(0,0,0,.5);
}

/* ORIENTAÇÃO */
.cartaz-a4.deitado{
    width:297mm;
    height:210mm;
}

/* TEMAS */
.tema-padrao{
    background:#ffde00;
    border-color:#e63946;
}

.tema-acougue{
    background:#111;
    border-color:#e63946;
    color:#fff;
}

.tema-acougue .nome-produto{
    color:#fff;
}

.tema-acougue .topo-oferta{
    background:#e63946;
}

.tema-acougue .detalhe-produto{
    color:#ddd;
}

.tema-hortifruti{
    background:#fff94d;
    border-color:#28a745;
}

.tema-hortifruti .topo-oferta{
    background:#28a745;
}

.tema-hortifruti .valor-principal,
.tema-hortifruti .cifrão{
    color:#28a745;
}

/* TOPO */
.topo-oferta{
    width:105%;

    background:#e63946;
    color:#fff;

    text-align:center;

    padding:10px 0;

    text-transform:uppercase;

    font-family:'Anton', sans-serif;

    font-size:5rem;

    letter-spacing:3px;
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

/* NOME */
.nome-produto{
    font-family:'Anton', sans-serif;

    font-size:7rem;

    color:#111;

    text-transform:uppercase;

    text-align:center;

    line-height:.95;

    letter-spacing:2px;
}

/* DETALHE */
.detalhe-produto{
    margin-top:10px;

    font-family:'Bebas Neue', sans-serif;

    font-size:3rem;

    color:#444;

    text-align:center;

    letter-spacing:2px;
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
}

.valor-centavos{
    font-size:8rem;
    vertical-align:super;
}

/* DE / POR */
.preco-de{
    font-family:'Bebas Neue', sans-serif;

    font-size:3rem;

    color:#777;

    text-decoration:line-through;
}

/* ATACADO */
.bloco-atacado{
    display:flex;
    width:100%;

    justify-content:space-around;

    background:rgba(0,0,0,.05);

    padding:15px;

    border-radius:10px;
}

.unidade-varejo,
.unidade-atacado{
    font-family:'Bebas Neue', sans-serif;
    font-size:2rem;
    text-align:center;
}

.preco-box{
    font-size:4.5rem;
    color:#e63946;
    font-family:'Anton', sans-serif;
}

/* 4 CARTAZES */
.grade-4{
    width:210mm;
    height:297mm;

    display:grid;
    grid-template-columns:1fr 1fr;
    grid-template-rows:1fr 1fr;

    gap:10px;
}

.cartaz-mini{
    background:#ffde00;

    border:8px solid #e63946;

    padding:15px;

    display:flex;
    flex-direction:column;
    justify-content:space-between;
    align-items:center;
}

.cartaz-mini .topo-oferta{
    font-size:2rem;
    padding:5px 0;
}

.cartaz-mini .nome-produto{
    font-size:2.8rem;
}

.cartaz-mini .detalhe-produto{
    font-size:1.4rem;
}

.cartaz-mini .valor-principal{
    font-size:6rem;
}

.cartaz-mini .valor-centavos{
    font-size:3rem;
}

.cartaz-mini .cifrão{
    font-size:2rem;
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

    .cartaz-a4,
    .grade-4{
        box-shadow:none;
        page-break-after:always;

        -webkit-print-color-adjust:exact;
        print-color-adjust:exact;
    }

    @page{
        margin:0;
    }

}

</style>
</head>

<body>

<div id="painel-controle">

<h2>Painel Cartazista PRO</h2>

<label>Modelo do Cartaz</label>

<select id="modelo-cartaz">
    <option value="oferta">Oferta Tradicional</option>
    <option value="depor">Cartaz DE / POR</option>
    <option value="atacado">Atacado e Varejo</option>
    <option value="mini4">4 Cartazes Pequenos</option>
</select>

<label>Tema / Setor</label>

<select id="tema-setor">
    <option value="tema-padrao">Padrão</option>
    <option value="tema-acougue">Açougue</option>
    <option value="tema-hortifruti">Hortifruti</option>
</select>

<label>Orientação</label>

<select id="orientacao">
    <option value="em-pe">Em Pé</option>
    <option value="deitado">Deitado</option>
</select>

<label>Produtos</label>

<textarea id="entrada-dados">
ARROZ TIO JOÃO;PCT 5KG;24,99
FEIJÃO CAMIL;1KG;7,49
LEITE INTEGRAL;CX 1L;4,29
CAFÉ SANTA CLARA;250G;8,99
</textarea>

<button onclick="window.print()">
🖨️ Imprimir Cartazes
</button>

</div>

<div id="area-visualizacao"></div>

<script>

const inputDados = document.getElementById('entrada-dados');
const modelo = document.getElementById('modelo-cartaz');
const tema = document.getElementById('tema-setor');
const orientacao = document.getElementById('orientacao');
const area = document.getElementById('area-visualizacao');

function quebrarPreco(valor){

    if(!valor){
        return {r:'0', c:'00'};
    }

    let limpo = valor.replace('.', ',');

    if(limpo.includes(',')){

        let p = limpo.split(',');

        return{
            r:p[0],
            c:p[1].padEnd(2,'0').substring(0,2)
        };
    }

    return{
        r:limpo,
        c:'00'
    };
}

function cartazHTML(nome, detalhe, preco, temaAtual, orientacaoAtual){

    const p = quebrarPreco(preco);

    return `
    
    <div class="cartaz-a4 ${orientacaoAtual} ${temaAtual}">
    
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
                ${p.r}<span class="valor-centavos">,${p.c}</span>
            </div>

        </div>

    </div>

    `;
}

function renderizar(){

    area.innerHTML = '';

    const linhas = inputDados.value.trim().split('\n');

    /* 4 CARTAZES */

    if(modelo.value === 'mini4'){

        let html = `<div class="grade-4">`;

        linhas.slice(0,4).forEach(linha=>{

            const partes = linha.split(';');

            const nome = partes[0] || 'PRODUTO';
            const detalhe = partes[1] || '';
            const preco = quebrarPreco(partes[2] || '0,00');

            html += `

            <div class="cartaz-mini ${tema.value}">

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

        html += `</div>`;

        area.innerHTML = html;

        return;
    }

    linhas.forEach(linha=>{

        if(!linha.trim()) return;

        const partes = linha.split(';');

        const nome = partes[0] || 'PRODUTO';
        const detalhe = partes[1] || '';

        if(modelo.value === 'oferta'){

            area.innerHTML += cartazHTML(
                nome,
                detalhe,
                partes[2],
                tema.value,
                orientacao.value
            );
        }

        else if(modelo.value === 'depor'){

            const p = quebrarPreco(partes[3]);

            area.innerHTML += `

            <div class="cartaz-a4 ${orientacao.value} ${tema.value}">

                <div class="topo-oferta">
                    PROMOÇÃO
                </div>

                <div class="corpo-produto">

                    <div class="nome-produto">
                        ${nome}
                    </div>

                    <div class="detalhe-produto">
                        ${detalhe}
                    </div>

                </div>

                <div class="preco-de">
                    DE: R$ ${partes[2]}
                </div>

                <div class="bloco-preco">

                    <div class="cifrão">
                        POR R$
                    </div>

                    <div class="valor-principal">
                        ${p.r}<span class="valor-centavos">,${p.c}</span>
                    </div>

                </div>

            </div>

            `;
        }

        else if(modelo.value === 'atacado'){

            area.innerHTML += `

            <div class="cartaz-a4 ${orientacao.value} ${tema.value}">

                <div class="topo-oferta">
                    ATACADO E VAREJO
                </div>

                <div class="corpo-produto">

                    <div class="nome-produto">
                        ${nome}
                    </div>

                    <div class="detalhe-produto">
                        ${detalhe}
                    </div>

                </div>

                <div class="bloco-atacado">

                    <div class="unidade-varejo">
                        VAREJO<br>
                        <span class="preco-box">
                            R$ ${partes[2]}
                        </span>
                    </div>

                    <div class="unidade-atacado">
                        3 UN OU +<br>
                        <span class="preco-box">
                            R$ ${partes[3]}
                        </span>
                    </div>

                </div>

            </div>

            `;
        }

    });

}

inputDados.addEventListener('input', renderizar);

modelo.addEventListener('change', renderizar);

tema.addEventListener('change', renderizar);

orientacao.addEventListener('change', renderizar);

renderizar();

</script>

</body>
</html>
