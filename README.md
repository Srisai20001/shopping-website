# shopping-website
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Shopping Website</title>
<style>
body {
font-family: Arial, sans-serif;
background-color: #f4f4f4;
display: flex;
justify-content: center;
align-items: center;
height: 100vh;
margin: 0;
}
.container {
background-color: lightblue;
padding: 20px;
border-radius: 5px;
box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
width: 90%;
max-width: 400px;
}
h1 {
text-align: center;
color: #333;
}
form {
display: flex;
flex-direction: column;
gap: 10px;
margin-bottom: 20px;
}
form input {
padding: 10px;
border: 1px solid #ccc;
border-radius: 5px;
width: 80%;
}
form button {
padding: 10px 20px;
background-color: #28a745;
color: white;
border: none;
border-radius: 5px;
cursor: pointer;
}
form button:hover {
background-color: #218838;
}
ul {
list-style: none;
padding: 0;
}
ul li {
background-color: #fff;
padding: 10px;
border: 1px solid #ccc;
border-radius: 5px;
display: flex;
justify-content: space-between;
align-items: center;
margin-bottom: 10px;
}
.total {
text-align: right;
font-size: 18px;
font-weight: bold;
}
</style>
</head>
<body>
<div class="container">
<h1>Shopping Cart</h1>
<form id="addItemForm">
<input type="text" id="itemName" placeholder="Item Name" required>
<input type="number" id="itemPrice" placeholder="Item Price" required>
<button type="submit">Add Item</button>
</form>
<ul id="shoppingList"></ul>
<div class="total">
Total: ₹<span id="totalPrice">0.00</span>
</div>
</div>
<script>
document.getElementById('addItemForm').addEventListener('submit', function(e) {
e.preventDefault();
addItem();
});

function addItem() {
const itemName = document.getElementById('itemName').value;
const itemPrice = document.getElementById('itemPrice').value;

const li = document.createElement('li');

const checkbox = document.createElement('input');
checkbox.type = 'checkbox';
checkbox.addEventListener('change', updateTotal);

const span = document.createElement('span');
span.textContent = `${itemName} - ₹${parseFloat(itemPrice).toFixed(2)}`;

const button = document.createElement('button');
button.textContent = 'Delete';
button.addEventListener('click', function() {
li.remove();
updateTotal();
});

li.appendChild(checkbox);
li.appendChild(span);
li.appendChild(button);

document.getElementById('shoppingList').appendChild(li);

document.getElementById('itemName').value = '';
document.getElementById('itemPrice').value = '';
updateTotal();
}

function updateTotal() {
const checkboxes = document.querySelectorAll('#shoppingList input[type="checkbox"]');
let total = 0;
checkboxes.forEach(checkbox => {
if (checkbox.checked) {
const price = parseFloat(checkbox.nextSibling.textContent.split('₹')[1]);
total += price;
}
});
document.getElementById('totalPrice').textContent = total.toFixed(2);
}
</script>
</body>
</html>
