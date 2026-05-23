
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PreçoPlay - Gerador de Cartazes Profissional</title>
    <style>
        :root {
            --amarelo-preco-play: #FFAA00;
            --vermelho-preco-play: #D50000;
            --preto-borda: #000000;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background-color: #1e222b;
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }

        /* --- PAINEL DE CONTROLE (Sumiço na Impressão) --- */
        #painel-controle {
            background: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
            margin-bottom: 25px;
            width: 100%;
            max-width: 500px;
            z-index: 10;
        }

        .campo {
            margin-bottom: 12px;
        }

        .campo label {
            display: block;
            margin-bottom: 4px;
            font-size: 13px;
            font-weight: bold;
            color: #333;
        }

        .campo input {
            width: 100%;
            padding: 10px;
            font-size: 15px;
            border: 2px solid #bdc3c7;
            border-radius: 4px;
        }

        .campo input:focus {
            border-color: var(--vermelho-preco-play);
            outline: none;
        }

        button {
            width: 100%;
            background: var(--vermelho-preco-play);
            color: white;
            border: none;
            padding: 12px;
            font-size: 16px;
            font-weight: bold;
            border-radius: 4px;
            cursor: pointer;
            text-transform: uppercase;
        }

        button:hover {
            background: #b30000;
        }

        /* --- O CARTAZ (Estilo Autêntico PreçoPlay) --- */
        .preview-area {
            background: #fff;
            padding: 5px;
            box-shadow: 0 15px 40px rgba(0,0,0,0.5);
        }

        #cartaz-a4 {
            width: 210mm;
            height: 297mm;
            background-color: var(--amarelo-preco-play);
            border: 14px solid var(--vermelho-preco-play);
            padding: 30px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: space-between;
            position: relative;
            overflow: hidden;
            box-shadow: inset 0 0 0 6px #ffffff; /* Linha branca interna clássica */
        }

        /* Header de Oferta Inclinado */
        .tag-oferta {
            background: var(--vermelho-preco-play);
            color: #ffffff;
            font-family: 'Impact', sans-serif;
            font-size: 80px;
            font-weight: bold;
            text-transform: uppercase;
            padding: 10px 90px;
            letter-spacing: 4px;
            transform: rotate(-3deg) skewX(-10deg);
            box-shadow: 8px 8px 0px var(--preto-borda);
            border: 4px solid #ffffff;
            margin-top: 15px;
            text-shadow: 3px 3px 0px var(--preto-borda);
        }

        /* Nome do Produto Centralizado com Destaque */
        .bloco-produto {
            width: 100%;
            text-align: center;
            margin: 20px 0;
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 180px;
        }

        #exibir-produto {
            font-family: 'Impact', 'Arial Black', sans-serif;
            font-size: 70px;
            color: #ffffff;
            text-transform: uppercase;
            line-height: 0.95;
            letter-spacing: 1px;
            /* Efeito de contorno preto grosso de cartazeiro manual */
            text-shadow: 
                -4px -4px 0 var(--preto-borda),  
                 4px -4px 0 var(--preto-borda),
                -4px  4px 0 var(--preto-borda),
                 4px  4px 0 var(--preto-borda),
                 6px  8px 0px rgba(0,0,0,0.4);
            word-wrap: break-word;
            max-width: 95%;
        }

        /* Bloco de Preço Gigante do Varejo */
        .bloco-preco {
            display: flex;
            justify-content: center;
            align-items: flex-start;
            font-family: 'Impact', sans-serif;
            color: var(--vermelho-preco-play);
            /* Sombra projetada no preço */
            filter: drop-shadow(6px 6px 0px var(--preto-borda));
            margin-bottom: 25px;
        }

        .cifrao {
            font-size: 90px;
            margin-top: 15px;
            margin-right: 2px;
            letter-spacing: -5px;
        }

        .reais {
            font-size: 330px;
            line-height: 0.72;
            letter-spacing: -12px;
            font-weight: 900;
        }

        .lado-centavos {
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            margin-left: 5px;
            margin-top: -5px;
        }

        .centavos {
            font-size: 140px;
            line-height: 0.75;
            font-weight: 900;
            letter-spacing: -4px;
            border-bottom: 14px solid var(--vermelho-preco-play);
            padding-bottom: 2px;
        }

        .unidade {
            font-family: 'Arial Black', sans-serif;
            font-size: 35px;
            color: var(--preto-borda);
            text-transform: uppercase;
            margin-top: 15px;
            font-weight: bold;
            letter-spacing: -1px;
        }

        /* Rodapé com Grafismo de Faixas */
        .rodape-decorativo {
            width: 105%;
            height: 25px;
            background: repeating-linear-stripes(
                -45deg,
                var(--vermelho-preco-play),
                var(--vermelho-preco-play) 20px,
                #ffffff 20px,
                #ffffff 40px
            );
            margin-bottom: -15px;
            border-top: 4px solid var(--preto-borda);
        }

        /* --- CONFIGURAÇÃO DE IMPRESSÃO A4 --- */
        @media print {
            body {
                background: #fff;
                padding: 0;
            }
            #painel-controle {
                display: none;
            }
            .preview-area {
                padding: 0;
                box-shadow: none;
            }
            #cartaz-a4 {
                width: 210mm;
                height: 297mm;
                -webkit-print-color-adjust: exact;
                print-color-adjust: exact;
            }
        }
    </style>
</head>
<body>

    <div id="painel-controle">
        <div class="campo">
            <label for="input-prod">Nome do Produto (Letras Garrafais)</label>
            <input type="text" id="input-prod" value="SABÃO EM PÓ OMO LAVAGEM PERFEITA 1,6KG" oninput="atualizarGrade()">
        </div>
        <div class="campo">
            <label for="input-reais">Preço (Inteiro)</label>
            <input type="number" id="input-reais" value="19" oninput="atualizarGrade()">
        </div>
        <div class="campo">
            <label for="input-centavos">Centavos</label>
            <input type="text" id="input-centavos" value="98" maxlength="2" oninput="atualizarGrade()">
        </div>
        <div class="campo">
            <label for="input-unidade">Unidade (Ex: CADA, KG, UN)</label>
            <input type="text" id="input-unidade" value="CADA" oninput="atualizarGrade()">
        </div>
        <button onclick="window.print()">Imprimir Cartaz A4</button>
    </div>

    <div class="preview-area">
        <div id="cartaz-a4">
            <!-- Selo Superior -->
            <div class="tag-oferta">OFERTA</div>
            
            <!-- Nome do Produto -->
            <div class="bloco-produto">
                <h1 id="exibir-produto">SABÃO EM PÓ OMO LAVAGEM PERFEITA 1,6KG</h1>
            </div>
            
            <!-- Preço Estilo PreçoPlay -->
            <div class="bloco-preco">
                <span class="cifrao">R$</span>
                <span class="reais" id="exibir-reais">19</span>
                <div class="lado-centavos">
                    <span class="centavos" id="exibir-centavos">98</span>
                    <span class="unidade" id="exibir-unidade">CADA</span>
                </div>
            </div>

            <!-- Faixa listrada de rodapé para fechar o layout -->
            <div class="rodape-decorativo"></div>
        </div>
    </div>

    <script>
        function atualizarGrade() {
            const produto = document.getElementById('input-prod').value;
            const reais = document.getElementById('input-reais').value || '0';
            let centavos = document.getElementById('input-centavos').value || '00';
            const unidade = document.getElementById('input-unidade').value;

            if(centavos.length === 1) centavos = centavos + '0';

            document.getElementById('exibir-produto').innerText = produto;
            document.getElementById('exibir-reais').innerText = reais;
            document.getElementById('exibir-centavos').innerText = centavos;
            document.getElementById('exibir-unidade').innerText = unidade;
        }
    </script>
</body>
</html>

