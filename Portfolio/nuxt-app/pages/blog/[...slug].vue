<template>
   <article
   class="prose dark:prose-invert max-w-none prose-pre:bg-white dark:prose-pre:bg-gray-800 prose-pre:text-gray-700 dark:prose-pre:text-gray-300">
      <!-- inside this prose element all typographic elements could be applied prose invert inverts colors 
      for dark mode   -->
    <ContentDoc v-slot="{doc}">
      <div class="grid grid-cols-6 gap-16">
         <div :class="{'col-span-4': doc.toc, 'col-span-6': !doc.toc}">
            <ContentRenderer :value="doc" />
         </div>
         <div class="col-span-2 not-prose" v-if="doc.toc">
            <aside class="sticky top-8">
               <div class="font-semibold mb-2">
                     Table of Contents
               </div>
               <nav>
                  <TocLinks :links="doc.body.toc.links" :active-id="activeId"/>
               </nav>
            </aside>
         </div>
      </div>
   </ContentDoc>
   </article>
</template>

<script setup>
const activeId = ref(null)
onMounted(() => {
   const callback = (entries) => { 
      for(const entry of entries) {
      if(entry.isIntersecting){
         activeId.value = entry.target.id 
         break;
      }
      }
   }
const observer = new IntersectionObserver(callback,{
   root: null,
   threshold: 0.5
})
// @ts-ignore
const elements = document.querySelectorAll('h2,h3')

for(const element of elements) {
   observer.observe(element)
}

onBeforeUnmount(()=>{
   for(const element of elements){
      observer.unobserve(element)
   }
})
})
</script>