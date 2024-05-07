<template>
   <div class="not-prose">
    <section v-if="pending">Loading...</section>
    <section v-else-if="error">Something went wrong... Try again!</section>
    <section v-else>
        <ul class="grid grid-cols-1 gap-4">
            <li v-for="repository in repos" :key="repository.id" class="border border-gray-200 rounded-sm p-4 hover:bg-gray-100 font-mono">
                <a :href="repository.html_url" target="_blank"> 
                    <!-- blank - because it targets link to open in a new window. -->
                 <div class="flex items-center justify-between text-sm">
                    <div class="font-semibold">{{ repository.name }}</div>
                    <div>{{ repository.stargazers_count }} ★</div>
                </div>
                <p class="text-sm">
                    {{ repository.description }}
                </p>
                </a>
            </li>
        </ul>
    </section>
   </div>
</template>


<script setup>
const {error, pending, data} =  await useFetch("https://api.github.com/users/Bourbonmedici/repos")
// console.log("Data fetched from github API", data)
const repos = computed(() => {
  const filteredRepos = data.value.filter(repo => repo.description);
  console.log("filteredRepos in use",filteredRepos); // Debug statement to see filtered output
  return filteredRepos.sort((a, b) => b.stargazers_count - a.stargazers_count);
});

</script>