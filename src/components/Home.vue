<template>
  <v-container>
    <v-layout>
      <v-flex xs12 class="text-xs-center">
        <v-progress-circular
        :size="70"
        :width="7"
        color="purple darken-4"
        indeterminate
        v-if="loading"
      ></v-progress-circular>
      </v-flex>
    </v-layout>

    <v-layout row wrap class="my-3">
      <v-flex xs12 class="text-xs-center">
        <h2>Join our meetups!</h2>
      </v-flex>
    </v-layout>

    <v-layout row wrap v-if="!loading">
      <v-flex xs12>
        <v-carousel class="pointer">
          <v-carousel-item
            v-for="meetup in meetups"
            :key="meetup.id"
            :src="meetup.imageUrl"
            @click.native="onLoadMeetup(meetup.id)"
          >
            <div class="title">{{ meetup.title }}</div>
          </v-carousel-item>
        </v-carousel>
      </v-flex>
    </v-layout>

    <v-layout row wrap class="mt-3" v-if="!userIsAuthenticated">
      <v-flex xs12 sm6 class="text-xs-center text-sm-right">
        <v-btn large router :to="{name: 'meetups'}" color="purple darken-4" dark>Explore Meetups</v-btn>
      </v-flex>
      <v-flex xs12 sm6 class="text-xs-center text-sm-left">
        <v-btn large router :to="{name: 'createMeetup'}" color="purple darken-4" dark>Organize Meetup</v-btn>
      </v-flex>
    </v-layout>

  </v-container>
</template>

<script>
export default {
  computed: {
    meetups () {
      return this.$store.getters.featuredMeetups
    },
    loading () {
      return this.$store.getters.loading
    },
    userIsAuthenticated () {
      return this.$store.getters.user !== null && this.$store.getters.user !== undefined
    }
  },
  methods: {
    onLoadMeetup (meetupId) {
      this.$router.push({name: 'meetup', params: {id: meetupId}})
    }
  }
}
</script>

<style scoped>
  .title {
    position: absolute;
    bottom: 50px;
    left: 50%;
    transform: translate(-50%, 0);
    padding: 5px 15px;
    background-color: rgba(0,0,0,.5);
    color: #fff;
    border-top-right-radius: 5px;
    border-top-left-radius: 5px;
  }
</style>
