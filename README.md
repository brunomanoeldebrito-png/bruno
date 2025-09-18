# bruno
impressão de boletos aquirvos etc...
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Impressão Rápida - Admin</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      background: #f1f2f6;
      font-family: 'Segoe UI', sans-serif;
      margin: 0;
      padding: 0;
    }
    header {
      background: #343a40;
      color: white;
      padding: 20px;
      text-align: center;
    }
    .container {
      max-width: 900px;
      margin: 30px auto;
      background: white;
      padding: 30px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    h2 {
      text-align: center;
      color: #333;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 10px;
      text-align: left;
    }
    th {
      background: #f0f0f0;
    }
    input[type="password"] {
      width: 200px;
      padding: 10px;
      margin-bottom: 20px;
    }
    button {
      padding: 10px 20px;
      background: #28a745;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background: #218838;
    }
    .hidden {
      display: none;
    }
  </style>
</head>
<body>
  <header>
    <h1>Impressão Rápida</h1>
    <p>🔒 Acesso Restrito - Painel de Agendamentos</p>
  </header>

  <div class="container">
    <div id="login">
      <h2>Digite a senha para acessar:</h2>
      <input type="password" id="senha" placeholder="Senha de acesso">
      <button onclick="verificarSenha()">Entrar</button>
      <p id="erro" style="color: red;"></p>
    </div>

    <div id="painel" class="hidden">
      <h2>Resumo de Agendamentos</h2>
      <table id="tabela">
        <thead>
          <tr>
            <th>Nome</th>
            <th>Serviço</th>
            <th>Qtd</th>
            <th>Data</th>
            <th>Horário</th>
            <th>Contato</th>
            <th>Pagamento</th>
            <th>Enviado em</th>
          </tr>
        </thead>
        <tbody></tbody>
      </table>
    </div>
  </div>

  <script>
    const SENHA_CORRETA = "secreto123"; // 🔒 Altere para sua senha

    function verificarSenha() {
      const senha = document.getElementById('senha').value;
      if (senha === SENHA_CORRETA) {
        document.getElementById('login').classList.add('hidden');
        document.getElementById('painel').classList.remove('hidden');
        carregarAgendamentos();
      } else {
        document.getElementById('erro').textContent = "Senha incorreta!";
      }
    }

    async function carregarAgendamentos() {
      const url = "COLE_AQUI_A_URL_DO_SEU_WEBAPP"; // ← Substitua pela URL do Google Apps Script

      try {
        const res = await fetch(url);
        const dados = await res.json();
        const tbody = document.querySelector("#tabela tbody");
        tbody.innerHTML = "";

        dados.forEach(agendamento => {
          const tr = document.createElement("tr");
          tr.innerHTML = `
            <td>${agendamento.Nome}</td>
            <td>${agendamento.Serviço}</td>
            <td>${agendamento.Quantidade}</td>
            <td>${agendamento.Data}</td>
            <td>${agendamento.Horário}</td>
            <td>${agendamento.Contato}</td>
            <td>${agendamento.Pagamento}</td>
            <td>${agendamento.DataHoraEnvio}</td>
          `;
          tbody.appendChild(tr);
        });
      } catch (err) {
        alert("Erro ao carregar dados.");
        console.error(err);
      }
    }
  </script>
</body>
</html>
