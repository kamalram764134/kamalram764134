<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>WebP to JPEG Converter</title>
</head>
<body>

  <input type="file" id="imageInput" accept="image/*">
  <button onclick="convertToJPEG()">Convert to JPEG</button>

  <br>

  <canvas id="outputCanvas" style="max-width: 100%;"></canvas>

  <script>
    function convertToJPEG() {
      const input = document.getElementById('imageInput');
      const canvas = document.getElementById('outputCanvas');
      const context = canvas.getContext('2d');

      const file = input.files[0];

      if (file) {
        const reader = new FileReader();

        reader.onload = function (e) {
          const img = new Image();
          img.src = e.target.result;

          img.onload = function () {
            canvas.width = img.width;
            canvas.height = img.height;
            context.drawImage(img, 0, 0);

            // Convert to JPEG
            const imageData = canvas.toDataURL('image/jpeg');
            const downloadLink = document.createElement('a');
            downloadLink.href = imageData;
            downloadLink.download = 'converted_image.jpg';
            downloadLink.click();
          };
        };

        reader.readAsDataURL(file);
      }
    }
  </script>

</body>
</html>
