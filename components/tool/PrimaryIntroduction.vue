<template>
  <div class="lg:m-8 lg:mt-6 p-4 rounded-lg border border-gray-200 bg-gray-50
              dark:bg-slate-800 dark:border-slate-500">
    <p class="font-bold text-lg mb-1.5 dark:text-slate-300" v-if="title">{{ title }}</p>
    <div class="mb-4" v-if="document">
      <nuxt-content class="prose prose-sm max-w-none reset-code overflow-x-auto
                           dark:prose-p:text-slate-300 dark:prose-headings:text-slate-300
                           dark:prose-strong:text-slate-300 dark:prose-table:text-slate-300" :document="document"/>
    </div>
    <div class="flex flex-col" v-if="references">
      <p class="font-bold text-lg mb-1 dark:text-slate-300">References</p>
      <a v-for="reference in references" :href="reference.url"
         class="group text-blue-500 italic w-fit" target="_blank">
        {{ reference.name }}
        <ion-icon class="align-middle -mt-0.5 transition-transform group-hover:translate-x-1"
                  name="arrow-forward-outline"/>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "PrimaryIntroduction",
  props: {
    title: {
      type: String,
      default: null
    },
    references: {
      type: Array,
      default: null
    },
    path: {
      type: String,
      default: null
    }
  },
  data() {
    return {
      document: null
    }
  },
  async mounted() {
    this.document = await this.$content(this.path).fetch();
  },
}
</script>

<style>
.reset-code {
  @apply prose-code:before:content-none prose-code:after:content-none prose-code:rounded prose-code:bg-gray-300 dark:prose-code:bg-slate-500 dark:prose-code:text-slate-50 prose-code:py-0.5 prose-code:px-1 prose-code:mx-0.5;
}

.nuxt-content-container {
  position: inherit !important;
}
</style>
