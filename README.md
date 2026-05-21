<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerador Multi-Modelos de Cartazes (Estilo Cartazista.online)</title>
    <style>
        /* --- FONTES LOCAIS --- */
        @font-face { font-family: 'CartazistaPincel'; src: url('CaveatBrush-Regular.ttf') format('truetype'); }
        @font-face { font-family: 'CartazistaTitulo'; src: url('PermanentMarker-Regular.ttf') format('truetype'); }

        /* --- LAYOUT DO SISTEMA --- */
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: 'Segoe UI', sans-serif; background-color: #333; display: flex; height: 100vh; overflow: hidden; }
        
        #painel-controle {
            width: 400px; background-color: #1e1e24; color: #fff; padding: 20px;
            display: flex; flex-direction: column; gap: 15px; box-shadow: 4px 0 10px rgba(0,0,0,0.5); z-index: 10; overflow-y: auto;
        }
        h2 { color: #ffcc00; font-size: 1.2rem; border-bottom: 2px solid #ffcc00; padding-bottom: 5px; }
        label { font-size: 0.85rem; color: #aaa; font-weight: bold; margin-bottom: -5px; }
        select, textarea {
            width: 100%; background-color: #2d2d34; color: #fff; border: 1px solid #444;
            padding: 10px; font-size: 0.9rem; border-radius: 4px;
        }
        select:focus, textarea:focus { outline: 2px solid #ffcc00; }
        textarea { flex-grow: 1; font-family: monospace; resize: none; min-height: 150px; }
        .btn-imprimir {
            background-color: #28a745; color: white; border: none; padding: 12px;
            font-size: 1rem; font-weight: bold; cursor: pointer; border-radius: 4px; transition: 0.2s;
        }
        .btn-imprimir:hover { background-color: #218838; }
        
        #area-visualizacao {
            flex-grow: 1; padding: 30px; overflow-y: auto; display: flex; flex-direction: column; align-items: center; gap: 40px;
        }

        /* --- ESTILOS BASE DOS CARTAZES (RETRAITO A4) --- */
        .cartaz-a4 {
            width: 210mm; height: 297mm; background-color: #ffde00; border: 15px solid #e63946;
            padding: 30px; box-shadow: 0 10px 25px rgba(0,0,0,0.5); display: flex;
            flex-direction: column; justify-content: space-between; align-items: center; position: relative; box-sizing: border-box;
        }
        
        /* Variação Paisagem (Deitado) */
        .cartaz-a4.deitado { width: 297mm; height: 210mm; }

        /* --- TEMAS (SETORIZAÇÃO) --- */
        .tema-padrao { background-color: #ffde00; border-color: #e63946; }
        .tema-acougue { background-color: #111; border-color: #e63946; color: #fff; }
        .tema-acougue .nome-produto { color: #fff; }
        .tema-acougue .topo-oferta { background-color: #e63946; color: #fff; }
        .tema-hortifruti { background-color: #ffde00; border-color: #28a745; }
        .tema-hortifruti .topo-oferta { background-color: #28a745; }
        .tema-hortifruti .valor-principal, .tema-hortifruti .cifrão { color: #28a745; }

        /* --- ELEMENTOS DO DESIGN --- */
        .topo-oferta {
            font-family: 'CartazistaTitulo', sans-serif; background-color: #e63946; color: #fff;
            width: 105%; text-transform: uppercase; font-size: 3.5rem; text-align: center; padding: 10px 0; margin-top: -10px;
        }
        .corpo-produto { flex-grow: 1; display: flex; flex-direction: column; justify-content: center; align-items: center; width: 100%; }
        .nome-produto { font-family: 'CartazistaPincel', sans-serif; font-size: 4.5rem; color: #111; text-transform: uppercase; line-height: 1.1; }
        .detalhe-produto { font-family: 'CartazistaPincel', sans-serif; font-size: 2.2rem; color: #555; text-transform: uppercase; margin-top: 5px; }
        
        /* Elementos específicos de Preço */
        .bloco-preco { display: flex; flex-direction: column; align-items: center; margin-bottom: 10px; }
        .cifrão { font-family: 'CartazistaTitulo', sans-serif; font-size: 2.5rem; color: #e63946; margin-bottom: -15px; }
        .valor-principal { font-family: 'CartazistaPincel', sans-serif; font-size: 10rem; color: #e63946; line-height: 0.85; }
        .valor-centavos { font-size: 5.5rem; vertical-align: super; }

        /* Estilos do modelo DE / POR */
        .preco-de { font-family: 'CartazistaPincel', sans-serif; font-size: 2.5rem; color: #666; text-decoration: line-through; margin-bottom: 10px; }
        .tema-acougue .preco-de { color: #aaa; }

        /* Estilos do modelo Atacado/Varejo */
        .bloco-atacado { display: flex; width: 100%; justify-content: space-around; background: rgba(0,0,0,0.05); padding: 15px; border-radius: 10px; }
        .unidade-varejo, .unidade-atacado { font-family: 'CartazistaPincel', sans-serif; font-size: 2rem; }
        .preco-box { font-size: 4rem; color: #e63946; font-family: 'CartazistaPincel', sans-serif; }

        /* --- ENGINE DE IMPRESSÃO --- */
        @media print {
            body { background: none; overflow: visible; }
            #painel-controle { display: none !important; }
            #area-visualizacao { padding: 0 !important; background: none !important; overflow: visible !important; display: block !important; }
            .cartaz-a4 { box-shadow: none !important; page-break-after: always !important; page-break-inside: avoid !important; -webkit-print-color-adjust: exact !important; print-color-adjust: exact !important; }
            @page { margin: 0; }
            .cartaz-a4.em-pe { size: A4 portrait; }
            .cartaz-a4.deitado { size: A4 landscape; }
        }
    </style>
</head>
<body>

    <div id="painel-controle">
        <h2>Painel Cartazista</h2>
        
        <label for="modelo-cartaz">Modelo do Cartaz</label>
        <select id="modelo-cartaz">
            <option value="oferta">Oferta Tradicional</option>
            <option value="depor">Cartaz DE / POR</option>
            <option value="atacado">Atacado e Varejo</option>
            <option value="bolsao">Modo Bolsão (2 Folhas)</option>
        </select>

        <label for="tema-setor">Tema / Setor</label>
        <select id="tema-setor">
            <option value="tema-padrao">Padrão (Amarelo/Vermelho)</option>
            <option value="tema-acougue">Açougue (Preto/Vermelho)</option>
            <option value="tema-hortifruti">Hortifruti (Amarelo/Verde)</option>
        </select>

        <label for="orientacao">Orientação da Folha</label>
        <select id="orientacao">
            <option value="em-pe">Em Pé (Retrato)</option>
            <option value="deitado">Deitado (Paisagem)</option>
        </select>

        <label id="label-instrucao">Dados dos Produtos (Separados por ';')</label>
        <textarea id="entrada-dados"></textarea>
        
        <button class="btn-imprimir" onclick="window.print()">🖨️ Gerar e Imprimir</button>
    </div>

    <div id="area-visualizacao"></div>

    <script>
        const inputDados = document.getElementById('entrada-dados');
        const selectModelo = document.getElementById('modelo-cartaz');
        const selectTema = document.getElementById('tema-setor');
        const selectOrientacao = document.getElementById('orientacao');
        const areaVisualizacao = document.getElementById('area-visualizacao');
        const labelInstrucao = document.getElementById('label-instrucao');

        // Textos de instrução dinâmicos baseados no modelo escolhido
        const placeholders = {
            oferta: "Produto;Detalhe;Preço\nEx: ARROZ TIO JOÃO;PCT 5KG;24,99",
            depor: "Produto;Detalhe;Preço Regular;Preço Oferta\nEx: FEIJÃO CAMIL;1KG;8,99;6,49",
            atacado: "Produto;Detalhe;Preço Varejo;Preço Atacado\nEx: REFRIGERANTE COCA COLA;PET 2L;8,99;7,99",
            bolsao: "Produto;Detalhe;Preço\nEx: SABÃO EM PÓ OMO;LAVAGEM PERFEITA 1.6KG;19,90"
        };

        function atualizarPlaceholder() {
            const mod = selectModelo.value;
            labelInstrucao.innerHTML = `Padrão de entrada para este modelo:<br><strong>${placeholders[mod].split('\n')[0]}</strong>`;
            renderizar();
        }

        function quebrarPreco(valor) {
            if (!valor) return { r: '0', c: '00' };
            let limpo = valor.replace('.', ',');
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
            const orientacao = selectOrientacao.value;
            const linhas = inputDados.value.trim().split('\n');

            linhas.forEach(linha => {
                if (!linha.trim()) return;
                const partes = linha.split(';');
                
                let htmlCartaz = '';
                const classeLayout = `cartaz-a4 ${orientacao} ${tema}`;

                if (modelo === 'oferta') {
                    const nome = partes[0] || 'PRODUTO';
                    const detalhe = partes[1] || '';
                    const p = quebrarPreco(partes[2]);
                    
                    htmlCartaz = `
                        <div class="${classeLayout}">
                            <div class="topo-oferta">Oferta</div>
                            <div class="corpo-produto">
                                <div class="nome-produto">${nome}</div>
                                <div class="detalhe-produto">${detalhe}</div>
                            </div>
                            <div class="bloco-preco">
                                <span class="cifrão">R$</span>
                                <div class="valor-principal">${p.r}<span class="valor-centavos">,${p.c}</span></div>
                            </div>
                        </div>`;
                } 
                else if (modelo === 'depor') {
                    const nome = partes[0] || 'PRODUTO';
                    const detalhe = partes[1] || '';
                    const pDe = partes[2] || '0,00';
                    const pPor = quebrarPreco(partes[3]);

                    htmlCartaz = `
                        <div class="${classeLayout}">
                            <div class="topo-oferta">Promoção</div>
                            <div class="corpo-produto">
                                <div class="nome-produto">${nome}</div>
                                <div class="detalhe-produto">${detalhe}</div>
                            </div>
                            <div class="preco-de">De: R$ ${pDe}</div>
                            <div class="bloco-preco">
                                <span class="cifrão">Por R$</span>
                                <div class="valor-principal">${pPor.r}<span class="valor-centavos">,${pPor.c}</span></div>
                            </div>
                        </div>`;
                }
                else if (modelo === 'atacado') {
                    const nome = partes[0] || 'PRODUTO';
                    const detalhe = partes[1] || '';
                    const pVar = partes[2] || '0,00';
                    const pAtac = partes[3] || '0,00';

                    htmlCartaz = `
                        <div class="${classeLayout}">
                            <div class="topo-oferta">Atacado e Varejo</div>
                            <div class="corpo-produto">
                                <div class="nome-produto">${nome}</div>
                                <div class="detalhe-produto">${detalhe}</div>
                            </div>
                            <div class="bloco-atacado">
                                <div class="unidade-varejo">Varejo Unit.<br><span class="preco-box">R$ ${pVar}</span></div>
                                <div class="unidade-atacado">A partir de 3 un.<br><span class="preco-box">R$ ${pAtac}</span></div>
                            </div>
                        </div>`;
                }
                else if (modelo === 'bolsao') {
                    const nome = partes[0] || 'PRODUTO';
                    const detalhe = partes[1] || '';
                    const p = quebrarPreco(partes[2]);

                    // O modo Bolsão gera DUAS folhas separadas consecutivas para o mesmo item
                    htmlCartaz = `
                        <!-- Folha 1: Nome do Produto -->
                        <div class="${classeLayout}">
                            <div class="topo-oferta">Oferta Especial</div>
                            <div class="corpo-produto">
                                <div class="nome-produto" style="font-size: 6rem;">${nome}</div>
                                <div class="detalhe-produto" style="font-size: 3rem;">${detalhe}</div>
                            </div>
                        </div>
                        <!-- Folha 2: Apenas o Preço Gigante -->
                        <div class="${classeLayout}">
                            <div class="topo-oferta">Preço do Dia</div>
                            <div class="corpo-produto">
                                <div class="bloco-preco">
                                    <span class="cifrão" style="font-size: 4rem;">R$</span>
                                    <div class="valor-principal" style="font-size: 15rem;">${p.r}<span class="valor-centavos" style="font-size: 8rem;">,${p.c}</span></div>
                                </div>
                            </div>
                        </div>`;
                }

                areaVisualizacao.innerHTML += htmlCartaz;
            });
        }

        // Eventos para atualização dinâmica na tela
        inputDados.addEventListener('input', renderizar);
        selectModelo.addEventListener('change', () => { atualizarPlaceholder(); inputDados.value = placeholders[selectModelo.value].split('\n').slice(1).join('\n'); renderizar(); });
        selectTema.addEventListener('change', renderizar);
        selectOrientacao.addEventListener('change', renderizar);

        // Estado inicial do sistema
        selectModelo.value = 'oferta';
        inputDados.value = "ARROZ TIO JOÃO;PCT 5KG;24,99\nFEIJÃO CAMIL;1KG;7,49\nLEITE INTEGRAL;CX 1L;4,29";
        atualizarPlaceholder();
    </script>
</body>
</html>
