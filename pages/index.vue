<template>
  <div class="bg-grey-lighter">
    <section class="flex flex-col justify-center items-center flex-wrap pb-16">
      <h1 class="text-center text-3xl md:text-4xl py-10">Your support is powerful!</h1>
      <div class="flex flex-col md:flex-row justify-around items-center w-5/6 md:w-2/3 mx-auto text-center">
        <div class="flex-1">
          <div>
            <img
              src="/img/me.jpg"
              srcset="/img/me@2x.jpg 2x"
              alt="Alexander Lichter"
              class="rounded-full border-solid border-4 border-grey-light shadow-lg mb-2 w-64 h-64">
            <p class="mb-2 font-light text-lg md:text-2xl">
              Alexander Lichter
            </p>
          </div>
          <vue-next-level-scroll target="#donate">
            <button class="mt-16 bg-green hover:bg-green-light px-8 py-4 rounded-full text-white text-2xl shadow-lg border border-green-light">
              Donate 🙏
            </button>
          </vue-next-level-scroll>
        </div>
        <div class="flex-1 text-left">
          <p class="mt-6 text-lg">
            👋 Hey! I am Alex, a freelance web developer and
            <a
              class="no-underline text-green-dark hover:underline"
              href="https://github.com/nuxt/nuxt.js#core-team"
              target="_blank"
              rel="noreferrer noopener">Nuxt.js</a>
            core team member. But since you're on this page, you probably already know this.
          </p>
          <p class="mt-6 text-lg">
            My goal is to contribute as much as possible to the Nuxt.js ecosystem.
            Currently, I am helping developers on a daily basis in the Discord, on GitHub and on
            <a
              class="no-underline text-blue-light hover:underline"
              href="http://twitter.com/TheAlexLichter"
              target="_blank"
              rel="noreferrer noopener"
            >Twitter</a>, writing blog posts and guides about programming topics and maintaining several packages.
          </p>
          <p class="mt-6 text-lg">
            Besides working on the Nuxt.js core, I've created a hand full of modules to make the developer's lives
            easier:
          </p>

          <ul class="mt-4 text-lg">
            <li>
              <a
                rel="noreferrer noopener"
                target="_blank"
                class="github-link"
                href="https://github.com/nuxt-community/redirect-module"
              >@nuxtjs/redirect-module</a> - Redirect old URLs to keep SEO up
            </li>
            <li>
              <a
                rel="noreferrer noopener"
                target="_blank"
                class="github-link"
                href="https://github.com/nuxt-community/feed-module"
              >@nuxtjs/feed-module</a> - Blog feeds for everyone!
            </li>
            <li>
              <a
                rel="noreferrer noopener"
                target="_blank"
                class="github-link"
                href="https://github.com/nuxt-community/separate-env-module/"
              >@nuxtjs/separate-env-module</a> - Split env values into server/client
            </li>
            <li>
              <a
                rel="noreferrer noopener"
                target="_blank"
                class="github-link"
                href="https://github.com/Developmint/nuxt-svg-loader"
              >nuxt-svg-loader</a> - Load SVGs as you'd load Vue components
            </li>
            <li>
              <a
                rel="noreferrer noopener"
                target="_blank"
                class="github-link"
                href="https://github.com/Developmint/nuxt-purgecss"
              >nuxt-purgecss</a> - Delete superfluous CSS
            </li>
            <li>You can find more on my
              <a
                rel="noreferrer noopener"
                target="_blank"
                class="github-link"
                href="https://github.com/manniL"
              >own GitHub</a> and
              <a
                rel="noreferrer noopener"
                target="_blank"
                class="github-link"
                href="https://github.com/manniL"
              >company GitHub</a> profile
            </li>
          </ul>

          <p class="mt-6 text-lg">
            I'm doing all of this in my <span class="font-bold">free time</span>! But I'd love to work on all these
            things <span class="font-bold">full time</span> one day.
          </p>
        </div>
      </div>
      <h2
        id="say-thanks"
        class="text-center text-3xl md:text-4xl mt-8 py-10">Say thanks</h2>
      <div class="flex justify-around items-center w-5/6 md:w-2/3 mx-auto text-center">
        <div class="flex-1 text-left">
          <p class="mt-6 text-xl">
            I really appreciate kind words or a simple <span class="text-black">thank you</span> a lot!
            This is what keeps me motivated (even on a bad Monday). Same goes for sharing my content or starring one of
            my libraries.
            <br><br>
            Unfortunately, I have to make a living somehow as well. On the one hand, I am offering Nuxt.js consulting
            through my company Developmint. However, if you know a company that needs help, code reviews, feedback, best
            practices or an external audit, feel free to pass my website along so they can
            <span class="font-bold">hire me</span>!
            <br>
            As it's in the nature of consulting, this is a very unsteady and unreliable kind of income though....
          </p>
        </div>
      </div>
      <h2 id="donate" class="text-center text-3xl md:text-4xl mt-8 py-10">Donate</h2>
      <div class="flex flex-col justify-around items-center w-5/6 md:w-2/3 mx-auto text-center">
        <div class="flex-1 text-left">
          <p class="mt-6 text-xl">
            If you think my community work and effort is worth a small donation, then here comes the opportunity!<br>
            <span class="font-bold">Every donation, no matter how small</span> helps me to cover the bills and to invest
            more time into open-source,
            the Nuxt ecosystem and helping out people.
          </p>
          <div class="mt-16 md:mt-32">
            <vue-next-level-scroll
              v-for="(item, i) in $options.donationItems"
              :key="i"
              target="#donationform">
              <donation-item
                v-bind="item"
                @click.native="changeDonationType(item)"/>
            </vue-next-level-scroll>
          </div>
        </div>
      </div>
      <div class="flex py-8 flex-col justify-around items-center w-5/6 md:w-2/3 mx-auto text-center">
        <donation-form :donation-type="donationType" @completed="showThanks = true"/>
      </div>
      <div
        v-if="showThanks"
        class="flex flex-col py-8 justify-around items-center w-5/6 md:w-2/3 mx-auto text-center md:mt-8 bg-white shadow-inner">
        <p class="text-lg">
          <span class="font-bold text-4xl">Thank you for your Donation!</span><br>
          People like you help the open-source community to stay alive and grow 😍
        </p>
      </div>
      <div class="flex flex-col py-8 justify-around items-center w-5/6 md:w-2/3 mx-auto text-center md:mt-8">
        <div class="mb-8">
          <h3 class="text-center text-3xl md:text-4xl mt-8 py-10">Don't own a credit card?</h3>
          <p>Supporting me via Wire Transfer is also possible!</p>
        </div>
        <div class="flex flex-col font-mono md:w-1/3 flex-no-shrink">
          <div
            v-for="([k,v]) in $options.bankDetails"
            :key="k"
            class="flex my-2 md:my-0">
            <div class="w-1/3 text-left" v-text="k"/>
            <div class="w-2/3 text-right" v-text="v"/>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  components: {
    VueNextLevelScroll: () => import('vue-next-level-scroll'),
    DonationItem: () => import('~/components/DonationItem'),
    DonationForm: () => import('~/components/DonationForm')
  },
  data() {
    return {
      donationType: {
        slug: 'none',
        price: -1
      },
      showThanks: false
    }
  },
  methods: {
    changeDonationType(type) {
      this.donationType = type
    }
  },
  donationItems: [
    {
      name: 'Public transport ticket',
      slug: 'ticket',
      description: 'Public transport isn\'t cheap in Germany, but it is still cheaper than driving by car and additionally paying for the parking lot',
      price: 261
    },
    {
      name: 'Fund one of my domains for a year',
      slug: 'domain',
      description: 'Domain registration is cheap... if you only have one. But who has only one domain and not like.. fifty? (No I am not addicted!)',
      price: 666
    },
    {
      name: 'Seven bottles of my favorite local soft drink',
      slug: 'kolle',
      description: 'That drink is called Kolle Mate and is locally produced in Dresden, Germany. It has caffeine included and is extremely delicious!',
      price: 1050
    },
    {
      name: 'Two months of Spotify Premium',
      slug: 'spotify',
      description: 'Honestly, I could not live without music! Listening to it while programming makes me way more productive, believe it or not!',
      price: 1998
    },
    {
      name: 'A bottle of 10 year old Talisker Scotch',
      slug: 'talisker',
      description: 'After releasing a new version or finishing a large piece of content I like to celebrate the achievement with a fine glass of Scotch',
      price: 3399
    },
    {
      name: 'Whatever you think is right',
      slug: 'questionmark',
      description: 'You are the one who wants to support me, so you are the one that selects the amount in the end!',
      price: -1
    }
  ],
  bankDetails: [
    ['Name', 'Alexander Lichter'],
    ['Subject', 'Lichter.io Donation'],
    ['Bank', 'Deutsche Kreditbank'],
    ['IBAN', 'DE80 1203 0000 1036 7634 05'],
    ['SWIFT / BIC', 'BYLADEM1001']
  ]
}
</script>
