<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cartazista Profissional - Estilo Fiel</title>
    <style>
        /* --- IMPORTAÇÃO DE FONTES DIRECTAS CASO ESTEJA ONLINE (FALLBACK LOCAL CASO DESTACADO ANTES) --- */
        @import url('https://googleapis.com');
        
        @font-face { font-family: 'CartazistaPincel'; src: url('CaveatBrush-Regular.ttf') format('truetype'); }
        @font-face { font-family: 'CartazistaTitulo'; src: url('PermanentMarker-Regular.ttf') format('truetype'); }

        /* --- SISTEMA E INTERFACE DO USUÁRIO --- */
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: 'Segoe UI', sans-serif; background-color: #2c3e50; display: flex; height: 100vh; overflow: hidden; }
        
        #painel-controle {
            width: 380px; background-color: #1a1a1a; color: #fff; padding: 25px;
            display: flex; flex-direction: column; gap: 18px; box-shadow: 5px 0 15px rgba(0,0,0,0.5); z-index: 10;
        }
        h2 { color: #ffcc00; font-size: 1.3rem; border-bottom: 3px solid #ffcc00; padding-bottom: 8px; text-transform: uppercase; letter-spacing: 1px; }
        label { font-size: 0.8rem; color: #bbb; font-weight: bold; text-transform: uppercase; }
        select, textarea {
            width: 100%; background-color: #2b2b2b; color: #fff; border: 2px solid #444;
            padding: 12px; font-size: 0.95rem; border-radius: 6px; font-weight: bold;
        }
        select:focus, textarea:focus { outline: none; border-color: #ffcc00; }
        textarea { flex-grow: 1; font-family: monospace; resize: none; }
        .btn-imprimir {
            background: linear-gradient(to bottom, #ffcc00, #ff9900); color: #000; border: none; padding: 15px;
            font-size: 1.1rem; font-weight: 900; cursor: pointer; border-radius: 6px; text-transform: uppercase; box-shadow: 0 4px 6px rgba(0,0,0,0.3);
        }
        .btn-imprimir:hover { background: #ffcc00; }
        #area-visualizacao { flex-grow: 1; padding: 40px; overflow-y: auto; display: flex; flex-direction: column; align-items: center; gap: 50px; background-color: #4b6584; }

        /* --- O VERDADEIRO DESIGN CARTAZISTA.ONLINE (A4 VERTICAL) --- */
        .cartaz-a4 {
            width: 210mm; height: 297mm; background-color: #ffea00; border: 18px solid #ff0000;
            padding: 30px; box-shadow: 0 15px 35px rgba(0,0,0,0.6); display: flex;
            flex-direction: column; justify-content: space-between; align-items: center; position: relative; box-sizing: border-box;
            overflow: hidden;
        }
        
        /* Tema Açougue (Visual Escuro) */
        .tema-acougue { background-color: #111111; border-color: #c90000; }
        .tema-acougue .nome-produto { color: #ffffff !important; -webkit-text-stroke: 3px #000; }
        .tema-acougue .detalhe-produto { color: #ffea00 !important; }

        /* Elemento Splash/Selo de Oferta Idêntico ao Site */
        .selo-oferta {
            background: linear-gradient(135deg, #ff0000 0%, #cc0000 100%);
            color: #ffffff; font-family: 'Permanent Marker', 'CartazistaTitulo', sans-serif;
            font-size: 4.5rem; text-transform: uppercase; padding: 15px 80px;
            border-radius: 0 0 50px 50px; border: 6px solid #000; border-top: none;
            margin-top: -32px; font-weight: bold; letter-spacing: 3px;
            text-shadow: 4px 4px 0px #000; box-shadow: 0 8px 0px rgba(0,0,0,0.15);
        }

        /* Nome do Produto com visual de canetão */
        .corpo-produto {
            flex-grow: 1; display: flex; flex-direction: column; justify-content: center;
            align-items: center; width: 100%; text-align: center; margin-top: 20px;
        }
        .nome-produto {
            font-family: 'Caveat Brush', 'CartazistaPincel', sans-serif;
            font-size: 6.5rem; color: #000000; text-transform: uppercase;
            line-height: 0.95; font-weight: 900; max-width: 95%;
            word-wrap: break-word;
        }
        .detalhe-produto {
            font-family: 'Caveat Brush', 'CartazistaPincel', sans-serif;
            font-size: 3rem; color: #ff0000; text-transform: uppercase;
            font-weight: bold; margin-top: 15px; letter-spacing: 1px;
        }

        /* Bloco de Preço Gigante Varejista */
        .bloco-preco {
            display: flex; align-items: flex-start; justify-content: center;
            font-family: 'Caveat Brush', 'CartazistaPincel', sans-serif;
            color: #ff0000; font-weight: 900; position: relative; margin-bottom: 20px;
        }
        
        /* Contorno preto nos preços para simular profundidade de tinta */
        .bloco-preco {
            text-shadow: -3px -3px 0 #000, 3px -3px 0 #000, -3px 3px 0 #000, 3px 3px 0 #000;
        }

        .cifrão { font-size: 4.5rem; margin-top: 1.5rem; margin-right: 5px; }
        .valor-principal { font-size: 16rem; line-height: 0.75; letter-spacing: -6px; }
        .valor-centavos { font-size: 8rem; line-height: 0.75; margin-top: -10px; display: inline-block; vertical-align: super; }

        /* Estilos Específicos para DE / POR */
        .container-depor { display: flex; flex-direction: column; align-items: center; width: 100%; }
        .preco-de {
            font-family: 'Caveat Brush', sans-serif; font-size: 3.5rem; color: #333;
            text-decoration: line-through; text-shadow: none; margin-bottom: -10px; font-weight: bold;
        }
        .tema-acougue .preco-de { color: #bbb; }

        /* Rodapé de Encarte Padrão */
        .rodape-decorativo {
            width: 105%; height: 25px; background: repeating-linear-gradient( -45deg, #000, #000 15px, #ffea00 15px, #ffea00 30px );
            margin-bottom: -32px; border-top: 5px solid #000;
        }
        .tema-acougue .rodape-decorativo {
            background: repeating-linear-gradient( -45deg, #000, #000 15px, #ff0000 15px, #ff0000 30px );
        }

        /* --- COMPATIBILIDADE DE IMPRESSÃO --- */
        @media print {
            body { background: none; overflow: visible; }
            #painel-controle { display: none !important; }
            #area-visualizacao { padding: 0 !important; background: none !important; overflow: visible !important; display: block !important; }
            .cartaz-a4 { box-shadow: none !important; page-break-after: always !important; page-break-inside: avoid !important; -webkit-print-color-adjust: exact !important; print-color-adjust: exact !important; }
            @page { size: A4 portrait; margin: 0; }
        }
    </style>
</head>
<body>

    <div id="painel-controle">
        <h2>Cartazista Online Pro</h2>
        
        <label for="modelo-cartaz">Modelo Comercial</label>
        <select id="modelo-cartaz">
            <option value="oferta">Oferta Tradicional</option>
            <option value="depor">Selo DE / POR</option>
        </select>

        <label for="tema-setor">Estilo Visual</label>
        <select id="tema-setor">
            <option value="tema-padrao">Mercearia / Hortifruti (Amarelo)</option>
            <option value="tema-acougue">Açougue / Frios (Preto)</option>
        </select>

        <label id="label-instrucao">Produtos (Nome;Detalhe;Preço)</label>
        <textarea id="entrada-dados"></textarea>
        
        <button class="btn-imprimir" onclick="window.print()">🖨️ Imprimir Cartazes (A4)</button>
    </div>

    <div id="area-visualizacao"></div>

    <script>
        const inputDados = document.getElementById('entrada-dados');
        const selectModelo = document.getElementById('modelo-cartaz');
        const selectTema = document.getElementById('tema-setor');
        const areaVisualizacao = document.getElementById('area-visualizacao');

        function quebrarPreco(valor) {
            if (!valor) return { r: '0', c: '00' };
            let limpo = valor.trim().replace('.', ',');
            if (limpo.includes(',')) {
                let p = limpo.split(',');
                return { r: p[0], c: p[1].padEnd(2, '0').substring(0, 2) };
            }
            return { r: limpo, c: '00' };
        }

        function renderizar() {
            areaVisualizacao.innerHTML = '';
            const modelo = selectModelo.value;
            const tema = selectTema.value;
            const linhas = inputDados.value.trim().split('\n');

            linhas.forEach(linha => {
                if (!linha.trim()) return;
                const partes = linha.split(';');
                
                let htmlCartaz = '';
                const classeLayout = `cartaz-a4 ${tema}`;

                if (modelo === 'oferta') {
                    const nome = partes[0] || 'PRODUTO';
                    const detalhe = partes[1] || '';
                    const p = quebrarPreco(partes[2]);
                    
                    htmlCartaz = `
                        <div class="${classeLayout}">
                            <div class="selo-oferta">Oferta</div>
                            <div class="corpo-produto">
                                <div class="nome-produto">${nome}</div>
                                <div class="detalhe-produto">${detalhe}</div>
                            </div>
                            <div class="bloco-preco">
                                <span class="cifrão">R$</span>
                                <span class="valor-principal">${p.r}</span><span class="valor-centavos">,${p.c}</span>
                            </div>
                            <div class="rodape-decorativo"></div>
                        </div>`;
                } 
                else if (modelo === 'depor') {
                    const nome = partes[0] || 'PRODUTO';
                    const detalhe = partes[1] || '';
                    const precoDe = partes[2] || '0,00';
                    const pPor = quebrarPreco(partes[3]);

                    htmlCartaz = `
                        <div class="${classeLayout}">
                            <div class="selo-oferta">Só Hoje</div>
                            <div class="corpo-produto">
                                <div class="nome-produto">${nome}</div>
                                <div class="detalhe-produto">${detalhe}</div>
                            </div>
                            <div class="container-depor">
                                <div class="preco-de">DE: R$ ${precoDe}</div>
                                <div class="bloco-preco">
                                    <span class="cifrão">POR R$</span>
                                    <span class="valor-principal">${pPor.r}</span><span class="valor-centavos">,${pPor.c}</span>
                                </div>
                            </div>
                            <div class="rodape-decorativo"></div>
                        </div>`;
                }

                areaVisualizacao.innerHTML += htmlCartaz;
            });
        }

        inputDados.addEventListener('input', renderizar);
        selectModelo.addEventListener('change', () => {
            if(selectModelo.value === 'depor') {
                inputDados.value = "SABÃO EM PÓ OMO;LAVAGEM PERFEITA 1.6KG;24,90;19,98";
            } else {
                inputDados.value = "ARROZ TIO JOÃO;TIPO 1 - PCT 5KG;24,99\nCOXÃO MOLE BOVINO;KG;34,90";
            }
            renderizar();
        });
        selectTema.addEventListener('change', renderizar);

        // Inicialização
        inputDados.value = "ARROZ TIO JOÃO;TIPO 1 - PCT 5KG;24,99\nCOXÃO MOLE BOVINO;KG;32,98";
        renderizar();
    </script>
</body>
</html>
