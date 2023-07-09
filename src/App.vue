<script setup>
const clearImg = async () => {
  chrome.tabs.query({ active: true, currentWindow: true }, function (tabs) {
    chrome.scripting.executeScript({
      target: { tabId: tabs[0].id },
      function: () => {
        const imgs = document.querySelectorAll('img')
        if (imgs && imgs.length) {
          imgs.forEach(ele => {
            ele.remove()
          })
        }
      }
    });
  }); 
}
</script>

<template>
  <header>
  </header>

  <main>
    <el-button @click="clearImg">清楚图片</el-button>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}
</style>
