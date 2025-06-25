# day3
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Dog API Viewer 🐶</title>
  <style>
    body {
  font-family: Arial, sans-serif;
  background-color: #f9f9f9;
  text-align: center;
  margin: 0;
  padding: 20px;
}

.container {
  max-width: 800px;
  margin: auto;
}

input {
  padding: 10px;
  width: 60%;
  margin: 10px 5px;
  font-size: 16px;
}

button {
  padding: 10px 16px;
  margin: 5px;
  font-size: 16px;
  cursor: pointer;
  background-color: #ff9800;
  color: white;
  border: none;
  border-radius: 5px;
}

button:hover {
  background-color: #e68900;
}

.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 15px;
  margin-top: 20px;
}

.gallery img {
  width: 100%;
  height: auto;
  border-radius: 10px;
  border: 2px solid #ddd;
}
  </style>
</head>
<body>

  <div class="container">
    <h1>🐾 Dog Gallery</h1>

    <input type="text" id="breedInput" placeholder="Search breed (e.g., husky)" />
    <button onclick="fetchByBreed()">Search</button>
    <button onclick="fetchDogs()">Load Random Dogs</button>

    <div id="dogContainer" class="gallery"></div>
  </div>

  <script>
    const container = document.getElementById("dogContainer");
const breedInput = document.getElementById("breedInput");

function fetchDogs() {
  fetch("https://dog.ceo/api/breeds/image/random/5")
    .then(res => res.json())
    .then(data => {
      showDogs(data.message);
    });
}

function fetchByBreed() {
  const breed = breedInput.value.trim().toLowerCase();
  if (!breed) return;

  fetch(`https://dog.ceo/api/breed/${breed}/images/random/5`)
    .then(res => res.json())
    .then(data => {
      if (data.status === "success") {
        showDogs(data.message);
      } else {
        container.innerHTML = `<p>No images found for "${breed}"</p>`;
      }
    });
}

function showDogs(images) {
  container.innerHTML = "";
  images.forEach(url => {
    const img = document.createElement("img");
    img.src = url;
    container.appendChild(img);
  });
}


fetchDogs();
  </script>
</body>
</html>
