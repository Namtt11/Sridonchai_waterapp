<template>
  <div>
    blog index

    <ul>
      <li v-for="blog in blogs">
        <RouterLink class="link link-primary" :to="`/blog/${blog.id}`">{{ blog.title }}</RouterLink>
      </li>
    </ul>

    <details class="dropdown">
      <summary class="m-1 btn">open or close</summary>
      <ul class="p-2 shadow menu dropdown-content z-[1] bg-base-100 rounded-box w-52">
        <li><a>Item 1</a></li>
        <li><a>Item 2</a></li>
      </ul>
    </details>

    <details class="dropdown">
      <summary class="m-1 btn">open or close</summary>
      <ul class="p-2 shadow menu dropdown-content z-[1] bg-base-100 rounded-box w-52">
        <li><a>Item 1</a></li>
        <li><a>Item 2</a></li>
      </ul>
    </details>
  </div>
</template>

<script lang="ts" setup>
import { Blog } from '@/domains/entities/blog'


let blogs: Blog[] = [
  new Blog(1, "Hello"),
  new Blog(2, "World"),
  new Blog(3, "Human"),
]



</script>

<style></style>