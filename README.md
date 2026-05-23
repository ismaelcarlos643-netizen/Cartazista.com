<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerador de Cartaz de Supermercado</title>
    <style>
        /* Configurações de Cores e Estilo Geral */
        :root {
            --cor-fundo: #FFD700; /* Amarelo Limão/Varejo */
            --cor-detalhe: #D32F2F; /* Vermelho Oferta */
            --cor-texto: #000000;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Arial Black', Impact, sans-serif;
        }

        body {
            background-color: #f0f2f5;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        /* Painel de Controle (Sumiço na Impressão) */
        #painel-controle {
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            margin-bottom: 30px;
            width: 100%;
            max-width: 500px;
        }

        .campo {
            margin-bottom: 15px;
        }

        .campo label {
            display: block;
            margin-bottom: 5px;
            font-size: 14px;
            color: #333;
            font-family: Arial, sans-serif;
        }

        .campo input {
            width: 100%;
            padding: 10px;
            font-size: 16px;
            border: 2px solid #ccc;
            border-radius: 4px;
            font-family: Arial, sans-serif;
        }

        button {
            width: 100%;
            background-color: var(--cor-detalhe);
            color: white;
            border: none;
            padding: 12px;
            font-size: 16px;
            font-weight: bold;
            border-radius: 4px;
            cursor: pointer;
            transition: background 0.2s;
        }

        button:hover {
            background-color: #b71c1c;
        }

        /* Área do Cartaz - Proporção A4 Vertical */
        .area-cartaz {
            background-color: #fff;
            padding: 10px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.15);
        }

        #cartaz {
            width: 210mm;
            height: 297mm;
            background-color: var(--cor-fundo);
            border: 15px solid var(--cor-detalhe);
            padding: 30px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        /* Elementos Visuais do Cartaz */
        .Selo-oferta {
            background-color: var(--cor-detalhe);
            color: #fff;
            padding: 15px 60px;
            font-size: 45px;
            text-transform: uppercase;
            letter-spacing: 2px;
            transform: skewX(-10deg);
            border-radius: 5px;
            box-shadow: 5px 5px 0px #000;
            margin-top: 10px;
        }

        #exibicao-produto {
            font-size: 55px;
            color: var(--cor-texto);
            text-transform: uppercase;
            line-height: 1.1;
            margin: 40px 0;
            word-wrap: break-word;
            max-width: 100%;
            display: -webkit-box;
            -webkit-line-clamp: 3;
            -webkit-box-orient: vertical;
        }

        /* Bloco de Preço Padrão de Supermercado */
        .bloco-preco {
            display: flex;
            align-items: flex-start;
            justify-content: center;
            color: var(--cor-detalhe);
            text-shadow: 3px 3px 0px #000;
            margin-bottom: 20px;
        }

        .cifrao {
            font-size: 70px;
            margin-top: 20px;
            margin-right: 5px;
        }

        .reais {
            font-size: 240px;
            line-height: 0.8;
            letter-spacing: -5px;
        }

        .coluna-centavos {
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            margin-left: 5px;
        }

        .centavos {
            font-size: 100px;
            line-height: 0.8;
            border-bottom: 8px solid var(--cor-detalhe);
            padding-bottom: 5px;
        }

        #exibicao-unidade {
            font-size: 35px;
            color: var(--cor-texto);
            text-transform: uppercase;
            text-shadow: none;
            margin-top: 10px;
        }

        /* Configuração Estrita de Impressão */
        @media print {
            body {
                background-color: #fff;
                padding: 0;
            }
            #painel-controle {
                display: none; /* Esconde as ferramentas */
            }
            .area-cartaz {
                box-shadow: none;
                padding: 0;
            }
            #cartaz {
                width: 210mm;
                height: 297mm;
                border: 15px solid var(--cor-detalhe);
                -webkit-print-color-adjust: exact; /* Força o navegador a imprimir as cores de fundo */
                print-color-adjust: exact;
            }
        }
    </style>
</head>
<body>

    <div id="painel-controle">
        <div class="campo">
            <label for="input-produto">Nome do Produto</label>
            <input type="text" id="input-produto" value="Arroz Integral Tipo 1 Tio João 5kg" oninput="atualizarCartaz()">
        </div>
        <div class="campo">
            <label for="input-reais">Preço (Apenas Reais)</label>
            <input type="number" id="input-reais" value="24" oninput="atualizarCartaz()">
        </div>
        <div class="campo">
            <label for="input-centavos">Centavos</label>
            <input type="text" id="input-centavos" value="98" maxlength="2" oninput="atualizarCartaz()">
        </div>
        <div class="campo">
            <label for="input-unidade">Unidade de Medida (Ex: KG, UN, LITRO)</label>
            <input type="text" id="input-unidade" value="Cada" oninput="atualizarCartaz()">
        </div>
        <button onclick="window.print()">Imprimir Cartaz (A4)</button>
    </div>

    <div class="area-cartaz">
        <div id="cartaz">
            <div class="Selo-oferta">Oferta!</div>
            
            <div id="exibicao-produto">Arroz Integral Tipo 1 Tio João 5kg</div>
            
            <div class="bloco-preco">
                <span class="cifrao">R$</span>
                <span class="reais" id="exibicao-reais">24</span>
                <div class="coluna-centavos">
                    <span class="centavos" id="exibicao-centavos">98</span>
                    <span id="exibicao-unidade">Cada</span>
                </div>
            </div>
        </div>
    </div>

    <script>
        function atualizarCartaz() {
            const produto = document.getElementById('input-produto').value;
            const reais = document.getElementById('input-reais').value || '0';
            let centavos = document.getElementById('input-centavos').value || '00';
            const unidade = document.getElementById('input-unidade').value;

            // Garante que os centavos sempre tenham 2 dígitos visuais se o usuário digitar apenas 1
            if(centavos.length === 1) centavos = centavos + '0';

            document.getElementById('exibicao-produto').innerText = produto;
            document.getElementById('exibicao-reais').innerText = reais;
            document.getElementById('exibicao-centavos').innerText = centavos;
            document.getElementById('exibicao-unidade').innerText = unidade;
        }
    </script>
</body>
</html>
