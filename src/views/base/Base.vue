<template>
  <div>

  </div>
</template>
<script>
import * as THREE from "three";
// 导入轨道控制器
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";

export default {
  mounted() {
    this.init()
  },
  methods: {
    init() {
      // 1，创建场景
      const scene = new THREE.Scene();

      // 添加坐标轴辅助器
      const axesHelper = new THREE.AxesHelper(5);
      scene.add(axesHelper);

      // 2，创建相机
      const camera = new THREE.PerspectiveCamera()
      camera.position.set(8,4,12);
      scene.add(camera);


      // 添加物体
      const cube = new THREE.BoxGeometry(1,1,1);
      const material = new THREE.MeshBasicMaterial({color: 'red'});
      const mesh = new THREE.Mesh(cube, material);
      scene.add(mesh);


      // 3，创建渲染器
      const renderer = new THREE.WebGLRenderer();
      renderer.setSize(window.innerWidth, window.innerHeight);
      document.body.appendChild(renderer.domElement);


      // 创建轨道控制器
      const controls = new OrbitControls(camera, renderer.domElement);

      // 如果OrbitControls改变了相机参数，重新调用渲染器渲染三维场景
      controls.addEventListener('change', function () {
        // 浏览器控制台查看相机位置变化
        console.log('camera.position',camera.position);
        renderer.render(scene, camera); //执行渲染操作
      });//监听鼠标、键盘事件


      renderer.render(scene, camera);

    }
  }
}
</script>
