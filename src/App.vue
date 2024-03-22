<script setup lang="ts">
const { exec, ChildProcess } = require('node:child_process')

const controller = new AbortController()
const { signal } = controller
console.log('singal', signal)
console.log('controller', controller)
let process: null | typeof ChildProcess = null

const doexec = (command: string) => {
  process = exec(command, { signal }, (err, stdout, stderr) => {
    if (err) {
      console.error('exec error:', err)
      return
    }
    console.log('stdout:', stdout)
  })
}

const exit = () => {
  controller.abort()
  if (process) {
    process.kill()
  }
}


</script>


<template>
  <div>
    <button @click="doexec('D:\\tools\\MarkText\\MarkText.exe')">exec notepad.exe</button>
    <button @click="exit">exec notepad.exe</button>
  </div>
</template>

<style></style>
