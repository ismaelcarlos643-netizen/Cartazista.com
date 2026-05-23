<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PreçoPlay - Gerador de Placa de Oferta</title>
    <style>
        :root {
            --amarelo-varejo: #FFEA00;
            --vermelho-oferta: #E53935;
            --preto-texto: #1A1A1A;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background-color: #e0e4e8;
            font-family: 'Arial Black', Impact, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 30px;
        }

        /* --- PAINEL DE CONTROLE (Desaparece na impressão) --- */
        #painel-config {
            background: #ffffff;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 8px 24px rgba(0,0,0,0.15);
            margin-bottom: 30px;
            width: 100%;
            max-width: 480px;
        }

        #painel-config h2 {
            font-family: Arial, sans-serif;
            font-size: 18px;
            margin-bottom: 15px;
            color: #333;
            text-align: center;
        }

        .grupo-input {
            margin-bottom: 15px;
        }

        .grupo-input label {
            display: block;
            margin-bottom: 6px;
            font-size: 13px;
            color: #555;
            font-family: Arial, sans-serif;
            font-weight: bold;
        }

        .grupo-input input {
            width: 100%;
            padding: 12px;
            font-size: 16px;
            border: 2px solid #ccd1d9;
            border-radius: 6px;
            font-family: Arial, sans-serif;
            transition: border-color 0.2s;
        }

        .grupo-input input:focus {
            border-color: var(--vermelho-oferta);
            outline: none;
        }

        .btn-imprimir {
            width: 100%;
            background-color: var(--vermelho-oferta);
            color: white;
            border: none;
            padding: 14px;
            font-size: 16px;
            font-weight: bold;
            border-radius: 6px;
            cursor: pointer;
            box-shadow: 0 4px 12px rgba(229, 57, 53, 0.3);
            transition: transform 0.1s, background 0.2s;
        }

        .btn-imprimir:hover {
            background-color: #c62828;
            transform: translateY(-1px);
        }

        /* --- ESTRUTURA DA PLACA (Estilo PreçoPlay) --- */
        .preview-container {
            background: #fff;
            padding: 10px;
            box-shadow: 0 12px 36px rgba(0,0,0,0.2);
        }

        #placa-preco {
            width: 210mm;
            height: 297mm;
            background-color: var(--amarelo-varejo);
            border: 18px solid var(--vermelho-oferta);
            padding: 40px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
            position: relative;
            overflow: hidden;
        }

        /* Tarja de Oferta Superior */
        .topo-oferta {
            background-color: var(--vermelho-oferta);
            color: #ffffff;
            font-size: 55px;
            padding: 15px 70px;
            text-transform: uppercase;
            letter-spacing: 3px;
            transform: skewX(-12deg);
            border-radius: 4px;
            box-shadow: 6px 6px 0px var(--preto-texto);
            margin-top: 15px;
            text-shadow: 2px 2px 0px rgba(0,0,0,0.3);
        }

        /* Nome do Produto */
        .container-produto {
            flex-grow: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            max-height: 35%;
            width: 100%;
            margin: 30px 0;
        }

        #txt-produto {
            font-size: 60px;
            color: var(--preto-texto);
            text-transform: uppercase;
            line-height: 1.1;
            text-align: center;
            word-wrap: break-word;
            display: -webkit-box;
            -webkit-line-clamp: 3;
            -webkit-box-orient: vertical;
            overflow: hidden;
        }

        /* Bloco de Preço Gigante */
        .container-preco {
            display: flex;
            justify-content: center;
            align-items: flex-start;
            color: var(--vermelho-oferta);
            filter: drop-shadow(4px 4px 0px var(--preto-texto));
            margin-bottom: 40px;
        }

        .cifrao {
            font-size: 80px;
            margin-top: 25px;
            margin-right: 10px;
        }

        .reais {
            font-size: 260px;
            line-height: 0.75;
            letter-spacing: -8px;
        }

        .col-centavos {
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            margin-left: 10px;
        }

        .centavos {
            font-size: 110px;
            line-height: 0.8;
            border-bottom: 10px solid var(--vermelho-oferta);
            padding-bottom: 5px;
            font-weight: 900;
        }

        .unidade {
            font-size: 38px;
            color: var(--preto-texto);
            text-transform: uppercase;
            margin-top: 15px;
            font-family: 'Arial Black', sans-serif;
        }

        /* --- REGRAS PARA IMPRESSÃO (A4) --- */
        @media print {
            body {
                background: #fff;
                padding: 0;
            }
            #painel-config {
                display: none; /* Esconde as configurações ao imprimir */
            }
            .preview-container {
                padding: 0;
                box-shadow: none;
            }
            #placa-preco {
                width: 210mm;
                height: 297mm;
                border: 18px solid var(--vermelho-oferta);
                -webkit-print-color-adjust: exact;
                print-color-adjust: exact;
            }
        }
    </style>
</head>
<body>

    <div id="painel-config">
        <h2>PreçoPlay - Gerador Comercial</h2>
        <div class="grupo-input">
            <label for="input-prod">Descrição do Produto</label>
            <input type="text" id="input-prod" value="Café Melitta Vácuo 500g" oninput="renderPlaca()">
        </div>
        <div class="grupo-input">
            <label for="input-rs">Valor (Reais)</label>
            <input type="number" id="input-rs" value="18" oninput="renderPlaca()">
        </div>
        <div class="grupo-input">
            <label for="input-cts">Centavos</label>
            <input type="text" id="input-cts" value="95" maxlength="2" oninput="renderPlaca()">
        </div>
        <div class="grupo-input">
            <label for="input-uni">Medida (Ex: UN, KG, LT)</label>
            <input type="text" id="input-uni" value="UN" oninput="renderPlaca()">
        </div>
        <button class="btn-imprimir" onclick="window.print()">Gerar & Imprimir Placa</button>
    </div>

    <div class="preview-container">
        <div id="placa-preco">
            <div class="topo-oferta">Oferta</div>
            
            <div class="container-produto">
                <h1 id="txt-produto">Café Melitta Vácuo 500g</h1>
            </div>
            
            <div class="container-preco">
                <span class="cifrao">R$</span>
                <span class="reais" id="txt-reais">18</span>
                <div class="col-centavos">
                    <span class="centavos" id="txt-centavos">95</span>
                    <span class="unidade" id="txt-unidade">UN</span>
                </div>
            </div>
        </div>
    </div>

    <script>
        function renderPlaca() {
            const produto = document.getElementById('input-prod').value;
            const reais = document.getElementById('input-rs').value || '0';
            let centavos = document.getElementById('input-cts').value || '00';
            const unidade = document.getElementById('input-uni').value;

            // Ajuste automático caso o usuário digite apenas 1 dígito nos centavos
            if (centavos.length === 1) centavos = centavos + '0';

            document.getElementById('txt-produto').innerText = produto;
            document.getElementById('txt-reais').innerText = reais;
            document.getElementById('txt-centavos').innerText = centavos;
            document.getElementById('txt-unidade').innerText = unidade;
        }
    </script>
</body>
</html>
