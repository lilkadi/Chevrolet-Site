<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Chevrolet Site</title>
<style>
body{margin:0;font-family:tahoma;background:#f5f5f5}
header{background:#000;color:#ffd700;padding:15px;text-align:center;position:sticky;top:0;z-index:1000}
button{cursor:pointer}

/* شريط الصور العلوي */
.banner-cars{
  position:relative;width:100%;height:300px;overflow:hidden;margin-bottom:10px;
}
.banner-cars img{
  width:100%;
  height:300px;
  object-fit:cover;
  position:absolute;
  top:0;
  left:0;
  transition:opacity 1s ease;
  opacity:0;
}
.banner-cars img.active{opacity:1}

#searchBtn{width:95%;margin:10px auto;display:block;padding:12px;background:#000;color:#fff;border:none;border-radius:8px;font-size:16px}
#searchInput{width:95%;margin:10px auto;display:none;padding:10px;font-size:16px;border-radius:8px;border:1px solid #fff;background:#000;color:#fff}

.product-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:15px;padding:15px}
.product{background:#fff;border-radius:10px;padding:10px;box-shadow:0 2px 6px rgba(0,0,0,.1);text-align:center}
.price{color:#ff6600;font-weight:bold;margin:5px}
.qty{display:flex;justify-content:center;gap:5px;margin:5px}
.qty button{width:30px;height:30px;border:none;border-radius:5px}
.inc{background:yellow}.dec{background:red;color:#fff}
.whatsappBtnProduct{display:block;margin:10px auto 0 auto;background:#25D366;color:#fff;border-radius:5px;padding:8px 10px;text-align:center;text-decoration:none;width:90%;font-size:14px}
.whatsappBtnProduct:hover{opacity:0.8}
.whatsappBtnProduct.inquiry{background:#007bff}

#cartCount{font-weight:bold;margin-left:5px}
.cartBtn{position:fixed;bottom:20px;right:20px;background:#000;color:#fff;border-radius:50%;padding:15px;font-size:20px;z-index:1000;}
#cartBox{display:none;position:fixed;bottom:80px;right:20px;background:#000;color:#fff;border:2px solid #fff;border-radius:10px;width:300px;max-height:400px;overflow:auto;padding:10px;}
#cartBox button#placeOrderBtn{width:100%;padding:10px;margin-top:10px;background:#ffd700;color:#000;border:none;border-radius:5px;cursor:pointer;}
#loginBtnTop{display:inline-block;padding:10px 20px;margin-top:10px;background:#ffd700;color:#000;border:none;border-radius:5px;cursor:pointer;}
#loginModal{display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.8);display:flex;align-items:center;justify-content:center;z-index:2000;}
#loginModal div{background:#000;color:#fff;padding:20px;border-radius:10px;text-align:center;min-width:300px;}
#loginModal input{width:90%; padding:8px; margin:10px 0;border-radius:5px;border:1px solid #fff;background:#222;color:#fff;}
#loginModal button{padding:10px 20px; margin-top:10px; cursor:pointer;background:#ffd700;color:#000;border:none;border-radius:5px;}
#orderBox{display:none; padding:10px; border:2px solid #fff; margin-top:10px; border-radius:10px; background:#000;color:#fff;}
#orderBox input{width:90%;padding:8px;margin:5px 0;border-radius:5px;border:1px solid #fff;background:#222;color:#fff;}
#orderBox button{padding:8px 12px;background:#ffd700;border:none;border-radius:5px;cursor:pointer;margin-top:10px;color:#000;}
</style>
</head>
<body>

<header>
<h2>Chevrolet Site</h2>
<button id="loginBtnTop" onclick="showLogin()">تسجيل الدخول</button>
</header>

<div class="banner-cars">
  <img src="https://cdn.salla.sa/mQpGy/dd06a5fb-2e9b-4f97-87be-c76dfdf02190-1000x1000-UiKRN84uJnxNI4O2A0mcIHD5lIcoIvmywG7AJ7vx.jpg" class="active">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSJn8zvfImPaKGVK4ZJIrrIPTdLMjMfIEpf1GQMGQiJpI6J_JAlhapRTwc6&s=10">
  <img src="https://images.netdirector.co.uk/gforces-auto/image/upload/w_412,h_309,q_auto:best,c_fill,f_auto,fl_lossy/auto-client/d418a4d2f88732d056860e0a37947119/traverse_1920x640.jpg">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSqwAx7NbfzcZJiTikZruvGMM5ZwVOyeD4T6tiEPa1OsJSjTNtpeYDuRk7V&s=10">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQoCakHSez2g2j27WncCQ5DUMaM2VWUsQqsRyhb1AwZrJa-75FQsstc3zQ&s=10">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcToA66OnCB295OmKol0CZJ4EoboIPsd1FOWRXykXCcdA&s=10">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTqvq0VHNraiYFApwMtwvUcsAth_OLRTYccJGE4NH-OU4CM40NWMdJ9bk8&s=10">
</div>

<button id="searchBtn" onclick="toggleSearch()">🔍 بحث عن قطعة</button>
<input id="searchInput" placeholder="اكتب اسم القطعة" onkeyup="searchProducts()">

<div class="product-grid" id="products"></div>

<div id="cartBox">
<h3>سلة المشتريات</h3>
<div id="cartItems"></div>
<b>المجموع: <span id="total">0</span> $</b>
<button id="placeOrderBtn" onclick="showOrderBox()">تثبيت الطلب</button>
<div id="orderBox">
<h3>بيانات الزبون</h3>
<input id="custName" placeholder="الاسم"><br>
<input id="custPhone" placeholder="رقم الهاتف"><br>
<input id="custAddress" placeholder="العنوان"><br>
<button onclick="sendOrder()">إرسال الطلب</button>
</div>
</div>

<div class="cartBtn" onclick="toggleCart()">🛒<span id="cartCount">0</span></div>

<div id="loginModal">
<div>
<h3>تسجيل الدخول</h3>
<input id="u" placeholder="اسم المستخدم"><br>
<input id="c" placeholder="رمز الدخول"><br>
<input id="p" type="password" placeholder="كلمة المرور"><br>
<button onclick="login()">دخول</button>
</div>
</div>

<script>
let products=[], cart=[];
const list=document.getElementById("products");

const bannerImages=document.querySelectorAll(".banner-cars img");
let current=0;
setInterval(()=>{
  bannerImages.forEach(img=>img.classList.remove("active"));
  current=(current+1)%bannerImages.length;
  bannerImages[current].classList.add("active");
},3000);

function showLogin(){ document.getElementById("loginModal").style.display="flex"; }
function login(){
  if(u.value==="admin" && c.value==="1" && p.value==="1234"){
    alert("تم تسجيل الدخول بنجاح");
  } else alert("خطأ في اسم المستخدم أو الرمز أو كلمة المرور");
  document.getElementById("loginModal").style.display="none";
}
function toggleSearch(){ 
  const input = document.getElementById("searchInput");
  input.style.display = input.style.display==="block"?"none":"block"; 
}

/* =========================
   قراءة المنتجات من SheetBest
========================= */
const apiURL = "https://api.sheetbest.com/sheets/044c3d5a-80e6-42eb-87cc-488eba7900aa";

fetch(apiURL)
  .then(res => res.json())
  .then(data => {
    products = data.map(item => ({
      name: item['اسم المادة'] || item['name'] || "بدون اسم",
      price: item['البيع'] || item['price'] || 0
    }));
    renderProducts();
  })
  .catch(err => console.error(err));

function renderProducts(filteredProducts){
    const data = filteredProducts || products;
    list.innerHTML = "";
    data.forEach((prod, idx)=>{
        const div = document.createElement("div");
        div.className = "product";
        div.innerHTML = `
            <h4>${prod.name}</h4>
            <div class="price">${prod.price} $</div>
            <div class="qty">
                <button class="dec" onclick="changeQty(${idx},-1)">-</button>
                <span id="qty${idx}">1</span>
                <button class="inc" onclick="changeQty(${idx},1)">+</button>
            </div>
            <a href="#" class="whatsappBtnProduct" onclick="addToCart(${idx})">أضف للطلب</a>
            <a href="#" class="whatsappBtnProduct inquiry" onclick="sendInquiry('${prod.name}', ${prod.price})">استفسار عن القطعة</a>
        `;
        list.appendChild(div);
    });
}

function searchProducts(){
    const term = document.getElementById("searchInput").value.toLowerCase();
    const filtered = products.filter(p=>p.name.toLowerCase().includes(term));
    renderProducts(filtered);
}

function changeQty(idx, val){
    const qtyEl = document.getElementById(`qty${idx}`);
    let qty = parseInt(qtyEl.innerText);
    qty += val;
    if(qty < 1) qty = 1;
    qtyEl.innerText = qty;
}

function addToCart(idx){
    const qty = parseInt(document.getElementById(`qty${idx}`).innerText);
    const prod = {...products[idx], qty};
    const existing = cart.find(c => c.name === prod.name);
    if(existing) existing.qty += qty;
    else cart.push(prod);
    updateCart();
}

function updateCart(){
    const cartItems = document.getElementById("cartItems");
    cartItems.innerHTML = "";
    let total = 0;
    cart.forEach(item=>{
        const div = document.createElement("div");
        div.innerHTML = `${item.name} x ${item.qty} = ${item.price*item.qty} $ <button onclick="removeCart('${item.name}')">حذف</button>`;
        cartItems.appendChild(div);
        total += item.price*item.qty;
    });
    document.getElementById("total").innerText = total;
    document.getElementById("cartCount").innerText = cart.reduce((a,b)=>a+b.qty,0);
}

function removeCart(name){
    cart = cart.filter(c=>c.name!==name);
    updateCart();
}

function toggleCart(){
    const box = document.getElementById("cartBox");
    box.style.display = box.style.display==="block"?"none":"block";
}

function showOrderBox(){ document.getElementById("orderBox").style.display="block"; }

function sendOrder(){
    const name = document.getElementById("custName").value;
    const phone = document.getElementById("custPhone").value;
    const address = document.getElementById("custAddress").value;
    if(!name || !phone || !address){ alert("ادخل الاسم، رقم الهاتف، والعنوان"); return; }

    let msg = `طلبية جديدة: الزبون: ${name} رقم الهاتف: ${phone} العنوان: ${address} الطلب: `;

    let total = 0;
    cart.forEach(item=>{
        const itemTotal = item.price * item.qty;
        msg += `${item.name} - ${item.qty} × ${item.price} = ${itemTotal} $; `;
        total += itemTotal;
    });

    msg += `المجموع: ${total}$ راح نراسلك لتحديد السعر مع التوصيل.`;

    window.open(`https://wa.me/9647872159504?text=${encodeURIComponent(msg)}`);
}

function sendInquiry(productName, productPrice){
    const msg = `لدي استفسار عن القطعة: اسم القطعة: ${productName} السعر: ${productPrice} $`;
    window.open(`https://wa.me/9647872159504?text=${encodeURIComponent(msg)}`);
}
</script>

</body>
</html>
