<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Farmers Direct Market</title>
<style>
body {
    font-family: Arial;
    margin: 0;
    background: #f4f4f4;
}
header {
    background: green;
    color: white;
    padding: 15px;
    text-align: center;
}
.container {
    padding: 20px;
}
button {
    padding: 8px 12px;
    margin: 5px;
    cursor: pointer;
}
.card {
    background: white;
    padding: 10px;
    margin: 10px 0;
    border-radius: 5px;
}
input {
    padding: 5px;
    margin: 5px;
}
.hidden {
    display: none;
}
</style>
</head>

<body>

<header>
    <h2>🌾 Direct Market Access for Farmers</h2>
</header>

<div class="container">

    <!-- Role Selection -->
    <h3>Select Dashboard</h3>
    <button onclick="showFarmer()">Farmer Dashboard</button>
    <button onclick="showBuyer()">Buyer Dashboard</button>

    <!-- Farmer Dashboard -->
    <div id="farmer" class="hidden">
        <h3>👨‍🌾 Farmer Dashboard</h3>

        <input type="text" id="pname" placeholder="Product Name">
        <input type="number" id="pprice" placeholder="Price (₹)">
        <button onclick="addProduct()">Add Product</button>

        <h4>Your Products</h4>
        <div id="farmerProducts"></div>
    </div>

    <!-- Buyer Dashboard -->
    <div id="buyer" class="hidden">
        <h3>🛒 Buyer Dashboard</h3>

        <h4>Available Products</h4>
        <div id="buyerProducts"></div>
    </div>

</div>

<script>
let products = [];

// Show dashboards
function showFarmer() {
    document.getElementById("farmer").classList.remove("hidden");
    document.getElementById("buyer").classList.add("hidden");
    displayFarmerProducts();
}

function showBuyer() {
    document.getElementById("buyer").classList.remove("hidden");
    document.getElementById("farmer").classList.add("hidden");
    displayBuyerProducts();
}

// Add product
function addProduct() {
    let name = document.getElementById("pname").value;
    let price = document.getElementById("pprice").value;

    if(name === "" || price === "") {
        alert("Enter product details");
        return;
    }

    products.push({name, price});
    displayFarmerProducts();

    document.getElementById("pname").value = "";
    document.getElementById("pprice").value = "";
}

// Remove product
function removeProduct(index) {
    products.splice(index, 1);
    displayFarmerProducts();
}

// Display farmer products
function displayFarmerProducts() {
    let list = document.getElementById("farmerProducts");
    list.innerHTML = "";

    products.forEach((p, i) => {
        list.innerHTML += `
            <div class="card">
                ${p.name} - ₹${p.price}
                <button onclick="removeProduct(${i})">Remove</button>
            </div>
        `;
    });
}

// Display buyer products
function displayBuyerProducts() {
    let list = document.getElementById("buyerProducts");
    list.innerHTML = "";

    products.forEach((p, i) => {
        list.innerHTML += `
            <div class="card">
                ${p.name} - ₹${p.price}
                <button onclick="buyProduct(${i})">Buy</button>
            </div>
        `;
    });
}

// Payment simulation
function buyProduct(index) {
    let product = products[index];
    let method = prompt("Choose Payment Method:\n1. UPI\n2. Card\n3. Cash");

    if(method) {
        alert(`Payment Successful for ${product.name} (₹${product.price}) via ${method}`);
    }
}
</script>

</body>
</html>
