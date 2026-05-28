<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerador de Cartazes de Oferta</title>
    <style>
        /* Configurações de Design Gerais */
        body {
            font-family: 'Arial Black', Gadget, sans-serif;
            background-color: #f0f2f5;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: #fff;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }
        h1 {
            text-align: center;
            color: #0d6efd;
            margin-top: 0;
        }
        p {
            font-family: Arial, sans-serif;
            color: #666;
            line-height: 1.5;
        }
        textarea {
            width: 100%;
            height: 150px;
            padding: 12px;
            box-sizing: border-box;
            border: 2px solid #ccc;
            border-radius: 4px;
            font-size: 14px;
            resize: vertical;
            font-family: monospace;
        }
        button {
            background-color: #ffcc00;
            color: #000;
            border: none;
            padding: 15px 30px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
            border-radius: 4px;
            margin-top: 15px;
            transition: background 0.2s;
        }
        button:hover {
            background-color: #e6b800;
        }

        /* Área de Impressão dos Cartazes */
        #previewArea {
            margin-top: 30px;
        }
        .cartaz {
            background-color: #ffcc00; /* Cor amarela clássica de encarte */
            border: 15px solid #ff0000; /* Borda vermelha chamativa */
            border-radius: 10px;
            width: 100%;
            max-width: 500px;
            height: 700px;
            margin: 0 auto 40px auto;
            box-sizing: border-box;
            padding: 30px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
            text-align: center;
            text-transform: uppercase;
        }
        .topo-promocao {
            background-color: #ff0000;
            color: #fff;
            font-size: 38px;
            font-weight: 900;
            width: 105%;
            padding: 10px 0;
            margin-top: -15px;
            transform: rotate(-2deg);
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        .produto-nome {
            font-size: 42px;
            color: #000;
            line-height: 1.1;
            word-wrap: break-word;
            margin: auto 0;
            max-height: 250px;
            overflow: hidden;
        }
        .bloco-preco {
            width: 100%;
        }
        .cifrão {
            font-size: 32px;
            color: #ff0000;
            vertical-align: top;
            margin-right: 5px;
        }
        .preco-inteiro {
            font-size: 120px;
            color: #ff0000;
            line-height: 0.8;
            font-weight: 900;
        }
        .preco-centavos {
            font-size: 55px;
            color: #ff0000;
            vertical-align: top;
            line-height: 1;
        }

        /* Estilos de Ocultação para o Navegador vs Impressão */
        @media print {
            body {
                background: none;
                padding: 0;
            }
            .container {
                box-shadow: none;
                padding: 0;
                max-width: 100%;
            }
            .no-print {
                display: none !important;
            }
            .cartaz {
                margin: 0 auto;
                page-break-after: always; /* Quebra de página automática para cada cartaz */
                border-width: 25px;
                max-width: 100%;
                height: 98vh; /* Ocupa quase toda a folha A4 vertical */
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <div class="no-print">
            <h1>Gerador Automático de Cartazes</h1>
            <p>Cole sua lista de ofertas abaixo. Digite o <strong>nome do produto</strong> e o <strong>preço</strong> separados por vírgula (um item por linha).</p>
            <p><em>Exemplo:<br>Arroz Integral Tio João 5kg, 24.90<br>Leite Integral Piracanjuba 1L, 4.59</em></p>
            
            <textarea id="listaProdutos" placeholder="Produto Exemplo 1kg, 9.99&#10;Outro Produto Unid, 14.50"></textarea>
            <button onclick="gerarCartazes()">Gerar Cartazes e Imprimir</button>
        </div>

        <div id="previewArea"></div>
    </div>

    <script>
        function gerarCartazes() {
            const txt = document.getElementById('listaProdutos').value;
            const linhas = txt.split('\n');
            const previewArea = document.getElementById('previewArea');
            
            // Limpa gerações anteriores
            previewArea.innerHTML = '';
            let temCartaz = false;

            linhas.forEach(linha => {
                if (!linha.trim() || !linha.includes(',')) return;

                // Divide o nome do produto e o preço pela vírgula
                const partes = linha.split(',');
                const nome = partes[0].trim();
                const precoString = partes[1].trim();

                // Converte e valida o preço flutuante
                const precoNum = parseFloat(precoString.replace(/[^\d.]/g, ''));
                if (isNaN(precoNum)) return;

                temCartaz = true;

                // Separa reais de centavos para estilização grande do PDV
                const valorFixo = precoNum.toFixed(2);
                const [inteiro, centavos] = valorFixo.split('.');

                // Montagem da estrutura HTML do cartaz estruturado
                const cartazDiv = document.createElement('div');
                cartazDiv.className = 'cartaz';
                
                cartazDiv.innerHTML = `
                    <div class="topo-promocao">OFERTA</div>
                    <div class="produto-nome">${nome}</div>
                    <div class="bloco-preco">
                        <span class="cifrão">R$</span><span class="preco-inteiro">${inteiro}</span><span class="preco-centavos">,${centavos}</span>
                    </div>
                `;
                
                previewArea.appendChild(cartazDiv);
            });

            // Dispara o comando de impressão do sistema se houver conteúdo válido
            if (temCartaz) {
                // Pequeno delay para garantir que o DOM renderizou antes de abrir o gerenciador
                setTimeout(() => {
                    window.print();
                }, 300);
            } else {
                alert('Por favor, insira ao menos um produto válido com preço separado por vírgula.');
            }
        }
    </script>

</body>
</html>

