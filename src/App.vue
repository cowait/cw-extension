<script setup>
const getAtiveTab = () => {
  return new Promise(resolve => {
    chrome.tabs.query({ active: true, currentWindow: true }, function (tabs) {
      resolve(tabs[0])
    }); 
  })
}
const clearIframe = async () => {
  const tab = await getAtiveTab()
  chrome.scripting.executeScript({
    target: { tabId: tab.id },
    function: () => {
      const eles = document.querySelectorAll('iframe')
      if (eles && eles.length) {
        eles.forEach(ele => {
          ele.remove()
        })
      }
    }
  });
}
const clearImg = async () => {
  const tab = await getAtiveTab()
  chrome.scripting.executeScript({
    target: { tabId: tab.id },
    function: () => {
      const imgs = document.querySelectorAll('img')
      if (imgs && imgs.length) {
        imgs.forEach(ele => {
          ele.remove()
        })
      }
    }
  });
}
</script>

<template>
  <header>
  </header>

  <main>
    <el-button @click="clearImg">清楚图片</el-button>
    <el-button @click="clearIframe">清除iframe</el-button>
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
