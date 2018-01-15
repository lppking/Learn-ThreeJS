## 矩阵转换

Three.js使用矩阵来表示3D转换，包括平移（位置），旋转以及缩放。每一个Object3D的实例都有一个存储了它们的位置，旋转和缩放信息的矩阵。以下内容讲了如何更新一个对象的转换信息。

---

### Convenience properties and matrixAutoUpdate

有两种方式来更新一个对象的转换信息：

1. 通过修改这个对象的**position**，**quaternion**，以及**scale**属性，three.js会根据修改后的属性值重新计算这个对象的矩阵（matrix）信息。

```
object.position.copy(start_position);
object.quaternion.copy(quaternion);
```

默认情况下，matrixAutoUpdate属性是设置为true，matrix将会自动重新计算。如果这个对象时静态的或者是你希望手动控制何时重新计算matrix，可以通过将**matrixAutoUpdate设置为false来高效的实现**：

```
object.matrixAutoUpdate = false;
```

在我们更改了某些属性后，通过如下方法手动更新matrix：

```
object.updateMatrix();
```

2. 直接修改这个对象的matrix。**Matrix4**这个类提供了多种方法来修改matrix：

```
object.matrix.setRotationFromQuaternion(quaternion);
object.matrix.setPosition(start_position);
obejct.matrixAutoUpdate = false;
```

这个地方的**matrixAutoUpdate**属性值必须为**false**，并且不可以手动调用**updateMatrix**方法。原因是如果没有取消自动更新或者是手动调用了自动更新，会基于position，scale等信息重新计算matrix，会覆盖掉你手动更改的值。

---

### Object and world matrices

一个对象的matrix存储了这个对象相对于其父对象的转换信息。如果要获取这个对象在全局坐标（world coordinates）中的转换信息，就必须访问该对象的Object3D.matrixWorld属性。

当子对象或者其父对象的转换信息（transformation）发生改变时，你可以通过调用updateMatrixWorld()来更新子对象的**matrixWorld**。

---

### Rotation and Quaternion

Three.js提供了两种方式来表示三维旋转：欧拉角（Euler angles）和四元数（Quaternions），以及在两者之间进行转换的方法。欧拉角受“万向锁（gimbol lock）”的影响，是在使用动态欧拉角表示三维物体的旋转时会出现的问题。出于这个原因，对象旋转相关总是存储在对象的**quaternion**中。

在早先的版本中，包含一个**useQuaternion**属性，通过设置为false，使对象的matrix使用欧拉角来计算。现在不建议这么做，推荐使用**setRotationFromEuler**方法来代替。

