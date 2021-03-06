<template>
  <form id="donationform" class="flex flex-col" @submit.prevent="pay">
    <h2 class="text-center text-3xl md:text-4xl mt-8 py-10">Please enter your credit card details</h2>

    <label class="text-md md:text-xl py-4 flex flex-col md:flex-row justify-between items-center">
      <span class="font-bold">Donation Amount (in Euro):</span>
      <input
        v-model="amount"
        class="appearance-none text-right px-3 py-2 shadow-inner border"
        type="number"
        lang="en-150"
        min="0.50"
        max="10000.00"
        step="0.01"
        placeholder="13.37">
    </label>
    <label ref="email" class="text-lg md:text-xl py-4 flex flex-col md:flex-row justify-between items-center">
      <span class="font-bold">Your e-mail (optional):</span>
      <input
        v-model="email"
        type="email"
        placeholder="you@areaweso.me"
        class="appearance-none text-right px-3 py-2 shadow-inner border">
    </label>
    <label class="text-md md:text-xl py-4 flex flex-col md:flex-row justify-between items-center">
      <span class="font-bold">Leave me a message (optional):</span>
      <input
        v-model="message"
        placeholder="<3"
        class="appearance-none text-right px-3 py-2 shadow-inner border">
    </label>
    <span class="text-md md:hidden mt-8 font-bold">Credit Card Info</span>
    <card
      :options="stripeOptions"
      :stripe="key"
      :class="{'border-green-dark':complete}"
      class="rounded px-4 py-2 border mt-2 bg-white shadow-inner text-grey-darkest"
      @change="complete = $event.complete"
    />
    <p class="text-sm text-grey-darker mt-2">
      Don't worry. Payments are processed through Stripe
    </p>
    <p v-if="error" class="text-lg text-red-dark my-5" v-text="error"/>

    <button class="bg-green hover:bg-green-light px-16 py-4 rounded-full text-white text-2xl w-auto mx-auto shadow-lg border border-green-light mt-8">
      <span v-if="!loading">Donate ❤️</span>
      <span
        v-else
        class="cp-spinner cp-meter h-16 w-16"
      />
    </button>
  </form>
</template>

<script>
import { Card, createToken } from 'vue-stripe-elements-plus'
import { key, options } from '~/config/stripe.json'
import { Confetti } from 'vue-confetti'

export default {
  components: {
    Card
  },
  props: {
    donationType: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      complete: false,
      message: '',
      amount: undefined,
      loading: false,
      error: false,
      invalid: [],
      email: '',
      stripeOptions: options,
      key
    }
  },
  watch: {
    donationType(type) {
      if (!type) {
        return
      }
      if (type.price === -1) {
        this.amount = undefined
        return
      }
      this.amount = Number(type.price / 100).toFixed(2)
      setTimeout(() => this.$refs.email.focus(), 250)
    }
  },
  methods: {
    resetFormData() {
      this.resetFormState()
      this.amount = undefined
      this.email = ''
      this.message = ''
    },
    resetFormState() {
      this.loading = false
      this.error = false
      this.invalid = []
    },
    async pay() {
      this.resetFormState()
      if (!this.amount || Number.isNaN(this.amount)) {
        this.invalid.push(['amount'])
      }

      const { token } = await createToken()
      const { email, message, amount: cents } = this
      const amount = cents * 100

      if (this.invalid.length) {
        this.error = 'The form is not filled correctly. The amount is set wrong.'
        return
      }

      if (amount < 50) {
        this.error = 'Stripe does not accept payments lower than 50 cents'
        return
      }

      if (!this.complete) {
        this.error = 'Your Credit Card details are not correct'
        return
      }

      this.loading = true

      try {
        await this.$axios.$post('pay', { token, amount, donationType: this.donationType.slug, email, message }, {
          headers: {
            'Content-Type': 'application/json'
          }
        })
        this.loading = false

        this.resetFormData()
        this.$emit('completed')
        const confetti = new Confetti()
        confetti.start({})
        setTimeout(() => confetti.stop(), 5000)
      } catch ({ response: { data: { message } } }) {
        this.error = message
        this.loading = false
      }
    }
  }
}
</script>
