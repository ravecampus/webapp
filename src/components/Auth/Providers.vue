<template>
  <v-layout column class="px-5 pb-5">
    <div
      v-for="provider in providers" 
      :key="provider.title"
    >
      <v-btn
        dark
        class="providerBtn" 
        :class="provider.title"
        block
        @click="authenticate(provider.title)"
        v-if="provider.title === 'google'"
      >
        <component :is="provider.icon" />
        {{ provider.title }} Login
      </v-btn>
      <v-tooltip bottom v-else>
        <v-btn
          dark
          class="providerBtn" 
          :class="provider.title"
          slot="activator"
          @click="authenticate(provider.title)"
          block
        >
          <component :is="provider.icon" />
          {{ provider.title }} Login
        </v-btn>
        <span>Coming Soon</span>
      </v-tooltip>
    </div>
  </v-layout>
</template>
<script>
import GoogleIcon from '@components/Icons/Google';
import FacebookIcon from '@components/Icons/Facebook';
import TwitterIcon from '@components/Icons/Twitter';
import GithubIcon from '@components/Icons/Github';
import { LOGIN_START } from '@state/mutationTypes';

export default {
  data: () => ({
    providers: [
      {
        title: 'google',
        icon: GoogleIcon,
      },
      {
        title: 'facebook',
        icon: FacebookIcon,
      },
      {
        title: 'twitter',
        icon: TwitterIcon,
      },
      {
        title: 'github',
        icon: GithubIcon,
      },
    ],
  }),
  methods: {
    authenticate: function(provider) {
      this.$store.dispatch(`auth/${LOGIN_START}`, { provider, vue: this });
    },
  },
};
</script>

<style lang="stylus" scoped>
@import '~@assets/style/variables';

.providerBtn {
  &.google {
    color: $colors.google.text !important;
    background-color: $colors.google.bg !important;
  }

  &.facebook {
    background-color: $colors.facebook.bg !important;
  }

  &.twitter {
    background-color: $colors.twitter.bg !important;
  }

  &.github {
    background-color: $colors.github.bg !important;
  }

  /* stylelint-disable-next-line */
  /deep/ .v-btn__content {
    justify-content: flex-start;
    font-weight: bold;
    text-transform: capitalize;
  }

  /deep/ svg {
    width: 18px;
    height: 18px;
    margin-right: 16px;
  }
}
</style>
