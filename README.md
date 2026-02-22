<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Banco Digital</title>

<style>
    body {
        margin: 0;
        background: #0f172a;
        font-family: 'Segoe UI', sans-serif;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
    }

    .phone {
        width: 360px;
        height: 640px;
        background: #020617;
        border-radius: 30px;
        overflow: hidden;
        box-shadow: 0 0 40px rgba(0,0,0,0.8);
        display: flex;
        flex-direction: column;
    }

    .header {
        background: linear-gradient(135deg, #2563eb, #1e40af);
        padding: 20px;
        color: white;
    }

    .header h2 {
        margin: 0;
    }

    .balance {
        font-size: 26px;
        margin-top: 10px;
    }

    .content {
        flex: 1;
        padding: 15px;
        color: white;
        overflow-y: auto;
    }

    .card {
        background: #1e293b;
        padding: 15px;
        border-radius: 15px;
        margin-bottom: 10px;
    }

    .actions {
        display: flex;
        justify-content: space-around;
        margin-top: 10px;
    }

    .actions button {
        padding: 10px;
        border: none;
        border-radius: 10px;
        background: #2563eb;
        color: white;
        cursor: pointer;
    }

    .transaction {
        border-bottom: 1px solid #334155;
        padding: 8px 0;
    }

    .login {
        padding: 30px;
        text-align: center;
        color: white;
    }

    input {
        padding: 10px;
        width: 80%;
        margin: 10px 0;
        border-radius: 10px;
        border: none;
    }

    button.login-btn {
        padding: 10px 20px;
        border: none;
        border-radius: 10px;
        background: #22c55e;
        color: white;
        cursor: pointer;
    }
</style>
</head>

<body>

<div class="phone">

    <!-- LOGIN -->
    <div id="loginScreen" class="login">
        <h2>Banco Digital</h2>
        <input type="password" id="pin" placeholder="Digite seu PIN">
        <br>
        <button class="login-btn" onclick="login()">Entrar</button>
        <p id="loginMsg"></p>
    </div>

    <!-- APP -->
    <div id="appScreen" style="display:none; flex:1; flex-direction:column;">

        <div class="header">
            <h2>Olá, Cliente</h2>
            <div class="balance" id="balance">R$ 0,00</div>
        </div>

        <div class="content">

            <div class="card">
                <strong>Ações</strong>
                <div class="actions">
                    <button onclick="showPix()">PIX</button>
                    <button onclick="showTransfer()">Transferir</button>
                    <button onclick="deposit()">Depositar</button>
                </div>
            </div>

            <div class="card">
                <strong>Extrato</strong>
                <div id="transactions"></div>
            </div>

        </div>
    </div>

</div>

<script>
let saldo = 2500;
let transactions = [
    {text: "Supermercado", value: -120},
    {text: "Salário", value: 3000},
    {text: "Netflix", value: -39}
];

function updateUI() {
    document.getElementById("balance").innerText = "R$ " + saldo;

    let list = "";
    transactions.slice().reverse().forEach(t => {
        list += `<div class="transaction">
            ${t.text} - R$ ${t.value}
        </div>`;
    });

    document.getElementById("transactions").innerHTML = list;
}

function login() {
    let pin = document.getElementById("pin").value;

    if (pin === "1234") {
        document.getElementById("loginScreen").style.display = "none";
        document.getElementById("appScreen").style.display = "flex";
        updateUI();
    } else {
        document.getElementById("loginMsg").innerText = "PIN incorreto";
    }
}

function showPix() {
    let valor = prompt("Valor do PIX:");
    if (!valor) return;

    saldo -= parseFloat(valor);
    transactions.push({text: "PIX enviado", value: -valor});
    updateUI();
}

function showTransfer() {
    let valor = prompt("Valor da transferência:");
    if (!valor) return;

    saldo -= parseFloat(valor);
    transactions.push({text: "Transferência", value: -valor});
    updateUI();
}

function deposit() {
    let valor = prompt("Valor do depósito:");
    if (!valor) return;

    saldo += parseFloat(valor);
    transactions.push({text: "Depósito", value: +valor});
    updateUI();
}
</script>

</body>
</html># Banco-
