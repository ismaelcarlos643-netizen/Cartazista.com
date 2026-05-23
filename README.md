<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerador de Cartaz Offline</title>
    <style>
        /* ==========================================================================
           1. ESTILO DA INTERFACE (O que aparece na tela do computador)
           ========================================================================== */
        body {
            font-family: 'Arial Black', Arial, sans-serif;
            background-color: #f0f2f5;
            margin: 0;
            padding: 20px;
            display: flex;
            gap: 30px;
        }

        /* Painel de controle do lado esquerdo */
        .painel-controle {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            width: 300px;
            height: fit-content;
        }

        .painel-controle h2 {
            margin-top: 0;
            color: #333;
            font-size: 20px;
        }

        .campo {
            margin-bottom: 15px;
        }

        .campo label {
            display: block;
            margin-bottom: 5px;
            color: #666;
            font-size: 14px;
        }

        .campo input, .campo select {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
            font-size: 16px;
        }

        .btn-imprimir {
            width: 100%;
            background-color: #00cc66;
            color: white;
            border: none;
            padding: 12px;
            font-size: 16px;
            font-weight: bold;
            border-radius: 4px;
            cursor: pointer;
            transition: 0.2s;
        }

        .btn-imprimir:hover {
            background-color: #009951;
        }

        /* Área de visualização do cartaz na tela */
        .area-preview {
            flex-grow: 1;
            display: flex;
            justify-content: center;
        }

        /* ==========================================================================
           2. ESTILO DO CARTAZ (Simula uma folha A4 em pé)
           ========================================================================== */
        .cartaz-folha {
            width: 210mm;
            height: 297mm;
            background-color: #ffe600; /* Amarelo forte de mercado */
            border: 10mm solid #e60000; /* Borda vermelha grossa */
            box-sizing: border-box;
            padding: 15mm;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            text-align: center;
            box-shadow: 0 10px 20px rgba(0,0,0,0.15);
            text-transform: uppercase;
        }

        .topo-alerta {
            color: #e60000;
            font-size: 45px;
            letter-spacing: 2px;
            margin: 0;
        }

        .nome-produto {
            color: #000;
            font-size: 55px;
            line-height: 1.1;
            word-wrap: break-word;
            margin: 20px 0;
            flex-grow: 1;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .bloco-preco {
            background-color: #e60000;
            color: #ffe600;
            padding: 15px;
            border-radius: 10px;
        }

        .cifrão {
            font-size: 40px;
            vertical-align: super;
        }

        .valor {
            font-size: 140px;
            line-height: 1;
        }

        /* ==========================================================================
           3. CÓDIGO DA IMPRESSÃO (O que vai para a impressora)
           ========================================================================== */
        @media print {
            /* Esconde a barra de ferramentas inteira */
            .painel-controle {
                display: none !important;
            }
            
            body {
                background: none;
                padding: 0;
                margin: 0;
            }

            .area-preview {
                margin: 0;
                padding: 0;
            }

            /* Força o cartaz a ocupar a folha inteira sem sombras */
            .cartaz-folha {
                box-shadow: none;
                margin: 0;
                page-break-inside: avoid;
            }
        }
    </style>
</head>
<body>

    <!-- Lado Esquerdo: Formulário -->
    <div class="painel-controle">
        <h2>Gerador de Cartaz</h2>
        
        <div class="campo">
            <label>Tipo de Oferta:</label>
            <input type="text" id="inputTopo" value="OFERTA IMBATÍVEL" oninput="atualizar()">
        </div>

        <div class="campo">
            <label>Nome do Produto:</label>
            <input type="text" id="inputProduto" value="SABÃO EM PÓ OMO 1KG" oninput="atualizar()">
        </div>

        <div class="campo">
            <label>Preço (R$):</label>
            <input type="text" id="inputPreco" value="14,99" oninput="atualizar()">
        </div>

        <button class="btn-imprimir" onclick="window.print()">Imprimir Cartaz</button>
    </div>

    <!-- Lado Direito: O Cartaz A4 -->
    <div class="area-preview">
        <div class="cartaz-folha">
            <h1 class="topo-alerta" id="viewTopo">OFERTA IMBATÍVEL</h1>
            <div class="nome-produto" id="viewProduto">SABÃO EM PÓ OMO 1KG</div>
            <div class="bloco-preco">
                <span class="cifrão">R$</span>
                <span class="valor" id="viewPreco">14,99</span>
            </div>
        </div>
    </div>

    <!-- Lógica JavaScript que atualiza a folha em tempo real -->
    <script>
        function atualizar() {
            const topo = document.getElementById('inputTopo').value;
            const produto = document.getElementById('inputProduto').value;
            const preco = document.getElementById('inputPreco').value;

            document.getElementById('viewTopo').innerText = topo || "OFERTA";
            document.getElementById('viewProduto').innerText = produto || "NOME DO PRODUTO";
            document.getElementById('viewPreco').innerText = preco || "0,00";
        }
    </script>

</body>
</html>
