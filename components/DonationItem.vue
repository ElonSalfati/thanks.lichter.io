<template>
  <button class="flex flex-col md:flex-row items-center my-8 border border-grey-light shadow-lg p-4 w-full hover:scale-105 transition-all-300">
    <span class="flex flex-no-shrink flex-col md:mr-8 mb-4 md:mb-0">
      <img v-bind="imageSources" :alt="name" class="rounded-full border border-grey">
    </span>
    <span class="text-center md:text-left">
      <span class="block text-2xl font-bold py-3">{{ textPrice }} — {{ name }}</span>
      <span v-text="description"/>
    </span>
  </button>
</template>

<script>

export default {
  props: {
    name: {
      type: String,
      required: true
    },
    slug: {
      type: String,
      default: 'kolle'
    },
    description: {
      type: String,
      required: true
    },
    price: {
      type: Number,
      required: true
    }
  },
  computed: {
    textPrice() {
      if (this.price !== -1) {
        const euro = this.price / 100
        return `${euro.toFixed(2).toLocaleString()} €`
      }
      return '???? €'
    },
    imageSources() {
      return {
        src: require(`~/assets/donations/${this.slug}.png`),
        srcset: `${require(`~/assets/donations/${this.slug}@2x.png`)} 2x`
      }
    }
  }
}
</script>
