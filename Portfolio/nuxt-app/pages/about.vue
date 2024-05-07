<!-- <template>
    <div>
        This Page is about me.
    </div>
    <div>
        <button @click="enableCustomLayout">Update Layout</button>
    </div>
</template>

<script setup>

definePageMeta{(
    layout: "another",
)}

function enableCustomLayout() {
    setPageLayout('another')
}

useHead({
    title: 'About'
})
</script> -->


<template>
    <article class="prose dark:prose-invert">
        <ContentDoc path="/about" />
    </article>
</template>