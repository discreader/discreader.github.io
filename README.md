<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DISCREADER</title>
    <!-- The style.css file allows you to change the look of your web pages.
         If you include the next line in all your web pages, they will all share the same look.
         This makes it easier to make new pages for your site. -->
    <link href="/style.css" rel="stylesheet" type="text/css" media="all">
  
  <style>
        body {
            margin: 0;
            overflow: hidden;
            background-color: black;
        }
        #fireCanvas {
            position: fixed;
            bottom: 0px;
            z-index: -999
            
        }
         
        .glowcentered {
          display: flex;
          justify-content: center;
          align-items: center;
          filter: drop-shadow(0px 0px 20px red)
        }   
        
          #john {
          display: flex;
          justify-content: center;
          align-items: center;
          bottom: 0px;
        }   
        
        .otherstuff {
        position: relative;
        transform: translateY(-600px);
        text-align: right;
        
        }
        

    </style>
  
  </head>
  <body>
    
    <div class="glowcentered">
    
    <img src="/spinning-skull.gif">
    <h1><u>THE DISCREADER WEB EXPERIENCE</u></h1>
    <img src="/spinning-skull2.gif">
    
    </div>
    
    <p class="glowcentered" >"Horrors"</p>
    
    <p>Find me here:</p>

<ul>
      <li><a href="https://www.youtube.com/@discreader/">▶YouTube</a></li>
      <li><a href="https://twitter.com/discreader">𓅩Twitter</a></li>
      <li><a href="https://discord.com/users/.discreader">Discord</a></li>
</ul>

<h2>Friends:</h2>
    <p><a href="https://thegrubzone.neocities.org/"><img src="/ruby.jpg"></a></p>
    <p><a href="https://sneb.neocities.org/"><img src="/sebb.png"></a></p>

<div id="john" >

<img src="/Romerohead_sprite.webp"

width="114 ">

</div>


 <div class="otherstuff">
<h2>OTHER PAGES</h2>
<ul>
      <li><a href="https://discreader.neocities.org/thecube">THE CUBE</li>
      <li><a href="https://discreader.neocities.org/art">ART</a></li>
    </ul>
</div>

    
  
  <!-- FIRE STUFF \/ -->
  
  <canvas id="fireCanvas"></canvas>
  
    <script>
        const fireWidth = window.innerWidth;
        const fireHeight = 150;
        const firePixelsArray = new Array(fireWidth * fireHeight).fill(0);
        const fireColorsPalette = [
            {r: 0, g: 0, b: 0},
            {r: 31, g: 7, b: 7},
            {r: 47, g: 15, b: 7},
            {r: 71, g: 15, b: 7},
            {r: 87, g: 23, b: 7},
            {r: 103, g: 31, b: 7},
            {r: 119, g: 31, b: 7},
            {r: 143, g: 39, b: 7},
            {r: 159, g: 47, b: 7},
            {r: 175, g: 63, b: 7},
            {r: 191, g: 71, b: 7},
            {r: 199, g: 71, b: 7},
            {r: 223, g: 79, b: 7},
            {r: 223, g: 87, b: 7},
            {r: 223, g: 87, b: 7},
            {r: 215, g: 95, b: 7},
            {r: 215, g: 95, b: 7},
            {r: 215, g: 103, b: 15},
            {r: 207, g: 111, b: 15},
            {r: 207, g: 119, b: 15},
            {r: 207, g: 127, b: 15},
            {r: 207, g: 135, b: 23},
            {r: 199, g: 135, b: 23},
            {r: 199, g: 143, b: 23},
            {r: 199, g: 151, b: 31},
            {r: 191, g: 159, b: 31},
            {r: 191, g: 159, b: 31},
            {r: 191, g: 167, b: 39},
            {r: 191, g: 167, b: 39},
            {r: 191, g: 175, b: 47},
            {r: 183, g: 175, b: 47},
            {r: 183, g: 183, b: 47},
            {r: 183, g: 183, b: 55},
            {r: 207, g: 207, b: 111},
            {r: 223, g: 223, b: 159},
            {r: 239, g: 239, b: 199},
            {r: 255, g: 255, b: 255}
        ];

        const fireCanvas = document.getElementById('fireCanvas');
        fireCanvas.width = window.innerWidth;
        fireCanvas.height = 150
        const fireContext = fireCanvas.getContext('2d');

        function calculateFirePropagation() {
            for (let column = 0; column < fireWidth; column++) {
                for (let row = 1; row < fireHeight; row++) {
                    const pixelIndex = column + (fireWidth * row);
                    updateFireIntensityPerPixel(pixelIndex);
                }
            }
            renderFire();
        }

        function updateFireIntensityPerPixel(currentPixelIndex) {
            const belowPixelIndex = currentPixelIndex + fireWidth;

            if (belowPixelIndex >= fireWidth * fireHeight) {
                return;
            }

            const decay = Math.floor(Math.random() * 1.4);
            const belowPixelFireIntensity = firePixelsArray[belowPixelIndex];
            const newFireIntensity = belowPixelFireIntensity - decay >= 0 ? belowPixelFireIntensity - decay : 0;

            firePixelsArray[currentPixelIndex - decay] = newFireIntensity;
        }

        function renderFire() {
            const imageData = fireContext.createImageData(fireWidth, fireHeight);
            for (let pixelIndex = 0; pixelIndex < firePixelsArray.length; pixelIndex++) {
                const fireIntensity = firePixelsArray[pixelIndex];
                const color = fireColorsPalette[fireIntensity];
                const pixelDataIndex = pixelIndex * 4;

                imageData.data[pixelDataIndex] = color.r;
                imageData.data[pixelDataIndex + 1] = color.g;
                imageData.data[pixelDataIndex + 2] = color.b;
                imageData.data[pixelDataIndex + 3] = 255; // Alpha channel
            }
            fireContext.putImageData(imageData, 0, 0);
        }

        function createFireSource() {
            for (let column = 0; column < fireWidth; column++) {
                const overflowPixelIndex = fireWidth * fireHeight;
                const pixelIndex = (overflowPixelIndex - fireWidth) + column;
                firePixelsArray[pixelIndex] = 36;
            }
        }

        function start() {
            createFireSource();
            setInterval(calculateFirePropagation, 10);
        }

        start();
    </script>

  </body>
</html>
