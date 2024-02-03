<script setup lang="ts">
import { ipcRenderer } from 'electron'
import process from 'process'

const openDevTool = () => {
  ipcRenderer.send('msg-trigger', { type: 'openPluginDevTools' });
}

const minimize = () => {
  ipcRenderer.send('detach:service', { type: 'minimize' });
}

const maximize = () => {
  ipcRenderer.send('detach:service', { type: 'maximize' });
}

const close = () => {
  ipcRenderer.send('detach:service', { type: 'close' });
}
</script>

<template>
  <div class="custom-title">
    <div class="info">
      <!-- <img :src="plugInfo.logo" /> -->
      <span>rubick 系统菜单</span>
    </div>
    <div class="handle-container">
      <div class="handle">
        <div class="devtool" @click="openDevTool" title="开发者工具"></div>
      </div>
      <div class="window-handle" v-if="process.platform !== 'darwin'">
        <div class="minimize" @click="minimize"></div>
        <div class="maximize" @click="maximize"></div>
        <div class="close" @click="close"></div>
      </div>
    </div>
  </div>
</template>
