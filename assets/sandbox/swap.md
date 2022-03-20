<br>

⚠️ I added this in case they decided to modify the official page

<br>
<br>

### [Swap Model Variants](https://modelviewer.dev/examples/scenegraph/)

This demonstrates the use of the glTF materials variants extension which allows multiple materials and textures to be packed with a single geometry in a GLB. Our API exposes these variant names as availableVariants and you can select one using the variantName attribute. This is similar functionality to the lower-level scene-graph API below, but in that case it is up to you to choose the right texture URL, rather than having that information stored in the GLB. Note: setting variantName to null reverts to the initial material.

<br>

---

<br>

#### [Swap textures](https://modelviewer.dev/examples/scenegraph/#swapTextures)

As above, you can change these values in AR, but only in WebXR mode. **iOS Quick Look reflects these texture changes so long as the USDZ is auto-generated.**

[model viewer / swap textures](https://modelviewer.dev/examples/scenegraph/#swapTextures)

<br>

```javascript
<model-viewer id="helmet" camera-controls src="../../shared-assets/models/glTF-Sample-Models/2.0/DamagedHelmet/glTF-Binary/DamagedHelmet.glb" ar ar-modes="webxr scene-viewer quick-look" alt="A 3D model of a helmet">
  <div class="controls">
    <div>
      <p>Diffuse</p>
      <select id="diffuse">
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/DamagedHelmet/glTF/Default_albedo.jpg">Damaged helmet</option>
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/Lantern/glTF/Lantern_baseColor.png">Lantern Pole</option>
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/WaterBottle/glTF/WaterBottle_baseColor.png">Water Bottle</option>
      </select>
    </div>
    <div>
      <p>Metallic-roughness</p>
      <select id="metallicRoughness">
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/DamagedHelmet/glTF/Default_metalRoughness.jpg">Damaged helmet</option>
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/Lantern/glTF/Lantern_roughnessMetallic.png">Lantern Pole</option>
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/WaterBottle/glTF/WaterBottle_occlusionRoughnessMetallic.png">Water Bottle</option>
      </select>
    </div>
    <div>
      <p>Normals</p>
      <select id="normals">
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/DamagedHelmet/glTF/Default_normal.jpg">Damaged helmet</option>
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/Lantern/glTF/Lantern_normal.png">Lantern Pole</option>
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/WaterBottle/glTF/WaterBottle_normal.png">Water Bottle</option>
      </select>
    </div>
    <div>
      <p>Occlusion</p>
      <select id="occlusion">
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/DamagedHelmet/glTF/Default_AO.jpg">Damaged helmet</option>
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/WaterBottle/glTF/WaterBottle_occlusionRoughnessMetallic.png">Water Bottle</option>
      </select>
    </div>
    <div>
      <p>Emission</p>
      <select id="emission">
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/DamagedHelmet/glTF/Default_emissive.jpg">Damaged helmet</option>
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/Lantern/glTF/Lantern_emissive.png">Lantern Pole</option>
        <option value="../../shared-assets/models/glTF-Sample-Models/2.0/WaterBottle/glTF/WaterBottle_emissive.png">Water Bottle</option>
      </select>
    </div>
  </div>
</model-viewer>
<script type="module">
const modelViewerTexture = document.querySelector("model-viewer#helmet");

modelViewerTexture.addEventListener("load", () => {

  const material = modelViewerTexture.model.materials[0];

  const createAndApplyTexture = async (channel, event) => {
    const texture = await modelViewerTexture.createTexture(event.target.value);
    if (channel.includes('base') || channel.includes('metallic')) {
      material.pbrMetallicRoughness[channel].setTexture(texture);
    } else {
      material[channel].setTexture(texture);
    }
  }

  document.querySelector('#normals').addEventListener('input', (event) => {
    createAndApplyTexture('normalTexture', event);
  });

  document.querySelector('#occlusion').addEventListener('input', (event) => {
    createAndApplyTexture('occlusionTexture', event);
  });

  document.querySelector('#emission').addEventListener('input', (event) => {
    createAndApplyTexture('emissiveTexture', event);
  });

  document.querySelector('#diffuse').addEventListener('input', (event) => {
    createAndApplyTexture('baseColorTexture', event);
  });

  document.querySelector('#metallicRoughness').addEventListener('input', (event) => {
    createAndApplyTexture('metallicRoughnessTexture', event);
  });
});

</script>
```
