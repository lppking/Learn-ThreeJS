## 通过模块导入

通过script标签导入three.js是一种快速启动运行的好方法，但是对于一个有长生命周期的项目而言，会有以下三个方面的缺点：

- 每次引用都需要重复的手工导入
- 如果要升级库版本也需要手动进行替换
- 构建文件中版本差异控制会受到影响

通过使用像npm这样的依赖管理工具可以让你在你的项目中简单方面的下载和导入你期望的库版本，最终避免如上所述的问题。

---

### 通过npm导入

Three.js已经发布到了npm上。所以如果你想要在项目中导入Three.js库只需要运行`npm install three`。注意：项目中通过npm导入分为局部导入和全局导入，相关内容可以自行google。

---

### 模块引用

假如你使用Webpace或者是Browserify来构建你的项目，你可以使用`require('modules')`的形式引入你需要的模块。如下所示：

```
var THREE = require('three');
var scene = new THREE.Scene();

```

你同样可以使用ES6新增的模块导入方法：

```
import * as THREE from 'three';
const scene = new THREE.Scene();
```

如果你不想要一次性导入Three的所有模块，只是想使用Scene模块，可以使用如下所示方法导入：

```
import { Scene } from 'three';
const scene = new Scene();
```
