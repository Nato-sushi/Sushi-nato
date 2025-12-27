<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Nato Sushi | Delivery</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body{margin:0;font-family:Arial;background:#0e0e0e;color:#fff}
header{text-align:center;padding:20px;background:#000}
h1{color:#e50914;margin:0}
h2{color:#e50914;margin-top:30px}
.container{padding:15px}
.item{background:#1c1c1c;padding:10px;border-radius:8px;margin-bottom:10px}
.item button{background:#1db954;border:none;padding:6px 10px;border-radius:5px;color:#fff;margin-top:5px}
.cart{background:#141414;padding:15px;border-radius:10px;margin-top:20px}
input,select{width:100%;padding:8px;margin-top:8px;border-radius:5px;border:none}
.btn{margin-top:15px;padding:15px;background:#25d366;color:#fff;text-align:center;border-radius:10px;font-size:18px}
.total{font-weight:bold;font-size:18px;color:#e50914;margin-top:10px}
.qty button{margin:0 5px}
</style>
</head>

<body>

<header>
<h1>Nato Sushi</h1>
<p>Delivery oriental • Pix • Dinheiro • Cartão</p>
</header>

<div class="container" id="menu"></div>

<div class="container cart">
<h3>🛒 Carrinho</h3>
<div id="cartItems"></div>

<label>Nome</label>
<input id="name">

<label>Endereço (com bairro)</label>
<input id="address" oninput="calcDelivery()">

<label>Quantidade de hashis</label>
<input type="number" id="hashi" value="1">

<label>Forma de pagamento</label>
<select id="payment">
<option>Pix</option>
<option>Dinheiro</option>
<option>Cartão</option>
</select>

<label><input type="checkbox" id="tare"> Molho Tarê (+ R$ 6,00)</label>

<p id="delivery"></p>
<p class="total" id="total">Total: R$ 0,00</p>

<div class="btn" onclick="sendWhatsApp()">Finalizar pedido</div>
</div>

<script>
const menu=[
{cat:"TEMAKI",items:[
["Temaki Salmão Natural",35],
["Temaki Salmão Filadélfia",38],
["Temaki Skin",35],
["Temaki Atum Natural",35],
["Temaki Atum Picante",38],
["Temaki Califórnia",38],
["Temaki Ebi",38]
]},
{cat:"COMBINADOS",items:[
["Combinado Sushi 16 peças",65],
["Combinado Sushi 30 peças",85],
["Combinado Sushi 50 peças",150],
["Combinado Brazeado 22 peças",80]
]},
{cat:"URAMAKI",items:[
["Dobo Salmão",35],
["Dragoflay",38],
["MAKI 2507",38],
["Cheff Maki",35],
["Salmo Crispe",35],
["Skin Maki",35],
["Ebi Maki",38],
["Salmão Califórnia",38],
["Mack Roll",35]
]},
{cat:"HOSSOMAKI",items:[
["Hossomaki Salmão",30],
["Hossomaki Filadélfia",32],
["Hossocappa",30],
["Hossotuna",30],
["Hossoebi",32]
]},
{cat:"HOT",items:[
["Hot Salmão",35],
["Hot Salmão Filadélfia",35],
["Hot Califórnia",38],
["Hot Combinado 20 peças",100]
]},
{cat:"NIGUIRI",items:[
["Niguiri Salmão",25],
["Niguiri Atum",25],
["Niguiri Skin",25],
["Niguiri Brazeado",25],
["Niguiri Salmão Filadélfia Brazeado",27]
]},
{cat:"JOE",items:[
["Joe Salmão",30],
["Joe Salmão Brazeado",30],
["Joe Salmão Brazeado Filadélfia",34],
["Joe Tuna Cappa Picante",30],
["Joe Salmão Maracujá",30],
["Joe Crispe",30],
["Joe Skin",30]
]}
];

let cart=[],deliveryFee=0;

menu.forEach(sec=>{
menuDiv.innerHTML+=`<h2>${sec.cat}</h2>`;
sec.items.forEach(i=>{
menuDiv.innerHTML+=`
<div class="item">
<strong>${i[0]}</strong><br>
R$ ${i[1].toFixed(2)}
<br><button onclick="add('${i[0]}',${i[1]})">Adicionar</button>
</div>`});
});

function add(n,p){
let i=cart.find(x=>x.n==n);
i?i.q++:cart.push({n,p,q:1});
render();
}

function calcDelivery(){
let a=address.value.toLowerCase();
deliveryFee=a.includes("centro")?5:a.includes("praia")?10:12;
delivery.innerText="🚚 Taxa: R$ "+deliveryFee.toFixed(2);
render();
}

function render(){
let h="",t=0;
cart.forEach(i=>{
h+=`${i.n} x${i.q}<br>`;
t+=i.p*i.q;
});
if(tare.checked)t+=6;
t+=deliveryFee;
cartItems.innerHTML=h;
total.innerText="Total: R$ "+t.toFixed(2);
}

tare.onchange=render;

function sendWhatsApp(){
let m=`🍣 *PEDIDO – NATO SUSHI* 🍣%0A%0A👤 ${name.value}%0A📍 ${address.value}%0A🥢 Hashis: ${hashi.value}%0A💳 ${payment.value}%0A%0A🛒 ITENS:%0A`;
let t=0;
cart.forEach(i=>{m+=`- ${i.n} x${i.q}%0A`;t+=i.p*i.q});
if(tare.checked){m+="- Molho Tarê (+6)%0A";t+=6}
m+=`🚚 Taxa: R$ ${deliveryFee}%0A💰 TOTAL: R$ ${(t+deliveryFee).toFixed(2)}`;
window.open("https://wa.me/5527995125034?text="+m);
}
</script>
</body>
</html>
