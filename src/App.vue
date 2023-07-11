<script setup>
const getAtiveTab = () => {
  return new Promise(resolve => {
    chrome.tabs.query({ active: true, currentWindow: true }, function (tabs) {
      resolve(tabs[0])
    }); 
  })
}
const hideImg = async () => {
  const tab = await getAtiveTab()
  chrome.scripting.executeScript({
    target: { tabId: tab.id },
    function: () => {
      const eles = document.querySelectorAll('img')
      if (eles && eles.length) {
        eles.forEach(ele => {
          ele.originHidden = ele.originHidden !== undefined ? ele.originHidden : ele.hidden
          ele.hidden = true
        })
      }
    }
  });
}
const restoreImgHidden = async () => {
  const tab = await getAtiveTab()
  chrome.scripting.executeScript({
    target: { tabId: tab.id },
    function: () => {
      const eles = document.querySelectorAll('img')
      if (eles && eles.length) {
        eles.forEach(ele => {
          ele.hidden = ele.originHidden
        })
      }
    }
  });
}
const hideIframe = async () => {
  const tab = await getAtiveTab()
  chrome.scripting.executeScript({
    target: { tabId: tab.id },
    function: () => {
      const eles = document.querySelectorAll('iframe')
      if (eles && eles.length) {
        eles.forEach(ele => {
          ele.originHidden = ele.originHidden !== undefined ? ele.originHidden : ele.hidden
          ele.hidden = true
        })
      }
    }
  });
}
const restoreIframeHidden = async () => {
  const tab = await getAtiveTab()
  chrome.scripting.executeScript({
    target: { tabId: tab.id },
    function: () => {
      const eles = document.querySelectorAll('iframe')
      if (eles && eles.length) {
        eles.forEach(ele => {
          ele.hidden = false
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
    <el-button @click="hideImg">隐藏图片</el-button>
    <el-button @click="restoreImgHidden">恢复图片</el-button>
    <el-button @click="hideIframe">隐藏iframe</el-button>
    <el-button @click="restoreIframeHidden">恢复iframe</el-button>
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
