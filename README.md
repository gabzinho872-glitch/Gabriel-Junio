<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minha Cantina - Sistema de Pedidos</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }
        body {
            background-color: #f4f6f8;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            padding: 25px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        h1, h2 {
            color: #1a2a3a;
        }
        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 25px;
        }
        .item-card {
            border: 1px solid #e0e0e0;
            padding: 15px;
            border-radius: 6px;
            text-align: center;
            background: #fafafa;
        }
        .item-card h3 {
            margin: 0 0 10px 0;
            font-size: 1.1rem;
        }
        .price {
            font-weight: bold;
            color: #2e7d32;
            margin-bottom: 10px;
        }
        button {
            background-color: #0066cc;
            color: white;
            border: none;
            padding: 8px 12px;
            border-radius: 4px;
            cursor: pointer;
            transition: background 0.2s;
        }
        button:hover {
            background-color: #004b99;
        }
        .order-summary {
            border-top: 2px solid #eee;
            padding-top: 15px;
        }
        ul {
            list-style: none;
            padding: 0;
        }
        li {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #f0f0f0;
        }
        .total {
            font-size: 1.2rem;
            font-weight: bold;
            text-align: right;
            margin-top: 15px;
        }
        .btn-finish {
            width: 100%;
            padding: 12px;
            background-color: #2e7d32;
            font-size: 1rem;
            margin-top: 15px;
        }
        .btn-finish:hover {
            background-color: #1b5e20;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Cantina Escolar 🥪</h1>
    <p>Escolha os produtos e faça o seu pedido abaixo:</p>

    <h2>Menu</h2>
    <div class="menu-grid">
        <div class="item-card">
            <h3>Salgado Assado</h3>
            <div class="price">R$ 5,00</div>
            <button onclick="adicionarItem('Salgado Assado', 5.00)">Adicionar</button>
        </div>
        <div class="item-card">
            <h3>Sumo Natural</h3>
            <div class="price">R$ 4,00</div>
            <button onclick="adicionarItem('Sumo Natural', 4.00)">Adicionar</button>
        </div>
        <div class="item-card">
            <h3>Sanduíche Natural</h3>
            <div class="price">R$ 7,50</div>
            <button onclick="adicionarItem('Sanduíche Natural', 7.50)">Adicionar</button>
        </div>
        <div class="item-card">
            <h3>Fruta da Época</h3>
            <div class="price">R$ 2,00</div>
            <button onclick="adicionarItem('Fruta da Época', 2.00)">Adicionar</button>
        </div>
    </div>

    <div class="order-summary">
        <h2>Resumo do Pedido</h2>
        <ul id="lista-carrinho">
            <li><em>Nenhum item selecionado.</em></li>
        </ul>
        <div class="total">Total: R$ <span id="valor-total">0.00</span></div>
        <button class="btn-finish" onclick="finalizarPedido()">Finalizar Pedido</button>
    </div>
</div>

<script>
    let carrinho = [];
    let total = 0;

    function adicionarItem(nome, preco) {
        carrinho.push({ nome, preco });
        total += preco;
        atualizarCarrinho();
    }

    function atualizarCarrinho() {
        const lista = document.getElementById('lista-carrinho');
        const totalElemento = document.getElementById('valor-total');
        
        lista.innerHTML = '';
        
        if (carrinho.length === 0) {
            lista.innerHTML = '<li><em>Nenhum item selecionado.</em></li>';
        } else {
            carrinho.forEach((item, index) => {
                const li = document.createElement('li');
                li.innerHTML = `${item.nome} - R$ ${item.preco.toFixed(2)} 
                    <button style="background:#cc0000; padding:2px 6px;" onclick="removerItem(${index})">X</button>`;
                lista.appendChild(li);
            });
        }
        
        totalElemento.innerText = total.toFixed(2);
    }

    function removerItem(index) {
        total -= carrinho[index].preco;
        carrinho.splice(index, 1);
        atualizarCarrinho();
    }

    function finalizarPedido() {
        if (carrinho.length === 0) {
            alert('Adicione pelo menos um item antes de finalizar!');
            return;
        }
        alert(`Pedido confirmado! Total a pagar: R$ ${total.toFixed(2)}`);
        carrinho = [];
        total = 0;
        atualizarCarrinho();
    }
</script>

</body>
</html>
