<template>
  <v-container class="fill-height" fluid>
    <v-layout align-center>
      <v-flex text-center>
        <h1 class="display-3 primary--text">
          {{ $t('No internet') }}
        </h1>
        <p class="my-5">
          {{ $t('Please check that you are connected to the internet.') }}
        </p>
        <v-btn :to="{ name: 'home' }" replace outlined color="primary">
          {{ $t('Refresh') }}
        </v-btn>
      </v-flex>
    </v-layout>
  </v-container>
</template>
