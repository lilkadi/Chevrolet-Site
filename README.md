<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Chevrolet Site</title>

<style>
:root{--black:#000;--yellow:#ffd700;--white:#fff;--gray:#f2f2f2;--darkGray:#111}
*{box-sizing:border-box}
body{margin:0;font-family:tahoma;background:#000;color:#fff;user-select:none}
.main{width:100%;padding:0 12px}
header{background:var(--black);color:var(--yellow);padding:12px 10px;position:sticky;top:0;z-index:1000;display:flex;justify-content:space-between;align-items:center}
header h2{margin:0;font-size:20px;letter-spacing:2px}
header .btns{display:flex;gap:8px}
header button{background:var(--yellow);color:var(--black);border:none;padding:10px 10px;border-radius:10px;font-weight:700;cursor:pointer;font-size:13px}

/* Banner */
.banner-cars{
  position:relative;
  width:100%;
  height:200px;
  overflow:hidden;
  margin:10px 0;
  border-radius:15px;
  border:2px solid var(--yellow);
}
.banner-cars img{
  width:100%;
  height:200px;
  object-fit:cover;
  position:absolute;
  top:0;
  left:0;
  transition:opacity 1s ease;
  opacity:0
}
.banner-cars img.active{opacity:1}

/* Search */
.searchBar{
  display:flex;
  flex-direction:column;
  gap:10px;
  width:100%;
}
#searchInput{width:100%;padding:12px;border-radius:12px;border:2px solid var(--yellow);background:#111;color:#fff;font-size:16px}
#searchBtn,#catBtn{padding:12px;border:none;border-radius:12px;background:var(--yellow);color:#000;font-weight:700;cursor:pointer;font-size:16px}

/* Products */
.product-grid{
  display:grid;
  grid-template-columns:1fr;
  gap:14px;
  width:100%;
  margin-top:10px;
}
.product{
  background:#fff;color:#000;border-radius:15px;padding:12px;
  box-shadow:0 8px 20px rgba(0,0,0,.25);
  cursor:pointer;
}
.product img{width:100%;height:160px;object-fit:cover;border-radius:12px}
.product h4{margin:10px 0 5px 0;font-size:18px;font-weight:800}
.product .price{color:#ff6600;font-weight:900;margin:5px 0;font-size:18px}
.qty{display:flex;justify-content:center;gap:8px;margin:10px 0}
.qty button{width:36px;height:36px;border:none;border-radius:8px;font-size:18px;font-weight:700}
.inc{background:var(--yellow)}
.dec{background:#ff3b3b;color:#fff}
.whatsappBtnProduct{display:block;margin:10px auto 0 auto;background:#25D366;color:#fff;border-radius:10px;padding:10px 12px;text-align:center;text-decoration:none;width:100%;font-size:14px;font-weight:700}

/* Cart Button */
.cartBtn{
  position:fixed;
  bottom:15px;
  right:15px;
  background:var(--black);
  color:var(--yellow);
  border-radius:50%;
  padding:16px;
  font-size:22px;
  z-index:1000;
  box-shadow:0 8px 20px rgba(0,0,0,.4)
}
#cartCount{font-weight:900;margin-left:8px}

/* Cart Modal */
.cartModal{
  position:fixed;top:0;left:0;width:100%;height:100%;
  background:rgba(0,0,0,0.8);
  display:none;
  align-items:center;justify-content:center;
  z-index:1500
}
.cartModalContent{
  width:90%;max-width:420px;background:#000;color:#fff;border:2px solid var(--yellow);
  border-radius:20px;padding:15px;position:relative;
}
.cartModalContent h2{text-align:center;margin:0;font-size:20px}
.cartModalContent .closeCart{position:absolute;top:12px;right:12px;font-size:30px;color:var(--yellow);cursor:pointer}
.cartItems{margin-top:15px;max-height:320px;overflow:auto}
.cartItem{
  display:flex;gap:10px;background:#111;border:1px solid rgba(255,215,0,.25);
  border-radius:15px;padding:10px;margin-bottom:12px;align-items:center
}
.cartItem img{width:60px;height:60px;object-fit:cover;border-radius:12px;border:2px solid var(--yellow)}
.cartItem .info{flex:1}
.cartItem .info h4{margin:0;font-size:14px;font-weight:900}
.cartItem .info p{margin:5px 0 0 0;color:#ddd;font-size:13px}
.qtyControl{display:flex;gap:6px;margin-top:8px;justify-content:flex-start}
.qtyControl button{width:28px;height:28px;border:none;border-radius:8px;font-size:18px;font-weight:800;cursor:pointer}
.removeBtn{background:#ff3b3b;color:#fff;border:none;padding:8px 10px;border-radius:10px;font-weight:800;cursor:pointer}
.cart-total{display:flex;justify-content:space-between;margin-top:15px;font-size:18px;font-weight:900}
.orderBtn{width:100%;padding:12px;margin-top:10px;border:none;border-radius:14px;font-weight:900;cursor:pointer;background:var(--yellow);color:#000}

/* Order Modal */
.orderModal{
  position:fixed;top:0;left:0;width:100%;height:100%;
  background:rgba(0,0,0,0.75);
  display:none;
  justify-content:center;align-items:center;
  z-index:2000
}
.orderModalContent{
  width:90%;max-width:420px;background:#000;color:#fff;border:2px solid var(--yellow);
  border-radius:20px;padding:20px;text-align:center;position:relative
}
.orderModalContent input{width:100%;padding:12px;margin:10px 0;border-radius:12px;border:2px solid var(--yellow);background:#111;color:#fff}
.orderModalContent button{width:100%;padding:12px;margin-top:10px;border:none;border-radius:12px;background:var(--yellow);color:#000;font-weight:900;cursor:pointer}
.closeOrder{position:absolute;top:18px;right:18px;font-size:28px;color:var(--yellow);cursor:pointer}

/* Product Modal */
#productModal{
  position:fixed;top:0;left:0;width:100%;height:100%;
  background:rgba(0,0,0,0.8);
  display:none;
  z-index:3000;
  display:flex;align-items:center;justify-content:center
}
#productModal .modalContent{
  width:95%;max-width:420px;background:#fff;border-radius:15px;overflow:hidden;direction:rtl
}
#productModal .modalHeader{
  background:var(--black);color:var(--yellow);
  padding:12px 15px;display:flex;justify-content:space-between;align-items:center
}
#productModal .modalHeader button{background:var(--yellow);color:#000;border:none;border-radius:10px;padding:10px 14px}
#productModal .modalBody{padding:18px}
.product-images{background:#fff;border-radius:15px;padding:15px;box-shadow:0 5px 15px rgba(0,0,0,.15)}
.main-img{width:100%;height:240px;border-radius:12px;object-fit:cover}
.thumbs{margin-top:10px;display:flex;gap:10px;overflow-x:auto}
.thumbs img{width:90px;height:60px;border-radius:10px;object-fit:cover;cursor:pointer;border:2px solid transparent}
.thumbs img.active{border-color:var(--yellow)}

.product-details{background:#fff;border-radius:15px;padding:15px;box-shadow:0 5px 15px rgba(0,0,0,.15)}
.product-title{font-size:20px;font-weight:900;margin:0 0 10px 0}
.product-price{font-size:20px;color:#ff6600;font-weight:900;margin:10px 0}
.product-desc{font-size:14px;line-height:1.6;color:#555;margin-top:10px}
.btns{display:flex;gap:10px;margin-top:15px}
.btn{flex:1;padding:12px 14px;border:none;border-radius:12px;cursor:pointer;font-size:14px;font-weight:700;transition:transform .2s ease,box-shadow .2s ease;box-shadow:0 6px 15px rgba(0,0,0,.2)}
.btn.cart{background:var(--yellow);color:#000}
.btn.whatsapp{background:#25D366;color:#fff}
.btn:hover{transform:translateY(-2px);box-shadow:0 10px 20px rgba(0,0,0,.25)}

.warranty{display:none;margin-top:15px;border:2px solid var(--yellow);background:#fff;color:#000;border-radius:12px;padding:12px 14px}
.warranty h3{margin:0 0 8px 0;font-size:18px;color:#ff6600}
.warranty ul{margin:0;padding-left:18px}
.warranty ul li{margin:6px 0}
.warranty p{margin:6px 0;font-size:14px}

.adminBar{margin-top:15px;background:#000;color:var(--yellow);padding:10px;border-radius:10px;display:none}
.adminBar input,.adminBar textarea{width:100%;padding:8px;margin:5px 0;border-radius:8px;border:1px solid #ddd}
.adminBar button{padding:10px 15px;background:var(--yellow);color:#000;border:none;border-radius:8px;cursor:pointer;font-weight:700}
.adminQty{display:flex;gap:10px;align-items:center;margin:5px 0}
.adminQty button{width:36px;height:36px;border:none;border-radius:8px;font-size:18px;font-weight:700;cursor:pointer}
.adminQty span{font-weight:900;font-size:18px}
.adminQty input{flex:1;padding:8px;border-radius:8px;border:1px solid #ddd;background:#111;color:#fff}

#copyResults{max-height:150px;overflow:auto;border:1px solid #ddd;padding:10px;border-radius:10px;background:#111}
#copyResults div{padding:8px;border-bottom:1px solid #333;cursor:pointer;color:#fff}
#copyResults div.selected{background:#ffd700;color:#000}

/* Category Modal */
.categoryModal{
  position:fixed;top:0;left:0;width:100%;height:100%;
  background:rgba(0,0,0,0.85);
  z-index:2500;
  display:none;
  justify-content:center;align-items:center
}
.categoryModalContent{
  width:95%;max-width:420px;background:#000;border:2px solid var(--yellow);
  border-radius:20px;padding:20px;color:#fff;position:relative
}
.categoryModalContent h2{text-align:center;margin:0 0 15px 0}
.closeCategory{position:absolute;top:15px;left:15px;background:var(--yellow);color:#000;border:none;padding:10px 12px;border-radius:10px;font-weight:700;cursor:pointer}
.categoryGrid{display:grid;grid-template-columns:1fr;gap:15px}
.categoryCard{background:rgba(255,255,255,0.05);border-radius:12px;border:1px solid #333;padding:12px 10px;text-align:center;cursor:pointer}
.categoryCard img{width:100%;height:120px;object-fit:contain;margin-bottom:8px}
.categoryCard .ar{font-size:16px;font-weight:bold;color:var(--yellow)}
.categoryCard .en{font-size:14px;color:#fff;direction:ltr}
#editCatBtn{display:none;margin-bottom:15px;background:var(--yellow);color:#000;border:none;padding:10px 12px;border-radius:10px;font-weight:700;cursor:pointer}
.editPanel{display:none;margin-top:15px;background:rgba(255,255,255,0.05);padding:15px;border-radius:12px;border:1px solid #333}
.editPanel input{width:100%;padding:10px;margin:8px 0;border-radius:10px;border:1px solid #333;background:rgba(0,0,0,0.3);color:#fff}
.editPanel button{padding:10px 12px;border:none;border-radius:10px;font-weight:700;cursor:pointer;margin-top:10px}

/* منع النسخ + F12 */
body{ -webkit-user-select:none; -moz-user-select:none; -ms-user-select:none; user-select:none;}
</style>
</head>

<body>
<header>
  <h2>Chevrolet Site</h2>
  <div class="btns">
    <button onclick="openCategories()">التصنيفات</button>
    <button id="adminBtn" onclick="showLogin()">Admin</button>
  </div>
</header>

<div class="main">
  <div class="banner-cars">
    <img src="https://cdn.salla.sa/mQpGy/dd06a5fb-2e9b-4f97-87be-c76dfdf02190-1000x1000-UiKRN84uJnxNI4O2A0mcIHD5lIcoIvmywG7AJ7vx.jpg" class="active">
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSJn8zvfImPaKGVK4ZJIrrIPTdLMjMfIEpf1GQMGQiJpI6J_JAlhapRTwc6&s=10">
  </div>

  <div class="searchBar">
    <input id="searchInput" placeholder="اكتب اسم القطعة" onkeyup="searchProducts()">
    <button id="searchBtn" onclick="toggleSearch()">بحث</button>
    <button id="catBtn" onclick="openCategories()">التصنيفات</button>
  </div>

  <div class="product-grid" id="products"></div>
</div>

<div id="cartModal" class="cartModal">
  <div class="cartModalContent">
    <span class="closeCart" onclick="toggleCart()">&times;</span>
    <h2>سلة المشتريات</h2>
    <div class="cartItems" id="cartItems"></div>
    <div class="cart-total">
      <span>المجموع:</span>
      <span id="cartTotal">0</span><span>$</span>
    </div>
    <button class="orderBtn" onclick="showOrderBox()">تثبيت الطلب</button>
  </div>
</div>

<div class="cartBtn" onclick="toggleCart()">🛒<span id="cartCount">0</span></div>

<div id="orderModal" class="orderModal">
  <div class="orderModalContent">
    <span class="closeOrder" onclick="closeOrderModal()">&times;</span>
    <h2>بيانات الزبون</h2>
    <input id="custName" placeholder="الاسم">
    <input id="custPhone" placeholder="رقم الهاتف">
    <input id="custAddress" placeholder="العنوان">
    <button onclick="sendOrder()">إرسال الطلب</button>
  </div>
</div>

<div id="loginModal">
  <div style="display:flex;justify-content:center;align-items:center;position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.75);z-index:2500;">
    <div style="width:90%;max-width:360px;background:#000;color:#fff;border:2px solid var(--yellow);border-radius:20px;padding:20px;text-align:center;">
      <h3>تسجيل دخول Admin</h3>
      <input id="username" placeholder="اسم المستخدم" style="width:100%;padding:12px;margin:10px 0;border-radius:12px;border:2px solid var(--yellow);background:#111;color:#fff;">
      <input id="password" placeholder="كلمة المرور" type="password" style="width:100%;padding:12px;margin:10px 0;border-radius:12px;border:2px solid var(--yellow);background:#111;color:#fff;">
      <button onclick="login()" style="width:100%;padding:12px;border:none;border-radius:12px;background:var(--yellow);color:#000;font-weight:900;cursor:pointer;">دخول</button>
      <button onclick="closeLogin()" style="width:100%;padding:12px;margin-top:10px;border:none;border-radius:12px;background:#ff3b3b;color:#fff;font-weight:900;cursor:pointer;">إغلاق</button>
    </div>
  </div>
</div>

<div id="productModal">
  <div class="modalContent">
    <div class="modalHeader">
      <span>تفاصيل المنتج</span>
      <button onclick="closeProduct()">إغلاق</button>
    </div>
    <div class="modalBody">
      <div class="product-images">
        <img id="mainImg" class="main-img" src="">
        <div class="thumbs">
          <img id="thumb1" src="" class="active" onclick="changeImg(this)">
          <img id="thumb2" src="" onclick="changeImg(this)">
          <img id="thumb3" src="" onclick="changeImg(this)">
        </div>
      </div>

      <div class="product-details">
        <h1 id="prodTitle" class="product-title"></h1>
        <div id="prodPrice" class="product-price"></div>
        <div id="prodDesc" class="product-desc"></div>

        <div class="btns">
          <button class="btn cart" onclick="addToCartFromModal()">أضف للسلة</button>
          <button class="btn whatsapp" onclick="sendWhatsApp()">واتساب</button>
        </div>

        <div class="warranty" id="warrantyBox"></div>

        <div id="adminBar" class="adminBar">
          <h3>لوحة تعديل Admin</h3>

          <label>عنوان المنتج:</label>
          <input id="editTitle" type="text">

          <label>السعر:</label>
          <div class="adminQty">
            <button onclick="adminPrice(-1)">-</button>
            <span id="adminPrice">0</span>
            <button onclick="adminPrice(1)">+</button>
          </div>
          <input id="editPrice" type="text">

          <label>الوصف:</label>
          <textarea id="editDesc" rows="3"></textarea>

          <button onclick="saveAdmin()">حفظ التعديلات</button>
        </div>

      </div>
    </div>
  </div>
</div>

<div id="categoryModal" class="categoryModal">
  <div class="categoryModalContent">
    <button class="closeCategory" onclick="closeCategories()">إغلاق</button>
    <h2>التصنيفات</h2>
    <button id="editCatBtn" onclick="toggleEditPanel()">تعديل التصنيفات</button>
    <div class="editPanel" id="editPanel">
      <h3>إضافة تصنيف جديد</h3>
      <input id="newCatAr" placeholder="اسم التصنيف بالعربي">
      <input id="newCatEn" placeholder="اسم التصنيف بالانجليزي">
      <input id="newCatImg" placeholder="رابط صورة التصنيف">
      <button onclick="addCategory()">إضافة</button>
      <hr style="border:1px solid #333;margin:15px 0;">
      <h3>تعديل / حذف تصنيف</h3>
      <input id="editCatIndex" placeholder="رقم التصنيف">
      <input id="editCatAr" placeholder="اسم جديد بالعربي">
      <input id="editCatEn" placeholder="اسم جديد بالانجليزي">
      <input id="editCatImg" placeholder="رابط صورة جديد">
      <button onclick="editCategory()">تعديل</button>
      <button onclick="deleteCategory()" style="background:#ff3b3b;color:#fff;">حذف</button>
    </div>
    <div class="categoryGrid" id="categoryGrid"></div>
  </div>
</div>

<script>
let products=[],cart=[];let selectedProductIndex=null;
const adminUser="lilkadi1",adminPass="19961996lilkadi";

function isAdmin(){return localStorage.getItem("isAdmin")==="true"}

function showLogin(){document.getElementById("loginModal").style.display="block"}
function closeLogin(){document.getElementById("loginModal").style.display="none"}

function login(){
  const u=document.getElementById("username").value;
  const p=document.getElementById("password").value;
  if(u===adminUser && p===adminPass){
    localStorage.setItem("isAdmin","true");
    document.getElementById("loginModal").style.display="none";
    alert("تم الدخول");
    showAdminBar();
  }else alert("خطأ");
}

const bannerImages=document.querySelectorAll(".banner-cars img");
let current=0;
setInterval(()=>{
  bannerImages.forEach(i=>i.classList.remove("active"));
  current=(current+1)%bannerImages.length;
  bannerImages[current].classList.add("active")
},3000);

const list=document.getElementById("products");

fetch("https://api.sheetbest.com/sheets/044c3d5a-80e6-42eb-87cc-488eba7900aa")
.then(r=>r.json())
.then(data=>{
  products=data.map((item,index)=>({
    id:index+1,
    name:item['اسم المادة']||item['name']||"بدون اسم",
    price:parseFloat(item['البيع']||item['price']||0),
    desc:(item['الوصف']||"لا يوجد وصف"),
    imgs:[item['صورة1']||"https://cdn.salla.sa/mQpGy/dd06a5fb-2e9b-4f97-87be-c76dfdf02190-1000x1000-UiKRN84uJnxNI4O2A0mcIHD5lIcoIvmywG7AJ7vx.jpg",item['صورة2']||item['صورة1'],item['صورة3']||item['صورة1']],
    qty:1,
    category:item['التصنيف']||"غير مصنف"
  }));
  renderProducts();
  showAdminBar();
});

function renderProducts(){
  list.innerHTML="";
  products.forEach(p=>{
    const div=document.createElement("div");
    div.className="product";
    div.onclick=()=>openProduct(p.id);
    div.innerHTML=`
      <h4>${p.name}</h4>
      <img src="${p.imgs[0]}" alt="Product Image">
      <div class="price">${p.price} $</div>
      <div class="qty">
        <button class="dec" onclick="event.stopPropagation();changeQty(${p.id},-1)">-</button>
        <span id="qty${p.id}">${p.qty}</span>
        <button class="inc" onclick="event.stopPropagation();changeQty(${p.id},1)">+</button>
      </div>
      <a href="#" class="whatsappBtnProduct" onclick="event.stopPropagation();addToCart(${p.id})">أضف للطلب</a>
    `;
    list.appendChild(div);
  });
}

function searchProducts(){
  const term=document.getElementById("searchInput").value.toLowerCase();
  const filtered=products.filter(p=>p.name.toLowerCase().includes(term));
  list.innerHTML="";
  filtered.forEach(p=>{
    const div=document.createElement("div");
    div.className="product";
    div.onclick=()=>openProduct(p.id);
    div.innerHTML=`
      <h4>${p.name}</h4>
      <img src="${p.imgs[0]}" alt="Product Image">
      <div class="price">${p.price} $</div>
      <div class="qty">
        <button class="dec" onclick="event.stopPropagation();changeQty(${p.id},-1)">-</button>
        <span id="qty${p.id}">${p.qty}</span>
        <button class="inc" onclick="event.stopPropagation();changeQty(${p.id},1)">+</button>
      </div>
      <a href="#" class="whatsappBtnProduct" onclick="event.stopPropagation();addToCart(${p.id})">أضف للطلب</a>
    `;
    list.appendChild(div);
  });
}

function changeQty(id,val){const p=products.find(x=>x.id===id);p.qty+=val;if(p.qty<1)p.qty=1;document.getElementById(`qty${id}`).innerText=p.qty}
function addToCart(id){const p=products.find(x=>x.id===id);const ex=cart.find(x=>x.id===p.id);if(ex)ex.qty+=p.qty;else cart.push({...p});updateCart()}
function updateCart(){const box=document.getElementById("cartItems");box.innerHTML="";let total=0;cart.forEach(item=>{const div=document.createElement("div");div.className="cartItem";div.innerHTML=`<img src="${item.imgs[0]}"><div class="info"><h4>${item.name}</h4><p>${item.price} $ لكل وحدة</p><div class="qtyControl"><button class="dec" onclick="changeCartQty(${item.id},-1)">-</button><span>${item.qty}</span><button class="inc" onclick="changeCartQty(${item.id},1)">+</button></div></div><button class="removeBtn" onclick="removeCart(${item.id})">حذف</button>`;box.appendChild(div);total+=item.price*item.qty});document.getElementById("cartTotal").innerText=total;document.getElementById("cartCount").innerText=cart.reduce((a,b)=>a+b.qty,0)}
function changeCartQty(id,val){const item=cart.find(x=>x.id===id);item.qty+=val;if(item.qty<1)item.qty=1;updateCart()}
function removeCart(id){cart=cart.filter(x=>x.id!==id);updateCart()}
function toggleCart(){const m=document.getElementById("cartModal");m.style.display=m.style.display==="flex"?"none":"flex";if(m.style.display==="flex")updateCart()}
function showOrderBox(){document.getElementById("cartModal").style.display="none";document.getElementById("orderModal").style.display="flex"}
function closeOrderModal(){document.getElementById("orderModal").style.display="none"}
function sendOrder(){
  const name=document.getElementById("custName").value;
  const phone=document.getElementById("custPhone").value;
  const address=document.getElementById("custAddress").value;
  if(!name||!phone||!address){alert("ادخل الاسم، رقم الهاتف، والعنوان");return}

  let msg=`طلبية جديدة:\nالزبون: ${name}\nرقم الهاتف: ${phone}\nالعنوان: ${address}\n\nالقطع:\n`;
  let total=0;
  cart.forEach(item=>{
    const it=item.price*item.qty;
    msg+=`${item.name} - ${item.qty} × ${item.price} = ${it} $\n`;
    total+=it;
  });
  msg+=`\nالمجموع: ${total}$`;
  window.open(`https://wa.me/9647872159504?text=${encodeURIComponent(msg)}`)
}

function openProduct(id){
  selectedProductIndex=products.findIndex(x=>x.id===id);
  const p=products[selectedProductIndex];

  document.getElementById("mainImg").src=p.imgs[0];
  document.getElementById("prodTitle").innerText=p.name;
  document.getElementById("prodPrice").innerText=p.price+" $";
  document.getElementById("prodDesc").innerText=p.desc;

  document.getElementById("thumb1").src=p.imgs[0];
  document.getElementById("thumb2").src=p.imgs[1];
  document.getElementById("thumb3").src=p.imgs[2];

  document.getElementById("editTitle").value=p.name;
  document.getElementById("editPrice").value=p.price;
  document.getElementById("editDesc").value=p.desc;

  document.getElementById("adminPrice").innerText=p.price; // مهم

  document.getElementById("productModal").style.display="flex";
  showAdminBar();
}

function closeProduct(){document.getElementById("productModal").style.display="none"}
function changeImg(el){document.getElementById("mainImg").src=el.src;document.querySelectorAll(".thumbs img").forEach(i=>i.classList.remove("active"));el.classList.add("active")}
function addToCartFromModal(){const p=products[selectedProductIndex];const ex=cart.find(x=>x.id===p.id);if(ex)ex.qty+=p.qty;else cart.push({...p});updateCart();alert("تم إضافة المنتج للسلة")}
function sendWhatsApp(){const msg="أريد أطلب هذا المنتج: "+document.getElementById("prodTitle").innerText;window.open(`https://wa.me/9647872159504?text=${encodeURIComponent(msg)}`)}

function showAdminBar(){document.getElementById("adminBar").style.display=isAdmin()?"block":"none"}

/* ===== دالة صعود/نزول السعر ===== */
function adminPrice(val){
  let price = parseFloat(document.getElementById("adminPrice").innerText) || 0;
  price += val;
  if(price < 0) price = 0;
  document.getElementById("adminPrice").innerText = price;
  document.getElementById("editPrice").value = price;
}

function saveAdmin(){
  if(selectedProductIndex===null)return;
  const p=products[selectedProductIndex];
  p.name=document.getElementById("editTitle").value;
  p.price=parseFloat(document.getElementById("editPrice").value)||0;
  p.desc=document.getElementById("editDesc").value.trim();
  renderProducts();
  openProduct(p.id);
  alert("تم حفظ التعديلات")
}

/* Categories */
let categories=[{ar:"الزيوت والسوائل",en:"Oils & Fluids",img:"https://cdn-icons-png.flaticon.com/512/2913/2913894.png"},
{ar:"الفلاتر",en:"Filters",img:"https://cdn-icons-png.flaticon.com/512/1605/1605750.png"},
{ar:"المحرك",en:"Engine",img:"https://cdn-icons-png.flaticon.com/512/919/919846.png"}];

function saveCategories(){localStorage.setItem("categories",JSON.stringify(categories))}
function loadCategories(){const s=localStorage.getItem("categories");if(s)categories=JSON.parse(s)}
loadCategories();

function renderCategories(){
  const g=document.getElementById("categoryGrid");
  g.innerHTML="";
  categories.forEach((c,idx)=>{
    g.innerHTML+=`
      <div class="categoryCard" onclick="filterByCategory('${c.ar}')">
        <img src="${c.img}">
        <div class="ar">${c.ar}</div>
        <div class="en">${c.en}</div>
        <div style="font-size:12px;color:#fff;margin-top:5px;">رقم: ${idx+1}</div>
      </div>
    `
  })
}

function openCategories(){document.getElementById("categoryModal").style.display="flex";renderCategories();checkEditButton()}
function closeCategories(){document.getElementById("categoryModal").style.display="none"}

function checkEditButton(){
  document.getElementById("editCatBtn").style.display=isAdmin()?"block":"none";
  document.getElementById("editPanel").style.display="none";
}

function toggleEditPanel(){
  if(!isAdmin()){alert("فقط Admin");return}
  const p=document.getElementById("editPanel");
  p.style.display=p.style.display==="block"?"none":"block";
}

function addCategory(){
  if(!isAdmin()){alert("فقط Admin");return}
  const ar=document.getElementById("newCatAr").value;
  const en=document.getElementById("newCatEn").value;
  const img=document.getElementById("newCatImg").value;
  if(!ar||!en||!img){alert("اكمل الحقول");return}
  categories.push({ar,en,img});
  saveCategories();
  renderCategories();
  alert("تم إضافة")
}

function editCategory(){
  if(!isAdmin()){alert("فقط Admin");return}
  const idx=parseInt(document.getElementById("editCatIndex").value)-1;
  if(idx<0||idx>=categories.length){alert("رقم غير صحيح");return}
  const ar=document.getElementById("editCatAr").value;
  const en=document.getElementById("editCatEn").value;
  const img=document.getElementById("editCatImg").value;
  if(ar)categories[idx].ar=ar;
  if(en)categories[idx].en=en;
  if(img)categories[idx].img=img;
  saveCategories();
  renderCategories();
  alert("تم تعديل")
}

function deleteCategory(){
  if(!isAdmin()){alert("فقط Admin");return}
  const idx=parseInt(document.getElementById("editCatIndex").value)-1;
  if(idx<0||idx>=categories.length){alert("رقم غير صحيح");return}
  categories.splice(idx,1);
  saveCategories();
  renderCategories();
  alert("تم حذف")
}

function filterByCategory(cat){
  const f=products.filter(p=>p.category===cat);
  list.innerHTML="";
  f.forEach(p=>{
    const div=document.createElement("div");
    div.className="product";
    div.onclick=()=>openProduct(p.id);
    div.innerHTML=`
      <h4>${p.name}</h4>
      <img src="${p.imgs[0]}" alt="Product Image">
      <div class="price">${p.price} $</div>
      <div class="qty">
        <button class="dec" onclick="event.stopPropagation();changeQty(${p.id},-1)">-</button>
        <span id="qty${p.id}">${p.qty}</span>
        <button class="inc" onclick="event.stopPropagation();changeQty(${p.id},1)">+</button>
      </div>
      <a href="#" class="whatsappBtnProduct" onclick="event.stopPropagation();addToCart(${p.id})">أضف للطلب</a>
    `;
    list.appendChild(div);
  });
  closeCategories();
}

function toggleSearch(){document.getElementById("searchInput").focus()}

document.getElementById("adminBtn").style.display="block";
</script>
</body>
</html>
