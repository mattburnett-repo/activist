<template>
  <div>
    <Head>
      <Title>{{ title }}</Title>
    </Head>
    <h1 class="p-4 text-light-text dark:text-dark-text">
      This is a page about getting active
    </h1>
  </div>
</template>

<script setup>
const title = ref("Get Active");
</script>