#### I wanted to save the notes I tool when I just started testing

```javascript
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />

    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>

    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Roboto:wght@500&display=swap"
      rel="stylesheet"
    />
    <!--  -->
    <script
      type="module"
      src="https://unpkg.com/@google/model-viewer/dist/model-viewer.min.js"
    ></script>
    <!--  -->

    <!--  -->
    <style>
      .container {
        margin: 40px 0;
        display: flex;
        flex-direction: column;
        width: 100vw;
        min-height: 40vh;
        padding: 4vh 0;
        /* border: 1px solid #000; */
        text-align: center;
      }

      h1 {
        margin: 40px 0;
        color: black;
        -webkit-text-fill-color: white; /* Will override color (regardless of order) */
        -webkit-text-stroke-width: 0.5px;
        -webkit-text-stroke-color: rgba(0, 0, 0, 0.479);
        font-family: "Roboto", sans-serif;
        letter-spacing: 5px;
        text-transform: uppercase;
      }
      /*


      */

      .wrapper {
        display: flex;

        flex-wrap: nowrap;
        width: 100%;
        height: 100%;
      }

      model-viewer {
        width: 600px;
        height: 600px;

        margin: 3px;
        filter: contrast(100%) brightness(100%);
        /* background: linear-gradient(
            0deg,
            rgb(181, 185, 123),
            rgba(224, 213, 175, 0.493)
          ),
          url(./assets/noise.png);
        border: 10px solid rgba(221, 228, 238, 0.151);*/
        /*  */
        background-image: linear-gradient(to top, #d299c2 0%, #fef9d7 100%);
      }
    </style>

    <!--  -->
  </head>
  <body>
    <!-- <model-viewer
      alt="Neil Armstrong's Spacesuit from the Smithsonian Digitization Programs Office and National Air and Space Museum"
      src="assets/scene.gltf




      ar

Augmented Reality
Attributes
ar

A prioritized list of the types of AR experiences to enable.
Allowed values are "webxr", to launch the AR experience in the browser, "scene-viewer",
to launch the Scene Viewer app, "quick-look", to launch the iOS Quick Look app.
You can specify any number of modes separated by whitespace. Note that the presence
of an ios-src will enable quick-look by itself; specifying quick-look here allows us
to generate a USDZ on the fly rather than downloading a separate ios-src file.

https://modelviewer.dev/examples/augmentedreality/




ar-modes="webxr scene-viewer quick-look"



----------------------

environment-image="shared-assets/environments/moon_1k.hdr"

----------------------


poster="shared-assets/models/NeilArmstrong.webp"

Displays an image instead of the model, useful for showing the
user something before a model is loaded and ready to render.
If you use a poster with transparency, you may also want to set
 --poster-color to transparent so that the background shows through.

      seamless-poster
      shadow-intensity="1"
      camera-controls
    ></model-viewer> -->
    <div class="container">
      <h1>model viewer</h1>

      <!-- <model-viewer
        src="assets/flower_hair-stair.glb"
        shadow-intensity="1"
        camera-controls
        auto-rotate
      ></model-viewer> -->
      <div class="wrapper">
        <model-viewer
          src="assets/carta2-with-modifiers.glb"
          shadow-intensity="1"
          camera-controls
          auto-rotate
          disable-zoom
        ></model-viewer>
        <!-- https://polyhaven.com/a/whipple_creek_regional_park_04
 -->
        <model-viewer
          skybox-image="assets/whipple_creek_regional_park_04_4k.hdr"
          environment-image="assets/studio_garden_4k.hdr"
          src="assets/carta.glb"
          shadow-intensity="1"
          camera-controls
          auto-rotate
        ></model-viewer>
        <!--


shadow-intensity

 -->

        <model-viewer
          alt="A 3D astronaut model depicted within a forest"
          src="assets/flower_hair-stair.glb"
          camera-controls
          auto-rotate
          shadow-intensity="1"
          shadow-softness="1"
        ></model-viewer>
        <!--

        reveal

https://modelviewer.dev/docs/

reveal="interaction"  the model will reveal only
when the user clicks on the selected area


reveal="manual"  nothing happens, but I guess its possible
to add a button and then once clicked the model will appear.

something like this:

https://modelviewer.dev/examples/augmentedreality/#customButton

reveal="auto"

Auto is the same i guess as to have no attribute reveal at all

      -->

        <model-viewer
          src="assets/TradingCard.glb"
          shadow-intensity="1"
          camera-controls
          auto-rotate
          reveal="auto"
        ></model-viewer>

        <!--

      Exposure



  Controls the exposure of both the model and skybox, for use primarily with HDR environments.

  Default Value	Options
  1	or any 'positive' value
       -->

        <model-viewer
          id="exposure-demo"
          skybox-image="assets/whipple_creek_regional_park_04_4k.hdr"
          src="assets/carta.glb"
          shadow-intensity="1"
          exposure="4"
          camera-controls
          auto-rotate
        ></model-viewer>
        <script>
          (() => {
            const modelViewer = document.querySelector("#exposure-demo");
            const time = performance.now();

            const animate = (now) => {
              modelViewer.exposure = oscillate(0, 2, 4000, now - time);
              requestAnimationFrame(animate);
            };

            animate();
          })();
        </script>
      </div>
    </div>

    <!--







animated






https://modelviewer.dev/examples/animation/index.html

Choose the animation inside the characters page:
click on the dropdown and choose whatever you like.

I took: Run,

https://poly.pizza/m/DgOCW9ZCRJ

     -->

    <div class="container">
      <h1>animations</h1>
      <div class="wrapper">
        <model-viewer
          src="assets/Character Animated.glb"
          shadow-intensity="1"
          camera-controls
          disable-zoom
          auto-rotate
          autoplay
          animation-name="Walk"
        ></model-viewer>
        <!-- speed of the animation -->

        <model-viewer
          id="change-speed-demo"
          src="assets/Character Animated.glb"
          shadow-intensity="1"
          disable-zoom
          camera-controls
          auto-rotate
          autoplay
          animation-name="Run"
        ></model-viewer>
        <script>
          (() => {
            const modelViewer = document.querySelector("#change-speed-demo");
            const speeds = [1, 3, 0.5, -1, 0];

            let i = 0;
            self.setInterval(() => {
              modelViewer.timeScale = speeds[i++ % speeds.length];
            }, 3000.0);
          })();
        </script>

        <!--



          crossfade animation




        -->

        <model-viewer
          id="paused-change-demo"
          src="assets/Character Animated.glb"
          shadow-intensity="1"
          disable-zoom
          camera-controls
          auto-rotate
          autoplay
          animation-name="Run"
        ></model-viewer>
        <script>
          (() => {
            const modelViewer = document.querySelector("#paused-change-demo");

            self.setInterval(() => {
              modelViewer.animationName =
                modelViewer.animationName === "Run" ? "PickUp" : "Run";
            }, 1500.0);
          })();
        </script>
      </div>
    </div>
  </body>
</html>

```
