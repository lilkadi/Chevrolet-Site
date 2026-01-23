<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Chevrolet Site</title>

<style>
:root{
  --black:#000;
  --yellow:#ffd700;
  --white:#fff;
  --gray:#f2f2f2;
  --darkGray:#111;
}
*{box-sizing:border-box}
body{
  margin:0;
  font-family:tahoma;
  background:#000;
  color:#fff;
  user-select:none;
}
.main{
  width:100%;
  max-width:430px;
  padding:0 15px;
}

/* Header */
header{
  background:var(--black);
  color:var(--yellow);
  padding:15px 20px;
  position:sticky;
  top:0;
  z-index:1000;
  display:flex;
  justify-content:space-between;
  align-items:center;
}
header h2{
  margin:0;
  font-size:22px;
}
header button{
  background:var(--yellow);
  color:var(--black);
  border:none;
  padding:10px 12px;
  border-radius:10px;
  font-weight:700;
  cursor:pointer;
  font-size:14px;
}

/* Products Grid */
.product-grid{
  display:grid;
  grid-template-columns:repeat(1,1fr);
  gap:18px;
  padding:15px 0;
}
.product{
  background:#fff;
  color:#000;
  border-radius:15px;
  padding:12px;
  box-shadow:0 8px 20px rgba(0,0,0,.25);
}
.product img{
  width:100%;
  height:160px;
  object-fit:cover;
  border-radius:12px;
}
.product h4{
  margin:10px 0 5px 0;
  font-size:18px;
  font-weight:800;
}
.product .price{
  color:#ff6600;
  font-weight:900;
  margin:5px 0;
  font-size:18px;
}
.qty{
  display:flex;
  justify-content:center;
  gap:8px;
  margin:10px 0;
}
.qty button{
  width:36px;
  height:36px;
  border:none;
  border-radius:8px;
  font-size:18px;
  font-weight:700;
}
.inc{background:var(--yellow)}
.dec{background:#ff3b3b;color:#fff}

/* Cart Button */
.cartBtn{
  position:fixed;
  bottom:20px;
  right:20px;
  background:var(--black);
  color:var(--yellow);
  border-radius:50%;
  padding:16px;
  font-size:22px;
  z-index:1000;
}
#cartCount{font-weight:900;margin-left:8px}

/* Modals */
.modal{
  position:fixed;top:0;left:0;width:100%;height:100%;
  background:rgba(0,0,0,0.8);
  display:none;
  align-items:center;
  justify-content:center;
  z-index:1500;
}
.modalContent{
  width:95%;max-width:520px;
  background:#000;color:#fff;
  border:2px solid var(--yellow);
  border-radius:20px;
  padding:20px;
  position:relative;
}
.modalContent h2{text-align:center;margin:0;font-size:22px}
.closeBtn{
  position:absolute;top:15px;right:15px;
  font-size:30px;color:var(--yellow);
  cursor:pointer;
}
.cartItems{margin-top:15px;max-height:320px;overflow:auto}
.cartItem{
  display:flex;gap:10px;background:#111;border:1px solid rgba(255,215,0,.25);
  border-radius:15px;padding:10px;margin-bottom:12px;align-items:center;
}
.cartItem img{width:70px;height:70px;object-fit:cover;border-radius:12px;border:2px solid var(--yellow)}
.cartItem .info{flex:1}
.cartItem .info h4{margin:0;font-size:15px;font-weight:900}
.cartItem .info p{margin:5px 0 0 0;color:#ddd;font-size:13px}
.qtyControl{display:flex;gap:6px;margin-top:8px;justify-content:flex-start}
.qtyControl button{width:28px;height:28px;border:none;border-radius:8px;font-size:18px;font-weight:800;cursor:pointer}
.removeBtn{background:#ff3b3b;color:#fff;border:none;padding:8px 10px;border-radius:10px;font-weight:800;cursor:pointer}
.cart-total{display:flex;justify-content:space-between;margin-top:15px;font-size:18px;font-weight:900}
.orderBtn{width:100%;padding:12px;margin-top:10px;border:none;border-radius:14px;font-weight:900;cursor:pointer;background:var(--yellow);color:#000}

/* Admin Panel */
.adminBar{
  margin-top:15px;
  background:#000;
  color:var(--yellow);
  padding:10px;
  border-radius:10px;
  display:none;
}
.adminBar input{
  width:100%;
  padding:8px;
  margin:5px 0;
  border-radius:8px;
  border:1px solid #ddd;
}
.adminBar button{
  padding:10px 15px;
  background:var(--yellow);
  color:#000;
  border:none;
  border-radius:8px;
  cursor:pointer;
  font-weight:700;
}

/* Admin Navigation */
.navBtn{
  width:48px;
  height:48px;
  border:none;
  border-radius:12px;
  font-size:22px;
  font-weight:900;
  background:var(--yellow);
  color:#000;
  cursor:pointer;
}

/* Dark/Light */
body.light{background:#fff;color:#000}
body.light header{background:#fff;color:#000}
body.light header button{background:#000;color:#fff}
body.light .product{background:#000;color:#fff}
body.light .modalContent{background:#fff;color:#000}
</style>

<script>
/* منع النسخ + F12 */
document.addEventListener("contextmenu", e => e.preventDefault());
document.addEventListener("keydown", e => {
  if(e.key === "F12" || (e.ctrlKey && e.shiftKey && e.key === "I")) e.preventDefault();
});

/* Admin بيانات ثابتة */
const adminUser="lilkadi1";
const adminPass="19961996lilkadi";

/* منتجات */
let products = [
  {id:1,name:"قطعة 1",price:20,desc:"وصف القطعة 1",img:"https://via.placeholder.com/400x200",qty:1},
  {id:2,name:"قطعة 2",price:35,desc:"وصف القطعة 2",img:"https://via.placeholder.com/400x200",qty:1},
  {id:3,name:"قطعة 3",price:50,desc:"وصف القطعة 3",img:"https://via.placeholder.com/400x200",qty:1}
];

let cart=[]; 
let currentIndex = 0;
let selectedProduct=null;

/* عرض المنتجات */
function renderProducts(){
  const list=document.getElementById("products");
  list.innerHTML="";
  products.forEach(p=>{
    const div=document.createElement("div");
    div.className="product";
    div.innerHTML=`
      <h4>${p.name}</h4>
      <img src="${p.img}">
      <div class="price">${p.price} $</div>
      <div class="qty">
        <button class="dec" onclick="changeQty(${p.id},-1)">-</button>
        <span id="qty${p.id}">${p.qty}</span>
        <button class="inc" onclick="changeQty(${p.id},1)">+</button>
      </div>
      <div class="btns">
        <button onclick="addToCart(${p.id})">أضف للسلة</button>
        <button onclick="openProduct(${p.id})">تفاصيل</button>
      </div>
    `;
    list.appendChild(div);
  });
}

/* تعديل كمية المنتج */
function changeQty(id,val){
  const p=products.find(x=>x.id===id);
  p.qty+=val;
  if(p.qty<1)p.qty=1;
  document.getElementById(`qty${id}`).innerText=p.qty;
}

/* سلة */
function addToCart(id){
  const p=products.find(x=>x.id===id);
  const ex=cart.find(x=>x.id===id);
  if(ex) ex.qty += p.qty;
  else cart.push({...p});
  updateCart();
}
function updateCart(){
  const box=document.getElementById("cartItems");
  box.innerHTML="";
  let total=0;
  cart.forEach(item=>{
    const div=document.createElement("div");
    div.className="cartItem";
    div.innerHTML=`
      <img src="${item.img}">
      <div class="info">
        <h4>${item.name}</h4>
        <p>${item.price} $</p>
        <div class="qtyControl">
          <button onclick="changeCartQty(${item.id},-1)">-</button>
          <span>${item.qty}</span>
          <button onclick="changeCartQty(${item.id},1)">+</button>
        </div>
      </div>
      <button class="removeBtn" onclick="removeCart(${item.id})">حذف</button>
    `;
    box.appendChild(div);
    total += item.price * item.qty;
  });
  document.getElementById("cartTotal").innerText=total;
  document.getElementById("cartCount").innerText = cart.reduce((a,b)=>a+b.qty,0);
}
function changeCartQty(id,val){
  const item=cart.find(x=>x.id===id);
  item.qty += val;
  if(item.qty<1) item.qty=1;
  updateCart();
}
function removeCart(id){
  cart = cart.filter(x=>x.id!==id);
  updateCart();
}
function toggleCart(){
  const m=document.getElementById("cartModal");
  m.style.display = m.style.display === "flex" ? "none" : "flex";
  updateCart();
}

/* الطلب */
function showOrderBox(){
  document.getElementById("cartModal").style.display="none";
  document.getElementById("orderModal").style.display="flex";
}
function closeOrderModal(){
  document.getElementById("orderModal").style.display="none";
}
function sendOrder(){
  const name=document.getElementById("custName").value;
  const phone=document.getElementById("custPhone").value;
  const address=document.getElementById("custAddress").value;
  if(!name||!phone||!address){alert("اكمل البيانات");return}

  let msg=`طلب جديد\nالاسم: ${name}\nالهاتف: ${phone}\nالعنوان: ${address}\n\nالقطع:\n`;
  let total=0;
  cart.forEach(i=>{
    msg += `${i.name} x${i.qty} = ${i.price*i.qty}$\n`;
    total += i.price*i.qty;
  });
  msg += `\nالمجموع: ${total}$`;

  window.open(`https://wa.me/9647872159504?text=${encodeURIComponent(msg)}`);
}

/* فتح تفاصيل المنتج */
function openProduct(id){
  currentIndex = products.findIndex(x => x.id === id);
  showProduct();
  document.getElementById("productModal").style.display="flex";
  showAdminBar();
}
function closeProduct(){document.getElementById("productModal").style.display="none";}

function showProduct(){
  const p = products[currentIndex];
  document.getElementById("prodTitle").innerText = p.name;
  document.getElementById("prodPrice").innerText = p.price + " $";
  document.getElementById("prodDesc").innerText = p.desc;
  document.getElementById("prodImg").src = p.img;

  document.getElementById("editName").value = p.name;
  document.getElementById("editPrice").value = p.price;
  document.getElementById("editImg").value = p.img;
}

/* Admin Login */
function showLogin(){
  document.getElementById("loginModal").style.display="block";
}
function closeLogin(){
  document.getElementById("loginModal").style.display="none";
}
function login(){
  const u=document.getElementById("username").value;
  const p=document.getElementById("password").value;
  if(u===adminUser && p===adminPass){
    localStorage.setItem("isAdmin","true");
    closeLogin();
    showAdminBar();
    alert("تم الدخول");
  }else alert("خطأ");
}
function showAdminBar(){
  const admin = localStorage.getItem("isAdmin")==="true";
  document.getElementById("adminBar").style.display = admin ? "block" : "none";
}

/* Admin Navigation */
function prevProduct(){
  if(currentIndex > 0){
    currentIndex--;
    showProduct();
  }
}
function nextProduct(){
  if(currentIndex < products.length - 1){
    currentIndex++;
    showProduct();
  }
}

/* Save Admin */
function saveAdmin(){
  const p = products[currentIndex];
  p.name = document.getElementById("editName").value;
  p.price = parseFloat(document.getElementById("editPrice").value) || 0;
  p.img = document.getElementById("editImg").value;

  renderProducts();
  showProduct();
  alert("تم الحفظ");
}

/* Theme */
function toggleTheme(){
  document.body.classList.toggle("light");
}

/* Init */
window.onload = function(){
  renderProducts();
  document.getElementById("cartModal").style.display="none";
  document.getElementById("orderModal").style.display="none";
  document.getElementById("productModal").style.display="none";
  document.getElementById("loginModal").style.display="none";
  showAdminBar();
}
</script>
</head>

<body>
<header>
  <h2>Chevrolet Site</h2>
  <div class="btns">
    <button onclick="showLogin()">Admin</button>
    <button onclick="toggleTheme()">🌙/☀️</button>
  </div>
</header>

<div class="main">
  <div class="product-grid" id="products"></div>
</div>

<div class="cartBtn" onclick="toggleCart()">🛒<span id="cartCount">0</span></div>

<!-- Cart Modal -->
<div id="cartModal" class="modal">
  <div class="modalContent">
    <span class="closeBtn" onclick="toggleCart()">&times;</span>
    <h2>سلة المشتريات</h2>
    <div class="cartItems" id="cartItems"></div>
    <div class="cart-total">
      <span>المجموع:</span>
      <span id="cartTotal">0</span><span>$</span>
    </div>
    <button class="orderBtn" onclick="showOrderBox()">تثبيت الطلب</button>
  </div>
</div>

<!-- Order Modal -->
<div id="orderModal" class="modal">
  <div class="modalContent">
    <span class="closeBtn" onclick="closeOrderModal()">&times;</span>
    <h2>بيانات الزبون</h2>
    <input id="custName" placeholder="الاسم">
    <input id="custPhone" placeholder="رقم الهاتف">
    <input id="custAddress" placeholder="العنوان">
    <button onclick="sendOrder()">إرسال الطلب</button>
  </div>
</div>

<!-- Login Modal -->
<div id="loginModal" class="modal">
  <div class="modalContent" style="max-width:360px;">
    <span class="closeBtn" onclick="closeLogin()">&times;</span>
    <h2>تسجيل دخول Admin</h2>
    <input id="username" placeholder="اسم المستخدم">
    <input id="password" type="password" placeholder="كلمة المرور">
    <button onclick="login()">دخول</button>
  </div>
</div>

<!-- Product Modal -->
<div id="productModal" class="modal">
  <div class="modalContent">
    <span class="closeBtn" onclick="closeProduct()">&times;</span>

    <!-- أزرار صعود ونزول داخل شاشة المنتج -->
    <div style="display:flex; justify-content:space-between; margin-bottom:10px;">
      <button onclick="prevProduct()" class="navBtn">↑</button>
      <button onclick="nextProduct()" class="navBtn">↓</button>
    </div>

    <h2 id="prodTitle"></h2>
    <img id="prodImg" src="" style="width:100%; border-radius:12px; margin:10px 0;">
    <div class="product-desc" id="prodDesc"></div>
    <div class="product-price" id="prodPrice"></div>

    <div class="adminBar" id="adminBar">
      <h3>تعديل المنتج</h3>
      <input id="editName" placeholder="اسم المنتج">
      <input id="editPrice" placeholder="السعر">
      <input id="editImg" placeholder="رابط الصورة">
      <button onclick="saveAdmin()">حفظ التعديل</button>
    </div>
  </div>
</div>

</body>
</html>
