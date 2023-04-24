# ThreeJS
ThreeJS实践


## 描述 ##

1. 初始化：定义场景、相机、渲染器、轨道控制器、绘制地面网络
2. 绘制地板，通过旋转调整角度贴合地板，并删去地面网络。
3. 加载3D模型，用load加载后，能拿到树状结构的obj
4. 绘制环境光，才能看到模型
5. 使用圆柱体实现展厅的效果
6. 引入GUI，增加调试面板


## 细节 ##

1. 属于场景中的配置项，最终都要加入场景中，scene.add(carModel)，比如3D模型、灯光、控制器。

2. 加载glb格式的3D模型需要一个new 一个 load，将3D模型传进去，

3. 轨道控制器：1.让场景旋转。2.控制视角范围，以免穿模穿帮。3.设置惯性，记得在render里update

4. threeJS有一个修改器，导入模型就可以在里面操作，直到自己喜欢的样子

5. 加载模型后会有carModal.traverse()方法，可以遍历每个节点对象，修改对应属性， 实现自定义效果

6. Tween实现动画

1. 阴影三步

   ```js
   // 阴影第一步：渲染器支持阴影
   renderer.shadowMap.enabled = true;
   //阴影第二步：模型产生阴影
   obj.castShadow = true;
   //阴影第三步：地面接收阴影
   floorMesh.receiveShadow = true;
   ```

2. 光线投射类Raycaster

   ```js
   光线投射用于进行鼠标拾取（在三维空间中计算出鼠标已过了什么物体）
     //光线投射类，用于鼠标交互，可以捕捉到穿越了什么物体
     var raycaster = new Raycaster();
   	var vector = new Vector2(pointer.x, pointer.y); //x,y是世界坐标系下的
     raycaster.setFromCamera(vector, camera);
     let intersects = raycaster.intersectObjects(scene.children);
   
   1.通过点击事件拿到点击的坐标，换算成世界坐标系
   2.通过raycaster可以知道点击事件点到了图层数组。
   3.遍历图层数组，然后根据name来取得对应图层，再作相应的处理，如果门的状态为关，则执行开门动画，否则执行关门动画
   ```

   
