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
}

/* كل النوافذ مخفية افتراضياً */
.cartModal,
.orderModal,
#productModal,
#categoryModal,
#loginModal {
  display: none;
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
  letter-spacing:2px;
}
header .btns{
  display:flex;
  gap:10px;
}
header button{
  background:var(--yellow);
  color:var(--black);
  border:none;
  padding:10px 12px;
  border-radius:10px;
  font-weight:700;
  cursor:pointer;
}

/* Banner */
.banner-cars{
  position:relative;
  width:100%;
  height:280px;
  overflow:hidden;
  margin-bottom:10px;
  border-bottom:2px solid var(--yellow);
}
.banner-cars img{
  width:100%;
  height:280px;
  object-fit:cover;
  position:absolute;
  top:0;
  left:0;
  transition:opacity 1s ease;
  opacity:0;
}
.banner-cars img.active{opacity:1}

/* Container */
.container{
  padding:15px;
  max-width:1200px;
  margin:0 auto;
}

/* Search */
.searchBar{
  display:flex;
  gap:10px;
  justify-content:center;
  margin:15px 0;
}
#searchInput{
  width:100%;
  max-width:520px;
  padding:12px;
  border-radius:12px;
  border:2px solid var(--yellow);
  background:#111;
  color:#fff;
  font-size:16px;
}
#searchBtn{
  padding:12px 20px;
  border:none;
  border-radius:12px;
  background:var(--yellow);
  color:#000;
  font-weight:700;
  cursor:pointer;
}
#carSelect{
  padding:12px;
  border-radius:12px;
  border:2px solid var(--yellow);
  background:#111;
  color:#fff;
  font-size:16px;
}
#catBtn{
  padding:12px 18px;
  border:none;
  border-radius:12px;
  background:var(--yellow);
  color:#000;
  font-weight:700;
  cursor:pointer;
}

/* Products */
.product-grid{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:18px;
}
.product{
  background:#fff;
  color:#000;
  border-radius:15px;
  padding:12px;
  box-shadow:0 8px 20px rgba(0,0,0,.25);
  cursor:pointer;
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
.whatsappBtnProduct{
  display:block;
  margin:10px auto 0 auto;
  background:#25D366;
  color:#fff;
  border-radius:10px;
  padding:10px 12px;
  text-align:center;
  text-decoration:none;
  width:100%;
  font-size:14px;
  font-weight:700;
}

/* Back Home */
#backHome{
  display:none;
  text-align:center;
  margin:15px 0;
}
#backHome button{
  padding:10px 15px;
  border:none;
  border-radius:12px;
  background:var(--yellow);
  color:#000;
  font-weight:800;
  cursor:pointer;
}

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
  box-shadow:0 8px 20px rgba(0,0,0,.4);
}
#cartCount{
  font-weight:900;
  margin-left:8px;
}

/* Cart Modal */
.cartModal{
  position:fixed;
  top:0; left:0;
  width:100%; height:100%;
  background:rgba(0,0,0,0.8);
  display:flex;
  align-items:center;
  justify-content:center;
  z-index:1500;
}
.cartModalContent{
  width:90%;
  max-width:520px;
  background:#000;
  color:#fff;
  border:2px solid var(--yellow);
  border-radius:20px;
  padding:20px;
  position:relative;
  box-shadow:0 20px 60px rgba(0,0,0,.7);
}
.cartModalContent h2{
  text-align:center;
  margin:0;
  font-size:22px;
}
.cartModalContent .closeCart{
  position:absolute;
  top:15px;
  right:15px;
  font-size:30px;
  color:var(--yellow);
  cursor:pointer;
}
.cartItems{
  margin-top:15px;
  max-height:320px;
  overflow:auto;
}
.cartItem{
  display:flex;
  gap:10px;
  background:#111;
  border:1px solid rgba(255,215,0,.25);
  border-radius:15px;
  padding:10px;
  margin-bottom:12px;
  align-items:center;
}
.cartItem img{
  width:70px;
  height:70px;
  object-fit:cover;
  border-radius:12px;
  border:2px solid var(--yellow);
}
.cartItem .info{
  flex:1;
}
.cartItem .info h4{
  margin:0;
  font-size:15px;
  font-weight:900;
}
.cartItem .info p{
  margin:5px 0 0 0;
  color:#ddd;
  font-size:13px;
}
.qtyControl{
  display:flex;
  gap:6px;
  margin-top:8px;
  justify-content:flex-start;
}
.qtyControl button{
  width:28px;
  height:28px;
  border:none;
  border-radius:8px;
  font-size:18px;
  font-weight:800;
  cursor:pointer;
}
.qtyControl .inc{background:var(--yellow)}
.qtyControl .dec{background:#ff3b3b;color:#fff}
.removeBtn{
  background:#ff3b3b;
  color:#fff;
  border:none;
  padding:8px 10px;
  border-radius:10px;
  font-weight:800;
  cursor:pointer;
}
.cart-total{
  display:flex;
  justify-content:space-between;
  margin-top:15px;
  font-size:18px;
  font-weight:900;
}
.orderBtn{
  width:100%;
  padding:12px;
  margin-top:10px;
  border:none;
  border-radius:14px;
  font-weight:900;
  cursor:pointer;
  background:var(--yellow);
  color:#000;
}

/* Order Modal */
.orderModal{
  position:fixed;
  top:0; left:0;
  width:100%; height:100%;
  background:rgba(0,0,0,0.75);
  display:flex;
  justify-content:center;
  align-items:center;
  z-index:2000;
}
.orderModalContent{
  width:90%;
  max-width:420px;
  background:#000;
  color:#fff;
  border:2px solid var(--yellow);
  border-radius:20px;
  padding:20px;
  text-align:center;
  position:relative;
}
.orderModalContent input{
  width:100%;
  padding:12px;
  margin:10px 0;
  border-radius:12px;
  border:2px solid var(--yellow);
  background:#111;
  color:#fff;
}
.orderModalContent button{
  width:100%;
  padding:12px;
  margin-top:10px;
  border:none;
  border-radius:12px;
  background:var(--yellow);
  color:#000;
  font-weight:900;
  cursor:pointer;
}
.closeOrder{
  position:absolute;
  top:18px;
  right:18px;
  font-size:28px;
  color:var(--yellow);
  cursor:pointer;
}

/* Product Modal */
#productModal{
  position:fixed;
  top:0;left:0;width:100%;height:100%;
  background:rgba(0,0,0,0.8);
  z-index:3000;
  display:flex;
  align-items:center;
  justify-content:center;
}
#productModal .modalContent{
  width:95%;
  max-width:1100px;
  background:#fff;
  border-radius:15px;
  overflow:hidden;
  direction:rtl;
}
#productModal .modalHeader{
  background:var(--black);
  color:var(--yellow);
  padding:12px 15px;
  display:flex;
  justify-content:space-between;
  align-items:center;
}
#productModal .modalHeader button{
  background:var(--yellow);
  color:#000;
  border:none;
  border-radius:10px;
  padding:10px 14px;
}
#productModal .modalBody{padding:18px}
.product-page{
  display:grid;
  grid-template-columns:1.3fr .7fr;
  gap:20px;
  align-items:start;
}
.product-images{
  background:#fff;
  border-radius:15px;
  padding:15px;
  box-shadow:0 5px 15px rgba(0,0,0,.15);
}
.main-img{
  width:100%;
  height:420px;
  border-radius:12px;
  object-fit:cover;
}
.thumbs{
  margin-top:10px;
  display:flex;
  gap:10px;
  overflow-x:auto;
}
.thumbs img{
  width:120px;
  height:80px;
  border-radius:10px;
  object-fit:cover;
  cursor:pointer;
  border:2px solid transparent;
}
.thumbs img.active{border-color:var(--yellow)}
.product-details{
  background:#fff;
  border-radius:15px;
  padding:20px;
  box-shadow:0 5px 15px rgba(0,0,0,.15);
}
.product-title{font-size:24px;font-weight:900;margin:0 0 10px 0}
.product-price{font-size:24px;color:#ff6600;font-weight:900;margin:10px 0}
.product-desc{font-size:14px;line-height:1.6;color:#555;margin-top:10px}
.btns{display:flex;gap:10px;margin-top:15px}
.btn{flex:1;padding:14px 20px;border:none;border-radius:12px;cursor:pointer;font-size:16px;font-weight:700;transition:transform .2s ease, box-shadow .2s ease;box-shadow:0 6px 15px rgba(0,0,0,.2)}
.btn.cart{background:var(--yellow);color:#000}
.btn.whatsapp{background:#25D366;color:#fff}
.btn:hover{transform:translateY(-2px);box-shadow:0 10px 20px rgba(0,0,0,.25)}
.specs{margin-top:20px;border-top:1px solid #eee;padding-top:15px}
.specs h3{margin:0 0 10px;font-size:18px}
.specs ul{list-style:none;padding:0;margin:0}
.specs ul li{padding:8px 0;border-bottom:1px dashed #ddd;color:#555}

/* Warranty */
.warranty{
  display:none;
  margin-top:15px;
  border:2px solid var(--yellow);
  background:#fff;
  color:#000;
  border-radius:12px;
  padding:12px 14px;
}
.warranty h3{
  margin:0 0 8px 0;
  font-size:18px;
  color:#ff6600;
}
.warranty ul{
  margin:0;
  padding-left:18px;
}
.warranty ul li{
  margin:6px 0;
}
.warranty p{
  margin:6px 0;
  font-size:14px;
}

/* Admin Bar */
.adminBar{
  margin-top:15px;
  background:#000;
  color:var(--yellow);
  padding:10px;
  border-radius:10px;
  display:none;
}
.adminBar input, .adminBar textarea, .adminBar select{
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

/* Search results box for copying */
#copyResults{
  max-height:150px;
  overflow:auto;
  border:1px solid #ddd;
  padding:10px;
  border-radius:10px;
  background:#111;
}
#copyResults div{
  padding:8px;
  border-bottom:1px solid #333;
  cursor:pointer;
  color:#fff;
}
#copyResults div.selected{
  background:#ffd700;
  color:#000;
}

/* Categories Modal */
.categoryModal{
  position:fixed;
  top:0; left:0;
  width:100%; height:100%;
  background:rgba(0,0,0,0.85);
  z-index:2500;
  display:flex;
  justify-content:center;
  align-items:center;
}
.categoryModalContent{
  width:95%;
  max-width:700px;
  background:#000;
  border:2px solid var(--yellow);
  border-radius:20px;
  padding:20px;
  color:#fff;
  position:relative;
}
.categoryModalContent h2{
  text-align:center;
  margin:0 0 15px 0;
}
.closeCategory{
  position:absolute;
  top:15px;
  left:15px;
  background:var(--yellow);
  color:#000;
  border:none;
  padding:10px 12px;
  border-radius:10px;
  font-weight:700;
  cursor:pointer;
}
.categoryGrid{
  display:grid;
  grid-template-columns:repeat(2,1fr);
  gap:15px;
}
.categoryCard{
  background:rgba(255,255,255,0.05);
  border-radius:12px;
  border:1px solid #333;
  padding:12px 10px;
  text-align:center;
  cursor:pointer;
}
.categoryCard img{
  width:100%;
  height:110px;
  object-fit:contain;
  margin-bottom:8px;
}
.categoryCard .ar{
  font-size:14px;
  font-weight:bold;
  color:var(--yellow);
}
.categoryCard .en{
  font-size:13px;
  color:#fff;
  direction:ltr;
}
#editCatBtn{
  display:none;
  margin-bottom:15px;
  background:var(--yellow);
  color:#000;
  border:none;
  padding:10px 12px;
  border-radius:10px;
  font-weight:700;
  cursor:pointer;
}
.editPanel{
  display:none;
  margin-top:15px;
  background:rgba(255,255,255,0.05);
  padding:15px;
  border-radius:12px;
  border:1px solid #333;
}
.editPanel input{
  width:100%;
  padding:10px;
  margin:8px 0;
  border-radius:10px;
  border:1px solid #333;
  background:rgba(0,0,0,0.3);
  color:#fff;
}
.editPanel button{
  padding:10px 12px;
  border:none;
  border-radius:10px;
  font-weight:700;
  cursor:pointer;
  margin-top:10px;
}
</style>
</head>

<body>

<header>
  <h2>Chevrolet Site</h2>
  <div class="btns">
    <button onclick="openCategories()">التصنيفات</button>
    <button id="wazeBtn" onclick="openAddress()">عنواننا</button>
    <button id="adminBtn" onclick="showLogin()" style="display:none">Admin</button>
  </div>
</header>

<div class="banner-cars">
  <img src="https://cdn.salla.sa/mQpGy/dd06a5fb-2e9b-4f97-87be-c76dfdf02190-1000x1000-UiKRN84uJnxNI4O2A0mcIHD5lIcoIvmywG7AJ7vx.jpg" class="active">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSJn8zvfImPaKGVK4ZJIrrIPTdLMjMfIEpf1GQMGQiJpI6J_JAlhapRTwc6&s=10">
</div>

<div class="container">
  <div class="searchBar">
    <input id="searchInput" placeholder="اكتب اسم القطعة" onkeyup="searchProducts()">
    <select id="carSelect" onchange="filterByCar()">
      <option value="">كل السيارات</option>
    </select>
    <button id="searchBtn" onclick="toggleSearch()">🔍 بحث</button>
    <button id="catBtn" onclick="openCategories()">التصنيفات</button>
  </div>

  <div id="backHome">
    <button onclick="backToHome()">العودة للصفحة الرئيسية</button>
  </div>

  <div class="product-grid" id="products"></div>
</div>

<!-- Cart Modal -->
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

<!-- Order Modal -->
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

<!-- Login Modal -->
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

<!-- Product Modal -->
<div id="productModal">
  <div class="modalContent">
    <div class="modalHeader">
      <span>تفاصيل المنتج</span>
      <button onclick="closeProduct()">إغلاق</button>
    </div>
    <div class="modalBody">
      <div class="product-page">
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

          <div class="specs">
            <h3>المواصفات</h3>
            <ul id="specList"></ul>
          </div>

          <div id="productDetailsBox" style="display:none; margin-top:15px; border-top:1px solid #ddd; padding-top:15px;">
            <h3>تفصيل المنتج</h3>
            <p id="productDetailsText" style="color:#555;"></p>
          </div>

          <div id="warrantyBox" class="warranty"></div>

          <!-- Admin Bar -->
          <div id="adminBar" class="adminBar">
            <h3>لوحة تعديل Admin</h3>
            <label>عنوان المنتج:</label>
            <input id="editTitle" type="text">
            <label>السعر:</label>
            <input id="editPrice" type="text">
            <label>الوصف:</label>
            <textarea id="editDesc" rows="3"></textarea>

            <!-- ✨ هنا تم تغيير النسخ إلى بحث + نتائج -->
            <label>نسخ الوصف لمنتجات أخرى:</label>
            <input id="copySearch" placeholder="اكتب اسم القطعة للنسخ" onkeyup="searchCopyProducts()">
            <div id="copyResults"></div>
            <button onclick="copyDescriptionToOthers()">تطبيق نفس الوصف</button>

            <label>رابط الصورة الرئيسية:</label>
            <input id="editImg1" type="text">
            <label>رابط الصورة الثانية:</label>
            <input id="editImg2" type="text">
            <label>رابط الصورة الثالثة:</label>
            <input id="editImg3" type="text">

            <label>المواصفة 1:</label>
            <input id="editSpec1" type="text">
            <label>المواصفة 2:</label>
            <input id="editSpec2" type="text">
            <label>المواصفة 3:</label>
            <input id="editSpec3" type="text">
            <label>المواصفة 4:</label>
            <input id="editSpec4" type="text">

            <label>تفصيل المنتج:</label>
            <textarea id="editDetails" rows="4" placeholder="اكتب تفصيل المنتج هنا..."></textarea>

            <button onclick="saveAdmin()">حفظ التعديلات</button>
          </div>

        </div>
      </div>
    </div>
  </div>
</div>

<!-- Categories Modal -->
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

      <hr style="border:1px solid #333; margin:15px 0;">

      <h3>تعديل / حذف تصنيف</h3>
      <input id="editCatIndex" placeholder="رقم التصنيف">
      <input id="editCatAr" placeholder="اسم جديد بالعربي">
      <input id="editCatEn" placeholder="اسم جديد بالانجليزي">
      <input id="editCatImg" placeholder="رابط صورة جديد">
      <button onclick="editCategory()">تعديل</button>
      <button onclick="deleteCategory()" style="background:#ff3b3b; color:#fff;">حذف</button>
    </div>

    <div class="categoryGrid" id="categoryGrid"></div>
  </div>
</div>

<script>
let products=[], cart=[];
let selectedProductIndex = null;

// ====== Admin ======
const adminUser = "lilkadi1";
const adminPass = "19961996lilkadi";

function isAdmin(){
  return localStorage.getItem("isAdmin") === "true";
}

function showLogin(){
  document.getElementById("loginModal").style.display = "block";
}

function closeLogin(){
  document.getElementById("loginModal").style.display = "none";
}

function login(){
  const user = document.getElementById("username").value;
  const pass = document.getElementById("password").value;

  if(user === adminUser && pass === adminPass){
    localStorage.setItem("isAdmin", "true");
    document.getElementById("loginModal").style.display = "none";
    alert("تم تسجيل الدخول بنجاح");
    checkAdminButton();
  } else {
    alert("اسم المستخدم أو كلمة المرور خطأ");
  }
}

function checkAdminButton(){
  if(isAdmin()){
    document.getElementById("adminBtn").style.display = "none";
  } else {
    document.getElementById("adminBtn").style.display = "block";
  }
}

// ====== Banner ======
const bannerImages=document.querySelectorAll(".banner-cars img");
let current=0;
setInterval(()=>{
  bannerImages.forEach(img=>img.classList.remove("active"));
  current=(current+1)%bannerImages.length;
  bannerImages[current].classList.add("active");
},3000);

// ====== Products ======
const list=document.getElementById("products");
const carSelect=document.getElementById("carSelect");

const apiURL = "https://api.sheetbest.com/sheets/044c3d5a-80e6-42eb-87cc-488eba7900aa";

fetch(apiURL)
  .then(res => res.json())
  .then(data => {
    const cars = [...new Set(data.map(x => (x['السيارة'] || x['car'] || "").trim()).filter(x => x))];
    cars.forEach(c=>{
      const opt = document.createElement("option");
      opt.value = c;
      opt.textContent = c;
      carSelect.appendChild(opt);
    });

    products = data.map((item, index) => ({
      id: index + 1,
      car: item['السيارة'] || item['car'] || "غير محدد",
      name: item['اسم المادة'] || item['name'] || "بدون اسم",
      price: parseFloat(item['البيع'] || item['price'] || 0),
      desc: (item['الوصف'] || "لا يوجد وصف"),
      imgs: [
        item['صورة1'] || "https://cdn.salla.sa/mQpGy/dd06a5fb-2e9b-4f97-87be-c76dfdf02190-1000x1000-UiKRN84uJnxNI4O2A0mcIHD5lIcoIvmywG7AJ7vx.jpg",
        item['صورة2'] || item['صورة1'] || "https://cdn.salla.sa/mQpGy/dd06a5fb-2e9b-4f97-87be-c76dfdf02190-1000x1000-UiKRN84uJnxNI4O2A0mcIHD5lIcoIvmywG7AJ7vx.jpg",
        item['صورة3'] || item['صورة1'] || "https://cdn.salla.sa/mQpGy/dd06a5fb-2e9b-4f97-87be-c76dfdf02190-1000x1000-UiKRN84uJnxNI4O2A0mcIHD5lIcoIvmywG7AJ7vx.jpg"
      ],
      specs: [
        item['مواصفة1'] || "",
        item['مواصفة2'] || "",
        item['مواصفة3'] || "",
        item['مواصفة4'] || ""
      ],
      details: item['تفصيل المنتج'] || "",
      qty: 1,
      category: item['التصنيف'] || "غير مصنف"
    }));

    renderProducts();
    checkAdminButton();
  })
  .catch(err => console.error(err));

function renderProducts(filteredProducts){
    const data = filteredProducts || products;
    list.innerHTML = "";
    data.forEach((prod)=>{
        const div = document.createElement("div");
        div.className = "product";
        div.onclick = ()=> openProduct(prod.id);

        div.innerHTML = `
            <h4>${prod.name}</h4>
            <img src="${prod.imgs[0]}" alt="Product Image">
            <div class="price">${prod.price} $</div>
            <div class="qty">
                <button class="dec" onclick="event.stopPropagation();changeQty(${prod.id},-1)">-</button>
                <span id="qty${prod.id}">${prod.qty}</span>
                <button class="inc" onclick="event.stopPropagation();changeQty(${prod.id},1)">+</button>
            </div>
            <a href="#" class="whatsappBtnProduct" onclick="event.stopPropagation();addToCart(${prod.id})">أضف للطلب</a>
        `;
        list.appendChild(div);
    });
}

function searchProducts(){
    const term = document.getElementById("searchInput").value.toLowerCase();
    const car = carSelect.value;
    const filtered = products.filter(p=>{
        return p.name.toLowerCase().includes(term) && (car ? p.car === car : true);
    });
    renderProducts(filtered);
}

function filterByCar(){
    searchProducts();
}

function changeQty(id, val){
    const prod = products.find(p=>p.id === id);
    prod.qty += val;
    if(prod.qty < 1) prod.qty = 1;
    document.getElementById(`qty${id}`).innerText = prod.qty;
}

function addToCart(id){
    const prod = products.find(p=>p.id === id);
    const existing = cart.find(c => c.id === prod.id);

    if(existing){
      existing.qty += prod.qty;
    } else {
      cart.push({...prod});
    }
    updateCart();
}

function updateCart(){
    const cartItems = document.getElementById("cartItems");
    cartItems.innerHTML = "";
    let total = 0;

    cart.forEach(item=>{
        const div = document.createElement("div");
        div.className = "cartItem";
        div.innerHTML = `
          <img src="${item.imgs[0]}">
          <div class="info">
            <h4>${item.name}</h4>
            <p>${item.price} $ لكل وحدة</p>
            <div class="qtyControl">
              <button class="dec" onclick="changeCartQty(${item.id},-1)">-</button>
              <span>${item.qty}</span>
              <button class="inc" onclick="changeCartQty(${item.id},1)">+</button>
            </div>
          </div>
          <button class="removeBtn" onclick="removeCart(${item.id})">حذف</button>
        `;
        cartItems.appendChild(div);
        total += item.price*item.qty;
    });

    document.getElementById("cartTotal").innerText = total;
    document.getElementById("cartCount").innerText = cart.reduce((a,b)=>a+b.qty,0);
}

function changeCartQty(id, val){
    const item = cart.find(c => c.id === id);
    item.qty += val;
    if(item.qty < 1) item.qty = 1;
    updateCart();
}

function removeCart(id){
    cart = cart.filter(c=>c.id!==id);
    updateCart();
}

function toggleCart(){
    const modal = document.getElementById("cartModal");
    modal.style.display = modal.style.display==="flex"?"none":"flex";
    if(modal.style.display === "flex") updateCart();
}

function showOrderBox(){
  document.getElementById("cartModal").style.display = "none";
  document.getElementById("orderModal").style.display = "flex";
}

function closeOrderModal(){
  document.getElementById("orderModal").style.display = "none";
}

function sendOrder(){
    const name = document.getElementById("custName").value;
    const phone = document.getElementById("custPhone").value;
    const address = document.getElementById("custAddress").value;
    if(!name || !phone || !address){ alert("ادخل الاسم، رقم الهاتف، والعنوان"); return; }

    let msg = `طلبية جديدة:\nالزبون: ${name}\nرقم الهاتف: ${phone}\nالعنوان: ${address}\n\nالقطع:\n`;
    let total = 0;
    cart.forEach(item=>{
        const itemTotal = item.price * item.qty;
        msg += `${item.name} - ${item.qty} × ${item.price} = ${itemTotal} $\n`;
        total += itemTotal;
    });
    msg += `\nالمجموع: ${total}$`;
    window.open(`https://wa.me/9647872159504?text=${encodeURIComponent(msg)}`);
}

// Product Modal
function openProduct(id){
  const idx = products.findIndex(p=>p.id === id);
  selectedProductIndex = idx;
  const p = products[idx];

  document.getElementById("mainImg").src = p.imgs[0];
  document.getElementById("prodTitle").innerText = p.name;
  document.getElementById("prodPrice").innerText = p.price + " $";
  document.getElementById("prodDesc").innerText = p.desc; // <--- الوصف الحالي

  document.getElementById("thumb1").src = p.imgs[0];
  document.getElementById("thumb2").src = p.imgs[1];
  document.getElementById("thumb3").src = p.imgs[2];

  const specList = document.getElementById("specList");
  specList.innerHTML = "";
  p.specs.forEach(spec => {
    if(spec && spec.trim() !== ""){
      const li = document.createElement("li");
      li.textContent = spec;
      specList.appendChild(li);
    }
  });

  const detailsBox = document.getElementById("productDetailsBox");
  const detailsText = document.getElementById("productDetailsText");
  if(p.details && p.details.trim() !== ""){
    detailsBox.style.display = "block";
    detailsText.innerText = p.details;
  } else {
    detailsBox.style.display = "none";
  }

  // Admin Bar
  document.getElementById("editTitle").value = p.name;
  document.getElementById("editPrice").value = p.price;
  document.getElementById("editDesc").value = p.desc;
  document.getElementById("editImg1").value = p.imgs[0];
  document.getElementById("editImg2").value = p.imgs[1];
  document.getElementById("editImg3").value = p.imgs[2];
  document.getElementById("editSpec1").value = p.specs[0];
  document.getElementById("editSpec2").value = p.specs[1];
  document.getElementById("editSpec3").value = p.specs[2];
  document.getElementById("editSpec4").value = p.specs[3];
  document.getElementById("editDetails").value = p.details;

  document.getElementById("productModal").style.display = "flex";
  showAdminBar();

  // تنظيف بحث النسخ عند فتح المنتج
  document.getElementById("copySearch").value = "";
  document.getElementById("copyResults").innerHTML = "";
  copySelected = [];
}

function closeProduct(){
  document.getElementById("productModal").style.display = "none";
}

function changeImg(el){
  document.getElementById("mainImg").src = el.src;
  document.querySelectorAll(".thumbs img").forEach(i=>i.classList.remove("active"));
  el.classList.add("active");
}

function addToCartFromModal(){
  const p = products[selectedProductIndex];
  const existing = cart.find(c => c.id === p.id);
  if(existing) existing.qty += p.qty;
  else cart.push({...p});
  updateCart();
  alert("تم إضافة المنتج للسلة ✅");
}

function sendWhatsApp(){
  const msg = "أريد أطلب هذا المنتج: " + document.getElementById("prodTitle").innerText;
  window.open(`https://wa.me/9647872159504?text=${encodeURIComponent(msg)}`);
}

function showAdminBar(){
  if(isAdmin()){
    document.getElementById("adminBar").style.display = "block";
  } else {
    document.getElementById("adminBar").style.display = "none";
  }
}

function saveAdmin(){
  if(selectedProductIndex === null) return;

  const p = products[selectedProductIndex];

  p.name  = document.getElementById("editTitle").value;
  p.price = parseFloat(document.getElementById("editPrice").value) || 0;

  // ✅ حذف الوصف القديم نهائياً إذا تركته فارغ
  p.desc  = document.getElementById("editDesc").value.trim();

  p.imgs[0] = document.getElementById("editImg1").value;
  p.imgs[1] = document.getElementById("editImg2").value;
  p.imgs[2] = document.getElementById("editImg3").value;

  p.specs[0] = document.getElementById("editSpec1").value;
  p.specs[1] = document.getElementById("editSpec2").value;
  p.specs[2] = document.getElementById("editSpec3").value;
  p.specs[3] = document.getElementById("editSpec4").value;

  p.details = document.getElementById("editDetails").value;

  renderProducts();
  openProduct(p.id);
  alert("تم حفظ التعديلات ✅");
}

/* =========================
   ✨ النسخ عبر البحث
   ========================= */
let copySelected = [];

function searchCopyProducts(){
  const term = document.getElementById("copySearch").value.toLowerCase();
  const results = products.filter(p => p.name.toLowerCase().includes(term));

  const box = document.getElementById("copyResults");
  box.innerHTML = "";

  results.forEach(p => {
    const div = document.createElement("div");
    div.textContent = p.name;
    div.onclick = () => toggleCopySelect(p.id, div);

    if(copySelected.includes(p.id)){
      div.classList.add("selected");
    }
    box.appendChild(div);
  });

  if(results.length === 0){
    box.innerHTML = "<div style='color:#aaa;'>لا توجد نتائج</div>";
  }
}

function toggleCopySelect(id, el){
  const idx = copySelected.indexOf(id);
  if(idx === -1){
    copySelected.push(id);
    el.classList.add("selected");
  } else {
    copySelected.splice(idx, 1);
    el.classList.remove("selected");
  }
}

function copyDescriptionToOthers(){
  if(copySelected.length === 0){
    alert("اختر منتج واحد على الأقل للنسخ");
    return;
  }

  const desc = document.getElementById("editDesc").value.trim(); // <--- نفس الوصف الجديد

  copySelected.forEach(id => {
    const prod = products.find(p => p.id === id);
    if(prod){
      prod.desc = desc; // ✅ يستبدل الوصف القديم بالكامل
    }
  });

  renderProducts();
  alert("تم تطبيق نفس الوصف على المنتجات المحددة ✅");
}

/* =========================
   التصنيفات
   ========================= */
let categories = [
  {ar:"التصميم الداخلي", en:"Interior Design", img:"https://cdn-icons-png.flaticon.com/512/3062/3062634.png"},
  {ar:"مساحات الزجاج", en:"Windshield Wipers", img:"https://cdn-icons-png.flaticon.com/512/1309/1309522.png"},
  {ar:"الزيوت والسوائل", en:"Oils & Fluids", img:"https://cdn-icons-png.flaticon.com/512/2913/2913894.png"},
  {ar:"الفلاتر", en:"Filters", img:"https://cdn-icons-png.flaticon.com/512/1605/1605750.png"},
  {ar:"المكابح", en:"Brakes", img:"https://cdn-icons-png.flaticon.com/512/3059/3059814.png"},
  {ar:"المحرك", en:"Engine", img:"https://cdn-icons-png.flaticon.com/512/919/919846.png"},
  {ar:"الكهرباء", en:"Electrical", img:"https://cdn-icons-png.flaticon.com/512/149/149060.png"},
  {ar:"الإطارات", en:"Tires", img:"https://cdn-icons-png.flaticon.com/512/2976/2976216.png"}
];

function saveCategories(){
  localStorage.setItem("categories", JSON.stringify(categories));
}

function loadCategories(){
  const saved = localStorage.getItem("categories");
  if(saved){
    categories = JSON.parse(saved);
  }
}
loadCategories();

function renderCategories(){
  const grid = document.getElementById("categoryGrid");
  grid.innerHTML = "";
  categories.forEach((c, idx)=>{
    grid.innerHTML += `
      <div class="categoryCard" onclick="filterByCategory('${c.ar}')">
        <img src="${c.img}">
        <div class="ar">${c.ar}</div>
        <div class="en">${c.en}</div>
        <div style="font-size:12px;color:#fff;margin-top:5px;">رقم: ${idx+1}</div>
      </div>
    `;
  });
}

function openCategories(){
  document.getElementById("categoryModal").style.display = "flex";
  renderCategories();
  checkEditButton();
}

function closeCategories(){
  document.getElementById("categoryModal").style.display = "none";
}

function checkEditButton(){
  if(isAdmin()){
    document.getElementById("editCatBtn").style.display = "block";
  } else {
    document.getElementById("editCatBtn").style.display = "none";
    document.getElementById("editPanel").style.display = "none";
  }
}

function toggleEditPanel(){
  if(!isAdmin()){
    alert("فقط Admin يقدر يعدل");
    return;
  }
  const panel = document.getElementById("editPanel");
  panel.style.display = panel.style.display === "block" ? "none" : "block";
}

function addCategory(){
  if(!isAdmin()){ alert("فقط Admin يقدر يضيف"); return; }

  const ar = document.getElementById("newCatAr").value;
  const en = document.getElementById("newCatEn").value;
  const img = document.getElementById("newCatImg").value;

  if(!ar || !en || !img){
    alert("اكمل جميع الحقول");
    return;
  }

  categories.push({ar,en,img});
  saveCategories();
  renderCategories();
  alert("تم إضافة التصنيف");
}

function editCategory(){
  if(!isAdmin()){ alert("فقط Admin يقدر يعدل"); return; }

  const idx = parseInt(document.getElementById("editCatIndex").value) - 1;
  if(idx < 0 || idx >= categories.length){
    alert("رقم التصنيف غير صحيح");
    return;
  }

  const ar = document.getElementById("editCatAr").value;
  const en = document.getElementById("editCatEn").value;
  const img = document.getElementById("editCatImg").value;

  if(ar) categories[idx].ar = ar;
  if(en) categories[idx].en = en;
  if(img) categories[idx].img = img;

  saveCategories();
  renderCategories();
  alert("تم تعديل التصنيف");
}

function deleteCategory(){
  if(!isAdmin()){ alert("فقط Admin يقدر يحذف"); return; }

  const idx = parseInt(document.getElementById("editCatIndex").value) - 1;
  if(idx < 0 || idx >= categories.length){
    alert("رقم التصنيف غير صحيح");
    return;
  }

  categories.splice(idx, 1);
  saveCategories();
  renderCategories();
  alert("تم حذف التصنيف");
}

// تصفية حسب التصنيف
function filterByCategory(cat){
  const filtered = products.filter(p=>p.category === cat);
  renderProducts(filtered);
  closeCategories();
  document.getElementById("backHome").style.display = "block";
}

// العودة للرئيسية
function backToHome(){
  renderProducts();
  document.getElementById("backHome").style.display = "none";
}

// ====== Search ======
function toggleSearch(){ 
  const input = document.getElementById("searchInput");
  input.focus();
}

// ====== Waze ======
function openAddress(){
  window.open("https://waze.com/ul/hsyrq48m2z", "_blank");
}

/* ====== Admin Secret Link ====== */
const ADMIN_SECRET = "chevy1996";
(function checkAdminSecret(){
  const params = new URLSearchParams(window.location.search);
  if(params.get("admin") === ADMIN_SECRET){
    document.getElementById("adminBtn").style.display = "block";
  }
})();

// عند تحميل الصفحة نخلي كل النوافذ مخفية
window.onload = function() {
  document.getElementById("cartModal").style.display = "none";
  document.getElementById("orderModal").style.display = "none";
  document.getElementById("productModal").style.display = "none";
  document.getElementById("categoryModal").style.display = "none";
  document.getElementById("loginModal").style.display = "none";
};
</script>

</body>
</html>
