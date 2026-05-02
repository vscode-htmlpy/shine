<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Shine Ministério — Cadastro</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,700;1,400&family=Jost:wght@300;400;600;700&display=swap" rel="stylesheet" />
<link rel="stylesheet" type="text/css" href="style.css">
</head>
<body>
<iframe name="hidden_iframe" id="hidden_iframe" style="display:none;"></iframe>
<div class="wrapper">
  <div class="header">
    <span class="crown">👑</span>
    <div class="brand">Shine Ministério</div>
    <div class="tagline">Cadastro de participantes</div>
    <div class="signup-count" id="signupCount">Total de inscritos: 0</div>
  </div>
  <div class="card">
    <div class="section-title">Formulário de Cadastro</div>
    <form id="shineForm" action="https://script.google.com/macros/s/AKfycbz3chsvKmTlzpT-zzrvLiIZpoBm1atR_0aasteqkSTTU89W-9uE3yTiC-9v3555Mf0j/exec" method="POST" target="hidden_iframe">
      <div class="field">
        <label>Nome completo *</label>
        <input type="text" id="nome" name="nome" placeholder="Seu nome completo" />
        <div class="error-text" id="err-nome">Informe seu nome completo.</div>
      </div>
      <div class="row-2">
        <div class="field">
          <label>Aniversário *</label>
          <input type="date" id="aniversario" name="aniversario" />
          <div class="error-text" id="err-aniversario">Informe sua data de nascimento.</div>
        </div>
        <div class="field">
          <label>Idade</label>
          <input type="number" id="idade" name="idade" placeholder="Ex: 15" min="0" max="100" readonly />
        </div>
      </div>
      <div class="field">
        <label>WhatsApp *</label>
        <input type="tel" id="whatsapp" name="whatsapp" placeholder="(00) 00000-0000" />
        <div class="error-text" id="err-whatsapp">Informe um WhatsApp com DDD.</div>
      </div>
      <div class="field">
        <label>Nome do responsável *</label>
        <input type="text" id="responsavel" name="responsavel" placeholder="Pai, mãe ou responsável" />
        <div class="error-text" id="err-responsavel">Informe o nome do responsável.</div>
      </div>
      <div class="field">
        <label>Telefone do responsável</label>
        <input type="tel" id="telResponsavel" name="telResponsavel" placeholder="(00) 00000-0000" />
      </div>
      <div class="section-title">Grupo Supere</div>
      <div class="field">
        <label>Você tem grupo Supere? *</label>
        <div class="radio-group">
          <div class="radio-option">
            <input type="radio" id="supere-sim" name="supere" value="Sim" />
            <label for="supere-sim">✅ Sim</label>
          </div>
          <div class="radio-option">
            <input type="radio" id="supere-nao" name="supere" value="Não" />
            <label for="supere-nao">❌ Não</label>
          </div>
        </div>
        <div class="error-text" id="err-supere">Selecione uma opção.</div>
      </div>
      <div class="field conditional" id="liderField">
        <label>Líder do Grupo Supere</label>
        <input type="text" id="lider" name="lider" placeholder="Nome da líder do seu grupo" />
      </div>
      <input type="hidden" name="dataEnvio" id="dataEnvio" />
      <input type="hidden" name="horaEnvio" id="horaEnvio" />
      <button type="button" class="btn-submit" id="btnEnviar" onclick="enviar()">✨ Enviar Cadastro</button>
    </form>
    <div class="success-box" id="successBox">
      <div class="success-title">Já recebemos os seus dados!</div>
      <div class="success-text">Obrigada por se cadastrar. Seus dados foram enviados com sucesso.</div>
    </div>
  </div>

  <div class="chart-card" id="ageChartCard" style="display:none;">
    <div class="section-title">Gráfico de Idade</div>
    <div class="chart-note">Faixas etárias de quem já se inscreveu.</div>
    <div class="chart-wrapper" id="ageChartWrapper"></div>
  </div>

  <div class="admin-card">
    <div class="admin-title">Área Administrativa</div>
    <div class="admin-text">Insira a senha para acessar os cadastros armazenados localmente.</div>
    <div class="admin-row">
      <input type="password" id="adminPassword" placeholder="Senha administrativa" />
      <button type="button" class="btn-submit" id="adminBtn">Entrar</button>
    </div>
    <div class="error-text" id="err-admin">Senha incorreta. Tente novamente.</div>
    <div class="admin-result" id="adminResult">
      <div class="admin-note">Abaixo estão os cadastros salvos no navegador. Essa visualização funciona sem precisar do Excel.</div>
      <div class="admin-row" style="margin-bottom: 16px; align-items: center; justify-content: space-between; gap: 12px;">
        <button type="button" class="btn-submit" id="copyListBtn">Copiar lista</button>
        <span id="adminCount" style="font-size:13px;color:var(--texto-claro);font-weight:700;">Total de inscritos: 0</span>
      </div>
      <div class="admin-row" style="margin-bottom: 16px; align-items: center;">
        <span id="copyNotice" style="font-size:13px;color:var(--texto-claro);margin-left:0;display:none;">Lista copiada para a área de transferência.</span>
        <span id="adminStatus" style="font-size:13px;color:var(--texto-claro);margin-left:10px;display:none;"></span>
      </div>
      <div class="admin-table-wrapper">
        <table class="admin-table" id="adminTable">
          <thead>
            <tr>
              <th>Nome</th>
              <th>Aniversário</th>
              <th>Idade</th>
              <th>WhatsApp</th>
              <th>Responsável</th>
              <th>Telefone</th>
              <th>Supere</th>
              <th>Líder</th>
              <th>Data</th>
              <th>Hora</th>
              <th>Ações</th>
            </tr>
          </thead>
          <tbody id="adminTableBody"></tbody>
        </table>
      </div>
    </div>
  </div>

  <div class="footer">Feito com 💗 para o Shine Ministério</div>
</div>

<script src="app.js"></script>
</body>
</html>
