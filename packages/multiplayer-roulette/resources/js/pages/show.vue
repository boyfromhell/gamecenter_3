<template>
  <key-value-table
    name="game"
    :api="`/api/history/games/${id}`"
    :headers="headers"
  >
    <template v-slot:account.user.name="{ item: { account: { user } } }">
      <user-profile-modal :user="user" />
    </template>
    <template v-slot:gameable.bets="{ item: { account: { user }, gameable: { bets } } }">
      <template v-for="(item, type) in bets[user.id]">
        <v-badge
          :key="type"
          :color="type === 'zero' ? 'green' : type"
          :content="item.bet"
          :value="true"
          inline
          class="ml-2"
        />
      </template>
    </template>
  </key-value-table>
</template>

<script>
import KeyValueTable from '~/components/KeyValueTable'
import UserProfileModal from '~/components/UserProfileModal'

export default {
  components: { UserProfileModal, KeyValueTable },

  props: ['id'],

  computed: {
    headers () {
      return [
        { text: this.$t('Player'), value: 'account.user.name' },
        { text: this.$t('Game'), value: 'title' },
        { text: this.$t('Bet'), value: 'bet', format: 'decimal' },
        { text: this.$t('Win'), value: 'win', format: 'decimal' },
        { text: this.$t('Profit'), value: 'profit', format: 'decimal' },
        { text: this.$t('Bets'), value: 'gameable.bets' },
        { text: this.$t('Winning number'), value: 'gameable.win_number' },
        { text: this.$t('Played'), value: 'updated_ago' }
      ]
    }
  }
}
</script>
