<template>
  <div>
    <v-tabs centered>
      <v-tab v-for="(tab,i) in tabs" :key="i" :to="{ name: tab.route }">
        {{ tab.name }}
      </v-tab>
    </v-tabs>
    <router-view />
  </div>
</template>

<script>
export default {
  middleware: ['auth', 'verified', '2fa_passed', 'admin'],

  data () {
    return {
      activeTab: null
    }
  },

  computed: {
    tabs () {
      const tabs = [
        { route: 'admin.dashboard.users', name: this.$t('Users') },
        { route: 'admin.dashboard.affiliates', name: this.$t('Affiliates') },
        { route: 'admin.dashboard.games', name: this.$t('Games') },
        { route: 'admin.dashboard.bonuses', name: this.$t('Bonuses') }
      ]

      if (this.$store.getters['package-manager/getById']('payments')) {
        tabs.push({ route: 'admin.dashboard.accounting', name: this.$t('Accounting') })
      }

      return tabs
    }
  }
}
</script>
