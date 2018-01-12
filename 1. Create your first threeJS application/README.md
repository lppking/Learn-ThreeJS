## Create your first threeJS application

本部分将涉及到ThreeJS最基础的内容，同时完成第一个完整的ThreeJS应用。

```
    /**
     * Three核心要素包含三个部分：scene, camera, renderer
     */
    var scene = new THREE.Scene();  // 创建一个Scene

    /**
     * 创建一个Camera（透视投影）
     * 75：field of view(FOV)，视野，即可见范围（度）
     * window.innerWidth / window.innerHeight：aspect ratio（长宽比），相机水平方向和竖直方向的比值，通常设置为Canvas的横纵比例
     * 0.1：相机（和物体）最近距离
     * 1000：最远距离
     */
    var camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    
    var renderer = new THREE.WebGLRenderer();

    /**
     * setSize()支持在保持渲染大小不变的情况下降低分辨率，用法如下：
     * .setSize(window.innerWidth/2, window.innerHeight/2, false) 这种用法渲染后canvas标签的大小仍然是100%，但是分辨率是原先的一半
     */
    renderer.setSize(window.innerWidth, window.innerHeight);  // 这个渲染大小会影响性能
    document.body.appendChild(renderer.domElement); // append canvas element

    /**
     * 要建立一个立方体，我们需要一个BoxGeometry对象，这个对象包含了立方体的所有点和面.
     */
    var geometry = new THREE.BoxGeometry(1, 1, 1);
    
    /**
     * 有了支架（立方体），还需要给立方体一个外表皮肤（材质）
     * 这里我们只设置材质的颜色
     */
    var material = new THREE.MeshBasicMaterial({
      color: 0x00ff00
    });
    var cube = new THREE.Mesh(geometry, material);
    scene.add(cube);  // 向场景中添加立方体，这个立方体将会被添加到(0, 0, 0)，这会导致立方体和相机重合

    camera.position.set(0,0,5);  // 将相机的位置延Z轴正方向移动5个距离，相机目前的位置(0,0,5)，所以我们是俯视物体

    /**
     * 到目前为止，画面上不会有任何内容，因为我们只是添加了一个渲染器renderer，但是渲染器中没有添加任何内容，所以不会有任何东西
     * 使用requestAnimationFrame相较于setInterval有一个明显的优点，就是当用户选择别的tab页时，当前的渲染会停下来
     */
    function animate() {
      requestAnimationFrame(animate); // 60hz
      rotateCube();
      renderer.render(scene, camera);
    }
    function rotateCube() {
      cube.rotation.x += 0.01;
      cube.rotation.y += 0.01;
    }
    animate();
```
