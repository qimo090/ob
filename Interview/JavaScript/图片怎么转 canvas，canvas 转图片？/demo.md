```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Canvas & Image</title>
    <style>
      canvas {
        border: 1px solid #000;
      }
    </style>
  </head>
  <body>
    <canvas id="canvas" width="500" height="500"></canvas>

    <button id="imageToCanvas">Image to Canvas</button>
    <button id="canvasToImage">Canvas To Image</button>
    <button id="export">Export</button>

    <script>

      function drawImage() {
        const canvas = document.getElementById("canvas");
        const ctx = canvas.getContext("2d");

        const img = new Image();
        img.src = "https://placehold.co/500x500";
        img.crossOrigin = 'anonymous';
        img.onload = () => {
          ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
        };
      }

      function drawCanvas() {
        const canvas = document.getElementById("canvas");
        const ctx = canvas.getContext("2d");

        const dataURL = canvas.toDataURL("image/png");
        const img = new Image();
        img.src = dataURL;
        document.body.appendChild(img);
      }

      function exportCanvas() {
        const canvas = document.getElementById("canvas");
        const ctx = canvas.getContext("2d");

        const dataURL = canvas.toDataURL("image/png");
        const a = document.createElement("a");
        a.href = dataURL;
        a.download = "canvas-image.png";
        a.click();
      }
    </script>
    <script>
      const imageToCanvas = document.getElementById("imageToCanvas");
      const canvasToImage = document.getElementById("canvasToImage");
      const exportBtn = document.getElementById("export");

      imageToCanvas.addEventListener("click", () => drawImage());

      canvasToImage.addEventListener("click", () => drawCanvas());

      exportBtn.addEventListener("click", () => exportCanvas());
    </script>
  </body>
</html>
```