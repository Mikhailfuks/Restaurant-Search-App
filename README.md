<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Restaurant Search App</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Restaurant Search</h1>
        <form id="searchForm">
            <input type="text" id="searchQuery" placeholder="Enter restaurant name or type" required>
            <button type="submit">Search</button>
        </form>
        <div id="results"></div>
        <h2>Favorites</h2>
        <div id="favorites"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>


body {
    font-family: Arial, sans-serif;
    background-color: #f5f5f5;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 600px;
    margin: auto;
    padding: 20px;
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

h1, h2 {
    text-align: center;
}

form {
    display: flex;
    justify-content: center;
}

input {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    width: 70%;
}

button {
    padding: 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

.restaurant-item, .favorite-item {
    background: #f8f9fa;
    margin: 10px 0;
    padding: 10px;
    border-radius: 4px;
}

.restaurant-item button, .favorite-item button {
    background-color: #dc3545;
    border: none;
    padding: 5px;
    border-radius: 4px;
    cursor: pointer;
}

.restaurant-item button:hover, .favorite-item button:hover {
    background-color: #c82333;
}


document.getElementById("searchForm").addEventListener("submit", function(event) {
    event.preventDefault();
    const query = document.getElementById("searchQuery").value;
    searchRestaurants(query);
});

let favorites = [];

function searchRestaurants(query) {
    const mockData = [
        { name: "Pizza Place", type: "Italian", address: "123 Main St", id: 1 },
        { name: "Burger Joint", type: "Fast Food", address: "456 Elm St", id: 2 },
        { name: "Sushi Spot", type: "Japanese", address: "789 Pine St", id: 3 },
        { name: "Taco Haven", type: "Mexican", address: "321 Maple St", id: 4 },
        { name: "Pasta House", type: "Italian", address: "654 Oak St", id: 5 }
    ];

    const results = mockData.filter(restaurant =>
        restaurant.name.toLowerCase().includes(query.toLowerCase()) ||
        restaurant.type.toLowerCase().includes(query.toLowerCase())
    );

    displayResults(results);
}

function displayResults(results) {
    const resultsDiv = document.getElementById("results");
    resultsDiv.innerHTML = "";




    results.forEach(restaurant => {
        const restaurantItem = document.createElement("div");
        restaurantItem.className = "restaurant-item";
        restaurantItem.innerHTML = `
            <h3>${restaurant.name}</h3>
            <p>Type: ${restaurant.type}</p>
            <p>Address: ${restaurant.address}</p>
            <button onclick="addToFavorites(${restaurant.id})">Add to Favorites</button>
        `;
        resultsDiv.appendChild(restaurantItem);
    });
}

function addToFavorites(id) {
    const mockData = [
        { name: "Pizza Place", type: "Italian", address: "123 Main St", id: 1 },
        { name: "Burger Joint", type: "Fast Food", address: "456 Elm St", id: 2 },
        { name: "Sushi Spot", type: "Japanese", address: "789 Pine St", id: 3 },
        { name: "Taco Haven", type: "Mexican", address: "321 Maple St", id: 4 },
        { name: "Pasta House", type: "Italian", address: "654 Oak St", id: 5 }
    ];

    const restaurant = mockData.find(res => res.id === id);
    if (restaurant && !favorites.includes(restaurant)) {
        favorites.push(restaurant);
        displayFavorites();
    }
}

function displayFavorites() {
    const favoritesDiv = document.getElementById("favorites");
    favoritesDiv.innerHTML = "";

    favorites.forEach(favorite => {
        const favoriteItem = document.createElement("div");
        favoriteItem.className = "favorite-item";
        favoriteItem.innerHTML = `
            <h3>${favorite.name}</h3>
            <p>Type: ${favorite.type}</p>
            <p>Address: ${favorite.address}</p>
        `;
        favoritesDiv.appendChild(favoriteItem);
    });
}
