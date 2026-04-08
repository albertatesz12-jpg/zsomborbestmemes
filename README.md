<!DOCTYPE html>
<html lang="hu">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>zsomborbestmeme</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #111, #333);
      color: white;
      text-align: center;
    }

    header {
      padding: 40px 20px;
      font-size: 2.5rem;
      font-weight: bold;
      background: #000;
    }

    .upload {
      margin: 20px;
    }

    input, button {
      padding: 10px;
      margin: 5px;
      border-radius: 10px;
      border: none;
    }

    button {
      background: #ff4081;
      color: white;
      cursor: pointer;
    }

    .container {
      padding: 20px;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
    }

    .meme {
      background: #222;
      border-radius: 16px;
      padding: 10px;
    }

    .meme img, .meme video {
      width: 100%;
      max-height: 200px;
      object-fit: contain;
      border-radius: 12px;
    }
  </style>
</head>
<body>

  <header>😂 zsomborbestmeme 😂</header>

  <div class="upload">
    <input type="file" id="fileInput" accept="image/*,video/*">
    <input type="text" id="caption" placeholder="Szöveg">
    <button onclick="addMemeFromInput()">Hozzáadás</button>
    <p>Ctrl+V-vel is beillesztheted és AUTOMATIKUSAN megjelenik 👇</p>
  </div>

  <div class="container" id="memeContainer"></div>

  <script>

    function displayFile(file, text="") {
      const reader = new FileReader();

      reader.onload = function(e) {
        const container = document.getElementById('memeContainer');
        const div = document.createElement('div');
        div.className = 'meme';

        if (file.type.startsWith('image')) {
          div.innerHTML = `<img src="${e.target.result}"><p>${text}</p>`;
        } else if (file.type.startsWith('video')) {
          div.innerHTML = `<video src="${e.target.result}" controls></video><p>${text}</p>`;
        }

        container.prepend(div);
      };

      reader.readAsDataURL(file);
    }

    function addMemeFromInput() {
      const file = document.getElementById('fileInput').files[0];
      const text = document.getElementById('caption').value;

      if (!file) return;

      displayFile(file, text);

      document.getElementById('fileInput').value = '';
      document.getElementById('caption').value = '';
    }

    document.addEventListener('paste', (event) => {
      const items = event.clipboardData.items;

      for (let item of items) {
        if (item.kind === 'file') {
          const file = item.getAsFile();
          if (file) {
            displayFile(file);
          }
        }
      }
    });

  </script>

</body>
</html>
