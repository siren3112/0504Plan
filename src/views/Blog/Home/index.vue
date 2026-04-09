<template>
  <div class="blog-container">
    <header class="blog-header">
      <h1 class="title">我的个人博客</h1>
    </header>

    <main class="blog-main">
      <h2>欢迎来到我的博客！</h2>
      <p>这里是我们即将参考 loveli.kikiw.cn 实现优美 UI 的地方。</p>
    </main>
  </div>
</template>

<script setup lang="ts">
// 这里是 Vue 3 的 setup 语法糖区域
</script>

<style scoped>
.blog-container {
  min-height: 100vh;
  background-color: #f9f9f9;
}
.blog-header {
  padding: 20px;
  background: #fff;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
}
.title {
  margin: 0;
  color: #333;
}
.blog-main {
  padding: 40px;
  max-width: 1200px;
  margin: 0 auto;
}
</style>