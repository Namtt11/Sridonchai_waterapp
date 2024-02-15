<template>
    <div>
      view blog by id = {{ name }}
      
    </div>
  </template>
  
  <script lang="ts" setup>
  
  const route = useRoute()
  console.log(route.params)
  
  const name = route.params.name
  
  
  </script>
  
  <style>
  
  </style>