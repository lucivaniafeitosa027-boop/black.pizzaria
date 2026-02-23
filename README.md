<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <title>Black Pizzaria | Portal VIP</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        :root { --ouro: #D4AF37; --preto: #050505; }
        body { background: var(--preto); color: #fff; font-family: sans-serif; overflow-x: hidden; }
        .card-black { background: #111; border: 1px solid #222; border-radius: 12px; padding: 18px; }
        .gold-text { color: var(--ouro); }
        .btn-gold { background: var(--ouro); color: #000; font-weight: bold; border-radius: 6px; padding: 10px; width: 100%; cursor: pointer; border: none; transition: 0.3s; }
        .btn-gold:active { transform: scale(0.95); opacity: 0.8; }
        .aba-ativa { border-bottom: 2px solid var(--ouro); color: var(--ouro); font-weight: bold; }
        input, select { background: #181818 !important; border: 1px solid #333 !important; color: white !important; outline: none; }
        
        .step { display: none; overflow-y: auto; max-height: 70vh; }
        .step.active { display: block; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        
        @keyframes scaleIn { from { transform: scale(0); opacity: 0; } to { transform: scale(1); opacity: 1; } }
        .success-icon { animation: scaleIn 0.5s ease-out forwards; }
    </style>
</head>
<body>

<script>
    const NOME_PIZZARIA = "BLACK PIZZARIA";
    const WHATSAPP_NUMERO = "5511982416568"; 
    const CHAVE_PIX = "5511982416568";

    const TAXAS_ENTREGA = {
        "Vila Rosina": 4.00,
        "Centro (Caieiras)": 5.00,
        "Laranjeiras": 7.00,
        "Serpa": 6.00,
        "Portal das Laranjeiras": 8.00,
        "Vera Tereza": 7.00,
        "Jardim dos Eucaliptos": 8.00,
        "Melhoramentos": 6.00,
        "Morro do Grande": 9.00,
        "Perus": 10.00
    };

    const PRODUTOS = [
        { id: 99, nome: "PIZZA MEIO A MEIO", preco: 65.00, categoria: "Tradicionais", descricao: "ESCOLHA DOIS SABORES (Exceto Gourmet).", especial: "meio-a-meio" },
        { id: 1, nome: "Black", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, CALABRESA, PRESUNTO, BACON, AZEITONA, CEBOLA , TOMATE E ORÉGANO." },
        { id: 2, nome: "PORTUGUESA", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, PRESUNTO, OVO, BACON, PALMITO, AZEITONA,CEBOLA, TOMATE E OREGANO." },
        { id: 3, nome: "NAPOLITANA", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, CALABRESA, FRANGO, BACON, CEBOLA, TOMATE E OREGANO." },
        { id: 4, nome: "BACON", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, BACON, AZEITONA, CEBOLA, TOMATE E OREGANO." },
        { id: 5, nome: "CALABRESA", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, CALABRESA, AZEITONA, CEBOLA,TOMATE E OREGANO.." },
        { id: 6, nome: "MUSSARELA", preco: 50.00, categoria: "Tradicionais", descricao: " MOLHO, MUSSARELA, AZEITONA, CEBOLA, TOMATE E ORÉGANO." },
        { id: 7, nome: "FRANGO COM CATUPIRY ", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, FRANGO, AZEITONA, CATUPIRY, CEBOLA, TOMATE E OREGANO.." },
        { id: 10, nome: "MODA DA CASA", preco: 65.00, categoria: "Gourmet", descricao: "MOLHO, MUSSARELA, CALABRESA, PRESUNTO, FRANGO, OVO, ERVILHA, AZEITONA, CEBOLA, TOMATE E OREGANO." },
        { id: 12, nome: "MALUCA DOIS RECHEIOS", preco: 80.00, categoria: "Gourmet", descricao: "MOLHO, MUSSARELA, CATUPIRY, CALABRESA, PRESUNTO, FRANGO, OVO, MILHO, AZEITONA, CEBOLA, TOMATE, ORÉGANO E DUAS MASSAS.." },
        { id: 11, nome: "CARNE COM CHEDDAR", preco: 60.00, categoria: "Gourmet", descricao: "MOLHO, MUSSARELA, CARNE, CHEDDAR, PIMENTÃO, AZEITONA, CEBOLA, TOMATE E OREGANO.." },
        { id: 13, nome: "BANANA", preco: 40.00, categoria: "Doces", descricao: "BANANA, LEITE CONDENSADO e CANELA EM PÓ." },
        { id: 14, nome: "Coca-Cola 2L", preco: 15.00, categoria: "Bebidas", descricao: "Gelada." },
        { id: 15, nome: "FANTA LARANJA 2L", preco: 15.00, categoria: "Bebidas", descricao: "Gelada." },
        { id: 16, nome: "guarana antarctica 2l", preco: 15.00, categoria: "Bebidas", descricao: "Gelada." },
        { id: 17, nome: "Borda de Catupiry", preco: 8.00, categoria: "Adicionais", descricao: "Borda recheada artesanal." },
        { id: 18, nome: "Borda de cheddar", preco: 8.00, categoria: "Adicionais", descricao: "Borda recheada artesanal." },
        { id: 19, nome: "catupiry com bacon", preco: 15.00, categoria: "Adicionais", descricao: "Borda recheada artesanal." },
        { id: 20, nome: "frango com catupiry", preco: 15.00, categoria: "Adicionais", descricao: "Borda recheada artesanal." },
        { id: 21, nome: "calabresa com cheddar", preco: 15.00, categoria: "Adicionais", descricao: "Borda recheada artesanal." },
        { id: 22, nome: "mussarela com catupiry", preco: 15.00, categoria: "Adicionais", descricao: "Borda recheada artesanal." }
    ];
</script>

<div class="max-w-md mx-auto p-4 pb-32">
    <header class="text-center py-10">
        <h1 class="text-4xl font-black gold-text italic tracking-tighter uppercase">BLACK PIZZARIA</h1>
    </header>

    <div class="flex justify-between border-b border-zinc-800 mb-8 overflow-x-auto text-[10px] uppercase tracking-widest px-2 gap-4 no-scrollbar">
        <button onclick="filtrar('Tradicionais')" id="tab-Tradicionais" class="pb-3 whitespace-nowrap aba-ativa">Tradicionais</button>
        <button onclick="filtrar('Gourmet')" id="tab-Gourmet" class="pb-3 whitespace-nowrap">Gourmet</button>
        <button onclick="filtrar('Doces')" id="tab-Doces" class="pb-3 whitespace-nowrap">Doces</button>
        <button onclick="filtrar('Bebidas')" id="tab-Bebidas" class="pb-3 whitespace-nowrap">Bebidas</button>
        <button onclick="filtrar('Adicionais')" id="tab-Adicionais" class="pb-3 whitespace-nowrap">Adicionais</button>
    </div>

    <div id="lista-pizzas" class="space-y-6"></div>
</div>

<div id="carrinho-bar" class="fixed bottom-0 left-0 right-0 bg-black/95 backdrop-blur-md p-5 border-t border-zinc-900 hidden flex justify-between items-center z-50">
    <div class="flex items-center gap-3">
        <div class="relative">
            <span class="absolute -top-2 -right-2 bg-yellow-600 text-black text-[10px] font-bold px-1.5 rounded-full" id="cart-count">0</span>
            <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 gold-text" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" /></svg>
        </div>
        <div>
            <p class="text-[10px] text-gray-500 uppercase italic">Subtotal + Entrega</p>
            <p class="text-xl font-bold gold-text" id="total-val">R$ 0,00</p>
        </div>
    </div>
    <button class="bg-yellow-600 text-black px-6 py-3 rounded-lg font-black text-[10px] uppercase italic" onclick="abrirModal()">Ver Carrinho</button>
</div>

<div id="modal-carrinho" class="fixed inset-0 bg-black/95 z-[60] hidden flex items-center justify-center p-4">
    <div class="bg-[#111] border border-zinc-800 w-full max-w-md rounded-2xl flex flex-col overflow-hidden relative">
        
        <div id="etapa-1" class="step active p-5">
            <div class="flex justify-between items-center mb-4">
                <h2 class="gold-text font-black uppercase text-xs italic">1. Itens</h2>
                <button onclick="fecharModal()" class="text-white text-2xl">&times;</button>
            </div>
            <div id="itens-checkout" class="space-y-4 mb-6"></div>
            <button onclick="mudarEtapa(2)" class="btn-gold uppercase text-[10px]">Próximo: Endereço</button>
        </div>

        <div id="etapa-2" class="step p-5">
            <div class="flex justify-between items-center mb-4">
                <h2 class="gold-text font-black uppercase text-xs italic">2. Endereço</h2>
                <button onclick="mudarEtapa(1)" class="text-white text-[10px]">Voltar</button>
            </div>
            <div class="space-y-3 mb-6">
                <input type="text" id="end-nome" placeholder="Seu Nome" class="w-full p-3 rounded-lg text-xs">
                <select id="end-bairro" onchange="atualizarBarra()" class="w-full p-3 rounded-lg text-xs">
                    <option value="" disabled selected>Escolha seu bairro (Caieiras)</option>
                    <script>
                        for (let b in TAXAS_ENTREGA) {
                            document.write(`<option value="${b}">${b} - R$ ${TAXAS_ENTREGA[b].toFixed(2)}</option>`);
                        }
                    </script>
                </select>
                <input type="text" id="end-rua" placeholder="Rua e Número" class="w-full p-3 rounded-lg text-xs">
                <input type="text" id="end-ref" placeholder="Ponto de referência" class="w-full p-3 rounded-lg text-xs">
            </div>
            <button onclick="mudarEtapa(3)" class="btn-gold uppercase text-[10px]">Próximo: Pagamento</button>
        </div>

        <div id="etapa-3" class="step p-5">
            <div class="flex justify-between items-center mb-4">
                <h2 class="gold-text font-black uppercase text-xs italic">3. Pagamento</h2>
                <button onclick="mudarEtapa(2)" class="text-white text-[10px]">Voltar</button>
            </div>
            <div class="space-y-4 mb-6">
                <select id="pag-metodo" onchange="togglePagamentoExtras()" class="w-full p-3 rounded-lg text-xs">
                    <option value="Pix">Pix (Pagar Agora)</option>
                    <option value="Dinheiro">Dinheiro</option>
                    <option value="Cartão de Crédito">Cartão de Crédito</option>
                    <option value="Cartão de Débito">Cartão de Débito</option>
                </select>
                <div id="box-pix" class="p-3 bg-zinc-900 border border-zinc-800 rounded-lg">
                    <p class="text-[10px] text-gray-400 italic">Chave Pix:</p>
                    <p class="gold-text font-bold text-sm tracking-widest" id="chave-pix-display"></p>
                </div>
                <div id="box-troco" class="hidden"><input type="number" id="pag-troco" placeholder="Troco para quanto?" class="w-full p-3 rounded-lg text-xs"></div>
                <div class="p-4 bg-zinc-900 rounded-lg border border-zinc-800">
                    <div class="flex justify-between text-[10px] text-zinc-500 uppercase"><span>Produtos:</span><span id="sub-resumo">R$ 0,00</span></div>
                    <div class="flex justify-between text-[10px] text-zinc-500 uppercase mb-2"><span>Entrega:</span><span id="taxa-resumo">R$ 0,00</span></div>
                    <div class="flex justify-between border-t border-zinc-800 pt-2 font-bold"><span class="text-xs uppercase">Total:</span><span id="total-resumo" class="gold-text">R$ 0,00</span></div>
                </div>
            </div>
            <button onclick="finalizarPedido()" class="btn-gold uppercase text-[10px]">Concluir Pedido</button>
        </div>

        <div id="etapa-4" class="step p-8 text-center relative">
            <button onclick="resetarTudo()" class="absolute top-2 right-4 text-white text-5xl font-light hover:text-yellow-600 transition-colors z-[999] p-2">&times;</button>
            
            <div class="success-icon mb-6 flex justify-center mt-6">
                <div class="h-20 w-20 bg-yellow-600 rounded-full flex items-center justify-center">
                    <svg class="h-10 w-10 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"></path></svg>
                </div>
            </div>
            
            <h2 class="text-2xl font-black gold-text italic uppercase mb-4">🍕 Pedido recebido com sucesso!</h2>
            <p class="text-zinc-400 text-sm leading-relaxed">
                Obrigado por escolher a <span class="gold-text font-bold uppercase">Black Pizzaria</span> 😍<br><br>
                Seu pedido já entrou em preparo.
            </p>
        </div>
    </div>
</div>

<script>
    let carrinho = [];
    document.getElementById('chave-pix-display').innerText = CHAVE_PIX;

    function resetarTudo() {
        carrinho = [];
        atualizarBarra();
        document.getElementById('carrinho-bar').classList.add('hidden');
        fecharModal();
        mudarEtapa(1);
        document.getElementById('end-nome').value = "";
        document.getElementById('end-rua').value = "";
        document.getElementById('end-ref').value = "";
        document.getElementById('end-bairro').selectedIndex = 0;
    }

    function filtrar(cat) {
        document.querySelectorAll('[id^="tab-"]').forEach(el => el.classList.remove('aba-ativa'));
        document.getElementById('tab-' + cat).classList.add('aba-ativa');
        renderizar(cat);
    }

    function renderizar(cat = 'Tradicionais') {
        const lista = document.getElementById('lista-pizzas');
        lista.innerHTML = ""; 
        PRODUTOS.filter(p => p.categoria === cat).forEach(p => {
            lista.innerHTML += `
                <div class="card-black">
                    <div class="flex justify-between items-start mb-4">
                        <div>
                            <h3 class="font-bold text-lg uppercase italic">${p.nome}</h3>
                            <p class="text-gray-500 text-[11px] mt-1">${p.descricao}</p>
                        </div>
                        <span class="font-bold gold-text text-sm">R$ ${p.preco.toFixed(2)}</span>
                    </div>
                    ${p.especial === 'meio-a-meio' ? 
                        `<input type="text" id="sabores-99" placeholder="Ex: Metade Calabresa / Metade Mussarela" class="w-full p-2 mb-2 rounded border border-zinc-800 text-[10px] bg-black text-white outline-none">` : ''}
                    <button class="btn-gold text-[10px] uppercase italic" onclick="add(${p.id})">Adicionar ao Carrinho</button>
                </div>`;
        });
    }

    function add(id) {
        const p = PRODUTOS.find(p => p.id === id);
        let nomeFinal = p.nome;
        if (p.especial === 'meio-a-meio') {
            const sabores = document.getElementById('sabores-99').value;
            if (!sabores) return alert("Por favor, digite os dois sabores da pizza meio a meio.");
            nomeFinal = `MEIO A MEIO (${sabores})`;
            document.getElementById('sabores-99').value = "";
        }
        carrinho.push({ ...p, nome: nomeFinal, qtd: 1 });
        atualizarBarra();
    }

    function atualizarBarra() {
        const sub = carrinho.reduce((acc, i) => acc + (i.preco * i.qtd), 0);
        const taxa = TAXAS_ENTREGA[document.getElementById('end-bairro').value] || 0;
        const total = sub + taxa;
        document.getElementById('total-val').innerText = `R$ ${total.toFixed(2)}`;
        document.getElementById('cart-count').innerText = carrinho.length;
        if(carrinho.length > 0) document.getElementById('carrinho-bar').classList.remove('hidden');
        document.getElementById('sub-resumo').innerText = `R$ ${sub.toFixed(2)}`;
        document.getElementById('taxa-resumo').innerText = `R$ ${taxa.toFixed(2)}`;
        document.getElementById('total-resumo').innerText = `R$ ${total.toFixed(2)}`;
    }

    function mudarEtapa(n) {
        document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
        document.getElementById('etapa-' + n).classList.add('active');
    }

    function abrirModal() {
        const cont = document.getElementById('itens-checkout');
        cont.innerHTML = "";
        carrinho.forEach((i, index) => {
            cont.innerHTML += `
                <div class="flex justify-between bg-zinc-900/50 p-3 rounded-lg border border-zinc-800">
                    <p class="text-[10px] font-bold uppercase italic">${i.nome}</p>
                    <div class="flex items-center gap-2">
                        <p class="gold-text text-[10px]">R$ ${i.preco.toFixed(2)}</p>
                        <button onclick="removerItem(${index})" class="text-red-500 font-bold ml-2">X</button>
                    </div>
                </div>`;
        });
        mudarEtapa(1);
        document.getElementById('modal-carrinho').classList.remove('hidden');
        document.body.style.overflow = 'hidden';
    }

    function removerItem(index) {
        carrinho.splice(index, 1);
        if (carrinho.length === 0) {
            fecharModal();
            document.getElementById('carrinho-bar').classList.add('hidden');
        } else {
            abrirModal();
            atualizarBarra();
        }
    }

    function fecharModal() { document.getElementById('modal-carrinho').classList.add('hidden'); document.body.style.overflow = 'auto'; }
    function togglePagamentoExtras() {
        const m = document.getElementById('pag-metodo').value;
        document.getElementById('box-troco').classList.toggle('hidden', m !== "Dinheiro");
        document.getElementById('box-pix').classList.toggle('hidden', m !== "Pix");
    }

    function finalizarPedido() {
        const nome = document.getElementById('end-nome').value;
        const bairro = document.getElementById('end-bairro').value;
        const rua = document.getElementById('end-rua').value;
        if(!nome || !bairro || !rua) return alert("Preencha o endereço completo!");

        const sub = carrinho.reduce((acc, i) => acc + (i.preco * i.qtd), 0);
        const taxa = TAXAS_ENTREGA[bairro] || 0;
        const pag = document.getElementById('pag-metodo').value;
        const troco = document.getElementById('pag-troco').value;

        let msg = `*NOVO PEDIDO - ${NOME_PIZZARIA}*\n\n`;
        carrinho.forEach(i => msg += `▪️ ${i.nome}\n`);
        msg += `\n🍕 *Produtos:* R$ ${sub.toFixed(2)}\n🛵 *Entrega:* R$ ${taxa.toFixed(2)}\n💰 *TOTAL:* R$ ${(sub+taxa).toFixed(2)}`;
        msg += `\n\n💳 *Pagamento:* ${pag}${pag === "Pix" ? '\n*(Chave: '+CHAVE_PIX+')*' : ''}${pag === "Dinheiro" && troco ? ' (Troco p/ R$ '+troco+')' : ''}`;
        msg += `\n\n📍 *ENTREGA:*\n${nome}\n${rua}\nBairro: ${bairro}`;

        window.open(`https://wa.me/${WHATSAPP_NUMERO}?text=${encodeURIComponent(msg)}`);
        mudarEtapa(4);
    }
    renderizar();
</script>
</body>
</html>
