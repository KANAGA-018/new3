# new3
<!DOCTYPE html>
<html>
<head>
<title>Product Recommendation System</title>

<style>

body{
font-family:Arial;
margin:0;
background:#f4f6f9;
}

header{
background:#2563eb;
color:white;
padding:15px;
text-align:center;
font-size:22px;
}

.container{
padding:20px;
}

.page{
display:none;
}

input{
padding:10px;
width:250px;
margin:5px;
border-radius:5px;
border:1px solid #ccc;
}

button{
padding:10px 15px;
border:none;
background:#2563eb;
color:white;
border-radius:5px;
cursor:pointer;
margin:5px;
}

button:hover{
background:#1e40af;
}

.location-buttons button{
background:#16a34a;
}

.products{
display:grid;
grid-template-columns:repeat(auto-fill,minmax(220px,1fr));
gap:20px;
}

.card{
background:white;
padding:15px;
border-radius:8px;
box-shadow:0 2px 8px rgba(0,0,0,0.1);
}

.card img{
width:100%;
height:150px;
object-fit:cover;
border-radius:5px;
}

.links a{
display:block;
margin-top:5px;
color:#2563eb;
text-decoration:none;
}

</style>
</head>

<body>

<header>
Smart Product Recommendation System
</header>

<!-- LOGIN PAGE -->

<div id="loginPage" class="container page" style="display:block">

<h2>Login</h2>

<input id="mobile" placeholder="Enter Mobile Number">

<h3>Select Location</h3>

<div class="location-buttons">

<button onclick="setLocation('Chennai')">Chennai</button>
<button onclick="setLocation('Madurai')">Madurai</button>
<button onclick="setLocation('Trichy')">Trichy</button>
<button onclick="setLocation('Coimbatore')">Coimbatore</button>

</div>

<button onclick="login()">Enter Website</button>

</div>


<!-- MAIN WEBSITE -->

<div id="mainPage" class="container page">

<h3>Welcome <span id="userMobile"></span></h3>

<p>Location: <b id="userLocation"></b></p>

<input id="searchInput" placeholder="Search product">

<button onclick="searchProduct()">Search</button>

<button onclick="openAdmin()">Admin Panel</button>

<h3>Products</h3>

<div class="products" id="productList"></div>

</div>


<!-- ADMIN PANEL -->

<div id="adminPage" class="container page">

<h2>Admin Panel</h2>

<input id="pname" placeholder="Product Name">
<input id="ptype" placeholder="Product Type">
<input id="pimage" placeholder="Image URL">
<input id="pshop" placeholder="Shop Name">

<br>

<button onclick="addProduct()">Add Product</button>

<button onclick="goHome()">Back to Website</button>

</div>


<script>

let selectedLocation="";

let products=[

{
name:"iPhone 14",
type:"mobile",
shop:"Reliance Digital",
image:"https://images.unsplash.com/photo-1598327105666"
},

{
name:"Samsung Galaxy S23",
type:"mobile",
shop:"Poorvika Mobiles",
image:"https://images.unsplash.com/photo-1511707171634"
},

{
name:"LG Washing Machine",
type:"washing",
shop:"Vasanth & Co",
image:"https://images.unsplash.com/photo-1626806787461"
},

{
name:"Wooden Sofa",
type:"furniture",
shop:"IKEA Store",
image:"https://images.unsplash.com/photo-1505693416388"
}

];


function setLocation(city){

selectedLocation=city;

alert("Location selected: "+city);

}


function login(){

let mobile=document.getElementById("mobile").value;

if(mobile.length>=10 && selectedLocation!=""){

document.getElementById("loginPage").style.display="none";

document.getElementById("mainPage").style.display="block";

document.getElementById("userMobile").innerText=mobile;

document.getElementById("userLocation").innerText=selectedLocation;

displayProducts(products);

}

else{

alert("Enter mobile number and select location");

}

}


function searchProduct(){

let query=document.getElementById("searchInput").value.toLowerCase();

let result=products.filter(p=>p.name.toLowerCase().includes(query) || p.type.includes(query));

displayProducts(result);

}


function displayProducts(list){

let html="";

list.forEach(p=>{

html+=`

<div class="card">

<img src="${p.image}">

<h4>${p.name}</h4>

<p><b>Available Shop:</b> ${p.shop}</p>

<div class="links">

<a target="_blank" href="https://www.google.com/maps/search/${p.shop}">Find Shop Location</a>

</div>

</div>

`

});

document.getElementById("productList").innerHTML=html;

}


function openAdmin(){

document.getElementById("mainPage").style.display="none";

document.getElementById("adminPage").style.display="block";

}


function goHome(){

document.getElementById("adminPage").style.display="none";

document.getElementById("mainPage").style.display="block";

}


function addProduct(){

let name=document.getElementById("pname").value;

let type=document.getElementById("ptype").value;

let image=document.getElementById("pimage").value;

let shop=document.getElementById("pshop").value;

products.push({

name:name,
type:type,
image:image,
shop:shop

});

alert("Product Added Successfully");

}

</script>

</body>
</html>
