# 15 LIGHTS
* adding lights as simple as adding mesh
* instantiate with the right class and add to scene
* Remove `AmbientLight` and `PointLight`
* can't see anything on screen b/c `MeshStandardMaterial` needs light 
## AMBIENT LIGHT
* `AmbientLight` applies **omnidirectional lighting**:
    - color
    - intensity 
* add `AmbientLight` with colour and intensity parameters:
    ```
    const ambientLight = new THREE.AmbientLight(0xffffffff, 0.5)
    scene.add(ambientLight)
    ```
* adds light from all directions so light is uniform all around scene 
* add to `Debug UI`:
    ```
    gui.add(ambientLight, 'intensity').min(0).max(1).step(0.001)
    ```
* can use `AmbientLight` to simulate light bouncing 
## DIRECTIONAL LIGHT
* `DirectionalLight` has a **sun-like** effect as if the sun rays were travelling in parallel
    - color
    - intensity 
* add to scene:
    ```
    const directionalLight = new THREE.DirectionalLight(0x00fffc, 0.3)
    scene.add(directionalLight)

    gui.add(directionalLight, 'intensity').min(0).max(1).step(0.001)
    ```
* to change directional, move the light:
    ```
    directionalLight.position.set(1, 0.25, 0)
    ```
## HEMISPHERE LIGHT 
* `HemisphereLight` similar to `AmbientLight` but with a different colour from the sky than the colour coming from the ground 
    - color (or skyColor)
    - groundColor
    - intensity
* add to scene:
    ```
    const hemisphereLight = new THREE.HemisphereLight(0xff0000, 0x000ff, 0.3)
    scene.add(hemisphereLight)
    ```
## POINT LIGHT
* `PointLight` is like a **lighter** 
* light starts at an infinitely small point and spreads uniformly in every direction
    - color
    - intensity
* add to scene:
    ```
    const pointLight = new THREE.PointLight(0xff9000, 0.5)
    scene.add(pointLight)

    gui.add(pointLight, 'intensity').min(0).max(1).step(0.001)
    ```
* move the light:
    ```
    pointLight.position.set(1, -0.5, 1)
    ```
* by default the light intensity doesn't fade
* can control the fade distance and how fast it fades with `distance` and `decay`:
    ```
    const pointLight = new THREE.PointLight(0xff9000, 0.5, 10, 2)
    ```
## RECT AREA LIGHT
* `RectAreaLight` works light the big rectangle lights at photoshoot sets
* it's a mix between a **directional light** and **diffuse light** 
    - color
    - intensity
    - width
    - height 
* add to scene:
    ```
    const rectAreaLight = new THREE.RectAreaLight(0x4e00ff, 2, 1, 1)
    scene.add(rectAreaLight)
    gui.add(rectAreaLight, 'intensity').min(0).max(1).step(0.001)
    ```
* `RectAreaLight` only works with `MeshStandardMaterial` and `MeshPhysicalMaterial`
* can move the light and rotate it 
* can also use the `lookAt(...)` to rotate more easily:
    ```
    rectAreaLight.position.set(-1.5, 0, 1,5)
    rectAreaLight.lookAt(new THREE.Vector3())
    ```
* have to move position then use `lookAt(...)` property 
## SPOT LIGHT
* `SpotLight` is like a flashlight
* it's a **cone** of light starting at a point and orientated in a direction
    - color 
    - intensity
    - distance
    - angle (light width)
    - penumbra (dim on edges of shape)
    - decay (how fast it goes to limit)
* add to scene:
    ```
    const spotLight = new THREE.SpotLight(0x78ff00, 0.5, 10, Math.PI * 0.1, 0.25, 1)
    spotLight.position.set(0, 2, 3)
    scene.add(spotLight)
    gui.add(spotLight, 'intensity').min(0).max(1).step(0.001)
    ```
* to rotate the `SpotLight`, add its `target` property to the scene and move it:
    ```
    scene.add(spotLight.target)
    spotLight.target.position.x = -0.75
    ```
## PERFORMANCE
* lights can cost a lot when it comes to performance
* try to add as few lights as possible 
* try to use lights that cost less
### MINIMAL COST LIGHTS
* `AmbientLight`
* ` HemisphereLight`
### MODERATE COST LIGHTS
* `DirectionalLight`
* `PointLight`
### HIGH COST LIGHTS 
* `SpotLight`
* `RectAreaLight`
## BAKING 
* idea is to **bake** light into the texture
* done using a 3D software
* drawbacks are that you can't move the light anymore and you have to load huge textures 
## HELPERS
* to assist with positioning the light, you can use helpers:
    - `HemisphereLightHelper`
    - `DirectionalLightHelper`
    - `PointLightHelper`
    - `RectAreaLightHelper`
    - `SpotLightHelper`
* add `HemisphereLightHelper`:
    ```
    const hemisphereLightHelper = new THREE.HemisphereLightHelper(hemisphereLight, 0.2)
    scene.add(hemisphereLightHelper)
    ```
* add `DirectionalLightHelper`:
    ```
    const directionalLightHelper = new THREE.DirectionalLightHelper(directionalLight, 0.2)
    scene.add(directionalLightHelper)
    ```
* add `PointLightHelper`:
    ```
    const pointLightHelper = new THREE.PointLightHelper(pointLight, 0.2)
    scene.add(pointLightHelper)
    ```
* `SpotLightHelper` has no **size**:
    ```
    const spotLightHelper = new THREE.SpotLightHelper(spotLight)
    scene.add(spotLightHelper)
    ```
* `RectLightHelper` isn't part of the **THREE** variable and needs to be imported:
    ```
    // import
    import { RectAreaLightHelper } from 'three/examples/jsm/helpers/RectAreaLightHelper.js'

    // helpers
    const rectAreaLightHelper = new RectAreaLightHelper(rectAreaLight)
    scene.add(rectAreaLightHelper)
    ```