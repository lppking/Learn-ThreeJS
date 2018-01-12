## 画线

本部分介绍如何使用ThreeJS画线段。

---

1. 准备三大核心元素

```
/*
  创建一个渲染器
*/
var renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

/*
  创建一个相机
  THREE.Vector3是一个3D矢量类，通过一个有序的三维坐标，可以用来表示三维空间中的一个点或是三维空间中的方向和长度
*/
var camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 1, 500)
camera.position.set(0, 0, 100)  // 设置相机的位置
camera.lookAt(new THREE.Vector3(0, 0, 0))   // 设置相机面向的方向

/*
  创建一个场景
*/
var scene = new THREE.Scene();
```

2. 创建材质

```
/*
  创建一个蓝颜色的实线材质
*/
var matetial = new THREE.LineBasicMaterial({
  color: 0x0000ff
});
```

3. 创建点（点构成线段）

```
/*
  创建几何体
  可以使用Geometry或者是BufferGeometry，后者性能好，前者简单
  geometry.vertices是一个点的集合，我们push三个点，可以连接两条线
*/
var geometry = new THREE.Geometry();
geometry.vertices.push(new THREE.Vector3(-10, 0, 0))    // 第一个点
geometry.vertices.push(new THREE.Vector3(0, 10, 0)) // 第二个点
geometry.vertices.push(new THREE.Vector3(10, 0, 0)) // 第三个点，不是起点，所以不闭合
```

4. 用点和材质生成线段

```
/*
  有了点geometry和材质material，就可以使用THREE.Line生成线
*/
var line = new THREE.Line(geometry, matetial);
```

5. 将线段添加到场景，调用渲染器渲染

```
/*
  最后一步，把线添加到场景，在渲染器中渲染场景和相机
*/
scene.add(line);
renderer.render(scene, camera)
```