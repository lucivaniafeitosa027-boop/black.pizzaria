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
        ::-webkit-scrollbar { width: 0px; }
        input, select { background: #181818 !important; border: 1px solid #333 !important; color: white !important; outline: none; }
        .step { display: none; }
        .step.active { display: block; }
    </style>
</head>
<body>

<script>
    const NOME_PIZZARIA = "BLACK PIZZARIA";
    const WHATSAPP_NUMERO = "5511982416568"; 
    const PRODUTOS = [
        { id: 1, nome: "Black", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, CALABRESA, PRESUNTO, BACON, AZEITONA, CEBOLA , TOMATE E ORÉGANO." },
        { id: 2, nome: "PORTUGUESA", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, PRESUNTO, OVO, BACON, PALMITO, AZEITONA,CEBOLA, TOMATE E OREGANO." },
        { id: 3, nome: "NAPOLITANA", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, CALABRESA, FRANGO, BACON, CEBOLA, TOMATE E OREGANO." },
        { id: 4, nome: "BACON", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, BACON, AZEITONA, CEBOLA, TOMATE E OREGANO." },
        { id: 5, nome: "CALABRESA", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, CALABRESA, AZEITONA, CEBOLA,TOMATE E OREGANO.." },
        { id: 6, nome: "MUSSARELA", preco: 50.00, categoria: "Tradicionais", descricao: " MOLHO, MUSSARELA, AZEITONA, CEBOLA, TOMATE E ORÉGANO." },
        { id: 7, nome: "FRANGO COM CATUPIRY ", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, FRANGO, AZEITONA, CATUPIRY, CEBOLA, TOMATE E OREGANO.." },
        { id: 8, nome: "FRANCESA", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, PRESUNTO, CALABRESA EM CUBOS, AZEITONA, CEBOLA, TOMATE E ORÉGANO.." },
        { id: 9, nome: "MARGUERITA", preco: 50.00, categoria: "Tradicionais", descricao: "MOLHO, MUSSARELA, MANJERICÃO, AZEITONA, CEBOLA, TOMATE E ORÉGANO." },
        { id: 10, nome: "MODA DA CASA", preco: 65.00, categoria: "Gourmet", descricao: "MOLHO, MUSSARELA, CALABRESA, PRESUNTO, FRANGO, OVO, ERVILHA, AZEITONA, CEBOLA, TOMATE E OREGANO." },
        { id: 11, nome: "CARNE COM CHEDDAR", preco: 60.00, categoria: "Gourmet", descricao: "MOLHO, MUSSARELA, CARNE, CHEDDAR, PIMENTÃO, AZEITONA, CEBOLA, TOMATE E OREGANO.." },
        { id: 12, nome: "MALUCA DOIS RECHEIOS", preco: 80.00, categoria: "Gourmet", descricao: "MOLHO, MUSSARELA, CATUPIRY, CALABRESA, PRESUNTO, FRANGO, OVO, MILHO, AZEITONA, CEBOLA, TOMATE, ORÉGANO E DUAS MASSAS.." },
        { id: 13, nome: "BANANA", preco: 40.00, categoria: "Doces", descricao: "BANANA, LEITE CONDENSADO E CANELA EM PÓ." },
        { id: 14, nome: "Coca-Cola 2L", preco: 15.00, categoria: "Bebidas", descricao: "Gelada." },
        { id: 15, nome: "FANTA LARANJA 2L", preco: 15.00, categoria: "Bebidas", descricao: "Gelada." },
        { id: 16, nome: "Borda de Catupiry", preco: 10.00, categoria: "Adicionais", descricao: "Borda recheada artesanal." },
        { id: 17, nome: "Borda de cheddar", preco: 10.00, categoria: "Adicionais", descricao: "Borda recheada artesanal." },
        { id: 18, nome: "BACON COM CATUPIRY ", preco: 10.00, categoria: "Adicionais", descricao: "Borda recheada artesanal." },
        { id: 19, nome: "FRANGO COM CATUPIRY", preco: 10.00, categoria: "Adicionais", descricao: "Borda recheada artesanal." },
        { id: 20, nome: "Calabresa com cheddar", preco: 10.00, categoria: "Adicionais", descricao: "Borda recheada artesanal." },
        { id: 21, nome: "Queijo com catupiry", preco: 10.00, categoria: "Adicionais", descricao: "Borda recheada artesanal." },
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

<div id="carrinho-bar" class="fixed bottom-0 left-0 right-0 bg-black/90 backdrop-blur-md p-5 border-t border-zinc-900 hidden flex justify-between items-center z-40">
    <div>
        <p class="text-[10px] text-gray-500 uppercase italic">Subtotal</p>
        <p class="text-xl font-bold gold-text" id="total-val">R$ 0,00</p>
    </div>
    <button class="bg-yellow-600 text-black px-6 py-3 rounded-lg font-black text-[10px] uppercase italic" onclick="abrirModal()">Ver Carrinho</button>
</div>

<div id="modal-carrinho" class="fixed inset-0 bg-black/95 z-[60] hidden flex items-center justify-center p-4">
    <div class="bg-[#111] border border-zinc-800 w-full max-w-md rounded-2xl flex flex-col max-h-[90vh]">
        
        <div id="etapa-1" class="step active flex flex-col h-full">
            <div class="p-5 border-b border-zinc-900 flex justify-between items-center">
                <h2 class="gold-text font-black uppercase text-xs italic">1. Itens</h2>
                <button onclick="fecharModal()" class="text-white text-2xl font-light">&times;</button>
            </div>
            <div id="itens-checkout" class="p-5 overflow-y-auto space-y-4"></div>
            <div class="p-6 border-t border-zinc-900">
                <button onclick="mudarEtapa(2)" class="btn-gold uppercase text-[10px] py-4">Continuar para Endereço</button>
            </div>
        </div>

        <div id="etapa-2" class="step flex flex-col h-full">
            <div class="p-5 border-b border-zinc-900 flex justify-between items-center">
                <h2 class="gold-text font-black uppercase text-xs italic">2. Entrega</h2>
                <button onclick="mudarEtapa(1)" class="text-white text-[10px] uppercase">Voltar</button>
            </div>
            <div class="p-5 space-y-4">
                <input type="text" id="end-nome" placeholder="Seu Nome" class="w-full p-3 rounded-lg text-xs">
                <div class="flex gap-2">
                    <input type="text" id="end-rua" placeholder="Rua" class="flex-1 p-3 rounded-lg text-xs">
                    <input type="text" id="end-num" placeholder="Nº" class="w-20 p-3 rounded-lg text-xs">
                </div>
                <input type="text" id="end-bairro" placeholder="Bairro" class="w-full p-3 rounded-lg text-xs">
            </div>
            <div class="p-6 border-t border-zinc-900">
                <button onclick="mudarEtapa(3)" class="btn-gold uppercase text-[10px] py-4">Próximo: Pagamento</button>
            </div>
        </div>

        <div id="etapa-3" class="step flex flex-col h-full">
            <div class="p-5 border-b border-zinc-900 flex justify-between items-center">
                <h2 class="gold-text font-black uppercase text-xs italic">3. Pagamento</h2>
                <button onclick="mudarEtapa(2)" class="text-white text-[10px] uppercase">Voltar</button>
            </div>
            <div class="p-5 space-y-4">
                <select id="pag-metodo" onchange="toggleTroco()" class="w-full p-3 rounded-lg text-xs">
                    <option value="Pix">Pix</option>
                    <option value="Cartão de Crédito">Cartão de Crédito</option>
                    <option value="Cartão de Débito">Cartão de Débito</option>
                    <option value="Dinheiro">Dinheiro</option>
                </select>
                <input type="number" id="pag-troco" placeholder="Troco para quanto?" class="w-full p-3 rounded-lg text-xs hidden">
                <div class="flex justify-between mt-10 p-4 bg-zinc-900 rounded-lg">
                    <span class="text-gray-500 uppercase text-[10px] font-bold">Total</span>
                    <span id="total-final" class="gold-text font-bold text-xl italic">R$ 0,00</span>
                </div>
            </div>
            <div class="p-6 border-t border-zinc-900">
                <button onclick="finalizarPedido()" class="btn-gold uppercase text-[10px] py-4">Finalizar e Enviar</button>
            </div>
        </div>

        <div id="etapa-4" class="step flex flex-col h-full text-center p-10">
            <div class="text-4xl mb-6">✅</div>
            <h2 class="gold-text font-black uppercase text-xl italic mb-4">Pedido Enviado!</h2>
            <p class="text-xs text-gray-500 mb-8 uppercase">Acompanhe os detalhes pelo WhatsApp.</p>
            <button onclick="window.location.reload()" class="btn-gold uppercase text-[10px] py-4 tracking-widest">Fazer Novo Pedido</button>
        </div>
    </div>
</div>

<script>
    let carrinho = [];

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
                        <div><h3 class="font-bold text-lg uppercase italic tracking-tighter">${p.nome}</h3><p class="text-gray-500 text-[11px] mt-1">${p.descricao}</p></div>
                        <span class="font-bold gold-text text-sm">R$ ${p.preco.toFixed(2)}</span>
                    </div>
                    <button class="btn-gold text-[10px] uppercase italic" onclick="add(${p.id})">Adicionar</button>
                </div>`;
        });
    }

    function add(id) {
        const item = carrinho.find(i => i.id === id);
        if (item) item.qtd++; else carrinho.push({...PRODUTOS.find(p => p.id === id), qtd: 1});
        const total = carrinho.reduce((acc, i) => acc + (i.preco * i.qtd), 0);
        document.getElementById('total-val').innerText = `R$ ${total.toFixed(2)}`;
        document.getElementById('carrinho-bar').classList.remove('hidden');
    }

    function mudarEtapa(n) {
        document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
        document.getElementById('etapa-' + n).classList.add('active');
        if(n === 3) document.getElementById('total-final').innerText = document.getElementById('total-val').innerText;
    }

    function abrirModal() {
        const cont = document.getElementById('itens-checkout');
        cont.innerHTML = "";
        carrinho.forEach(i => {
            cont.innerHTML += `
                <div class="flex justify-between items-center bg-[#181818] p-4 rounded-xl border border-zinc-900">
                    <div><p class="text-xs font-bold uppercase italic">${i.nome}</p><p class="gold-text text-[10px]">R$ ${(i.preco*i.qtd).toFixed(2)}</p></div>
                    <span class="text-xs font-bold">${i.qtd}x</span>
                </div>`;
        });
        mudarEtapa(1);
        document.getElementById('modal-carrinho').classList.remove('hidden');
    }

    function fecharModal() { document.getElementById('modal-carrinho').classList.add('hidden'); }
    function toggleTroco() { document.getElementById('pag-troco').classList.toggle('hidden', document.getElementById('pag-metodo').value !== "Dinheiro"); }

    function finalizarPedido() {
        const nome = document.getElementById('end-nome').value;
        const rua = document.getElementById('end-rua').value;
        const num = document.getElementById('end-num').value;
        const bairro = document.getElementById('end-bairro').value;
        const pag = document.getElementById('pag-metodo').value;
        const troco = document.getElementById('pag-troco').value;

        if(!nome || !rua || !num || !bairro) return alert("Por favor, preencha o endereço completo!");

        let msg = `*NOVO PEDIDO - ${NOME_PIZZARIA}*\n\n`;
        carrinho.forEach(i => msg += `▪️ ${i.qtd}x ${i.nome}\n`);
        msg += `\n💰 *Total:* ${document.getElementById('total-val').innerText}\n💳 *Pagamento:* ${pag}${troco?' (Troco p/ R$ '+troco+')':''}\n\n📍 *ENTREGA:*\n${nome}\n${rua}, ${num} - ${bairro}`;

        window.open(`https://wa.me/${WHATSAPP_NUMERO}?text=${encodeURIComponent(msg)}`);
        mudarEtapa(4);
    }

    renderizar();
</script>
</body>
</html>
