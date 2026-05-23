<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cartaz Fácil - Clone</title>
    <style>
        /* --- CONFIGURAÇÕES GERAIS DO SISTEMA --- */
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Arial', sans-serif; }
        body { background: #f0f2f5; color: #333; display: flex; height: 100vh; overflow: hidden; }
        
        /* Layout Principal */
        .sidebar { width: 380px; background: #fff; border-right: 1px solid #dcdfe6; padding: 18px; display: flex; flex-direction: column; gap: 14px; overflow-y: auto; box-shadow: 2px 0 10px rgba(0,0,0,0.05); }
        .main-content { flex: 1; display: flex; flex-direction: column; background: #eef1f6; overflow: hidden; }
        
        /* Topo Azul do Sistema */
        .system-header { background: #006699; color: #fff; padding: 12px 20px; font-weight: bold; font-size: 1.1rem; display: flex; align-items: center; justify-content: center; gap: 5px; }
        .system-header span { border: 1px solid #fff; padding: 2px 6px; font-size: 0.8rem; border-radius: 3px; }
        
        .preview-container { flex: 1; padding: 30px; display: flex; justify-content: center; align-items: center; overflow: auto; }

        /* Componentes de Formulário */
        h2 { font-size: 1.1rem; color: #444; border-bottom: 2px solid #ccc; padding-bottom: 5px; margin-bottom: 5px; }
        .form-group { display: flex; flex-direction: column; gap: 4px; }
        label { font-size: 0.8rem; font-weight: bold; color: #555; }
        input, select { padding: 9px; border: 1px solid #c0c4cc; border-radius: 4px; font-size: 0.85rem; outline: none; background: #fafafa; }
        input:focus, select:focus { border-color: #006699; background: #fff; }
        
        /* Grid de Modelos (Igual Imagem 3) */
        .format-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 8px; max-height: 250px; overflow-y: auto; padding-right: 5px; }
        .format-card { border: 1px solid #dcdfe6; border-radius: 4px; padding: 6px; text-align: center; cursor: pointer; background: #fff; font-size: 0.7rem; font-weight: bold; color: #666; transition: 0.2s; }
        .format-card:hover { border-color: #006699; background: #f4f9fc; }
        .format-card.active { border-color: #e6a23c; background: #fffdf5; color: #d48806; box-shadow: 0 0 0 1px #e6a23c; }
        .mini-preview { height: 35px; border: 1px solid #ddd; background: #fff; margin: 0 auto 4px auto; position: relative; border-radius: 2px; overflow: hidden; }
        .mini-header { height: 8px; background: #e30613; width: 100%; }
        
        /* Botões de Controle (Igual Imagem 2 e 3) */
        .btn-bar { display: flex; gap: 8px; margin-top: 10px; }
        .btn { padding: 12px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; font-size: 0.85rem; display: flex; align-items: center; justify-content: center; gap: 5px; color: white; }
        .btn-add { background: #f5bc3e; }
        .btn-print { background: #1a73e8; flex: 2; }
        .btn-lock { background: #67c23a; width: 50px; }
        
        /* -------------------------------------------------------------
           ESTILOS DOS CARTAZES (Fiel à Imagem 4)
        ------------------------------------------------------------- */
        .cartaz-wrapper { display: grid; gap: 30px; justify-content: center; padding: 20px; }
        
        .cartaz-box { background: white; box-shadow: 0 10px 30px rgba(0,0,0,0.1); box-sizing: border-box; position: relative; display: flex; flex-direction: column; align-items: center; border: 1px solid #ddd; page-break-inside: avoid; }

        /* Metadados Técnicos do Topo (Barra Verde/Azul na Imagem 4) */
        .cartaz-meta { width: 100%; height: 18px; background: #f0f0f0; border-bottom: 1px solid #ddd; display: flex; align-items: center; justify-content: space-between; padding: 0 8px; font-size: 0.6rem; color: #666; font-weight: bold; }
        .meta-tag { background: #00a65a; color: white; padding: 1px 4px; border-radius: 2px; font-size: 0.55rem; }

        /* Cabeçalho da Campanha */
        .cartaz-header { width: calc(100% - 24px); background: #e30613; color: #fff; text-align: center; padding: 12px 0; font-weight: 900; font-size: 2.2rem; text-transform: uppercase; letter-spacing: 1px; border-bottom: 5px solid #ffed00; margin-top: 12px; font-style: italic; }
        
        /* Conteúdo do Cartaz */
        .cartaz-produto { font-size: 1.35rem; font-weight: 800; color: #000; text-transform: uppercase; text-align: center; width: 90%; margin-top: 25px; line-height: 1.3; min-height: 52px; word-wrap: break-word; display: flex; align-items: center; justify-content: center; }
        .cartaz-unidade { font-size: 0.65rem; font-weight: bold; color: #444; width: 90%; text-align: left; margin-top: 30px; letter-spacing: 0.5px; }
        
        /* Bloco de Preço Magnificado */
        .cartaz-preco { display: flex; align-items: flex-start; justify-content: center; color: #e30613; font-weight: 900; margin-top: -5px; }
        .preco-inteiro { font-size: 8rem; line-height: 0.8; letter-spacing: -4px; }
        .preco-centavos { font-size: 3.3rem; line-height: 0.85; margin-top: 4px; margin-left: 1px; }
        
        /* Faixa Vermelha de Rodapé */
        .cartaz-footer-stripe { position: absolute; bottom: 12px; left: 12px; width: calc(100% - 24px); height: 8px; background: #e30613; }

        /* --- MEDIDAS DOS FORMATOS (PROPORÇÃO REAL) --- */
        .A3-RETRATO { width: 420px; height: 594px; }
        .A3-PAISAGEM { width: 594px; height: 420px; }
        .A4-RETRATO { width: 297px; height: 420px; }
        .A4-PAISAGEM { width: 420px; height: 297px; }
        .A5-RETRATO { width: 210px; height: 297px; }
        .A5-PAISAGEM { width: 297px; height: 210px; }
        .A6-RETRATO { width: 148px; height: 210px; }
        .A6-PAISAGEM { width: 210px; height: 148px; }
        .DUPLO-A3 { width: 840px; height: 594px; }

        /* Ajustes específicos para layouts Deitados (Paisagem) */
        .A3-PAISAGEM .cartaz-produto, .A4-PAISAGEM .cartaz-produto { margin-top: 15px; }
        .A3-PAISAGEM .preco-inteiro, .A4-PAISAGEM .preco-inteiro { font-size: 7rem; }

        /* --- SCRIPT DE IMPRESSÃO --- */
        @media print {
            body * { visibility: hidden; }
            .preview-container, .preview-container * { visibility: visible; }
            .preview-container { position: absolute; left: 0; top: 0; width: 100%; background: white; padding: 0; overflow: visible; }
            .cartaz-box { box-shadow: none; border: none; margin-bottom: 20px; }
            .cartaz-meta { display: none; } /* Oculta linha técnica na impressão final */
        }
    </style>
</head>
<body>

    <!-- Painel Lateral -->
    <div class="sidebar">
        <h2>Criação de Cartazes</h2>
        
        <div class="form-group">
            <label>Selecione a filial:</label>
            <select id="filial">
                <option>527 - Porto Alegre</option>
                <option>102 - Curitiba</option>
            </select>
        </div>

        <div class="form-group">
            <label>1 - Insira o nome do produto / marca:</label>
            <input type="text" id="inpNome" value="ARROZ BCO LF T1 SEPÉ 5KG">
        </div>

        <h2>Dados Balizagem</h2>

        <div class="form-group">
            <label>3 - Selecione Valor do Produto:</label>
            <input type="text" id="inpPreco" value="19,90">
        </div>

        <div class="form-group">
            <label>4 - Selecione a Campanha:</label>
            <select id="inpCampanha">
                <option value="OFERTA">OFERTA</option>
                <option value="ACOUGUE">ACOUGUE</option>
                <option value="HORTIFRUTI">HORTIFRUTI</option>
                <option value="DIA R">DIA R</option>
                <option value="SABADAO DAS FRALDAS">SABADÃO DAS FRALDAS</option>
            </select>
        </div>

        <div class="form-group">
            <label>5 - Selecione Formato / modelo:</label>
            <div class="format-grid">
                <div class="format-card" data-format="A3-PAISAGEM"><div class="mini-preview" style="width:45px;"><div class="mini-header"></div></div>A3 PAISAGEM</div>
                <div class="format-card active" data-format="A4-RETRATO"><div class="mini-preview" style="width:30px;"><div class="mini-header"></div></div>A4 RETRATO</div>
                <div class="format-card" data-format="A4-PAISAGEM"><div class="mini-preview" style="width:45px;"><div class="mini-header"></div></div>A4 PAISAGEM</div>
                <div class="format-card" data-format="A3-RETRATO"><div class="mini-preview" style="width:30px;"><div class="mini-header"></div></div>A3 RETRATO</div>
                <div class="format-card" data-format="A5-RETRATO"><div class="mini-preview" style="width:25px;"><div class="mini-header"></div></div>A5 RETRATO</div>
                <div class="format-card" data-format="A5-PAISAGEM"><div class="mini-preview" style="width:35px;"><div class="mini-header"></div></div>A5 PAISAGEM</div>
                <div class="format-card" data-format="A6-RETRATO"><div class="mini-preview" style="width:20px;"><div class="mini-header"></div></div>A6 RETRATO</div>
                <div class="format-card" data-format="DUPLO-A3"><div class="mini-preview" style="width:50px; background:#fbe9e7;"><div class="mini-header"></div></div>DUPLO A3</div>
            </div>
        </div>

        <div class="form-group">
            <label>Quantidade de cópias na folha:</label>
            <select id="inpCopias">
                <option value="4">4 Unidades (Igual imagem 4)</option>
                <option value="1">1 Unidade Única</option>
                <option value="2">2 Unidades</option>
            </select>
        </div>

        <div class="btn-bar">
        
