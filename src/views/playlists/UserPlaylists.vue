<template>
  <div class="user-playlists">
    <h2>My Playlists</h2>
    <div v-if="playlists">
      <ListView :playlists="playlists" />
    </div>
    <router-link :to="{ name: 'CreatePlaylist' }" class="btn">Create a Playlist</router-link>
  </div>
</template>

<script>
import getCollection from '@/composables/getCollection'
import getUser from '@/composables/getUser'
import ListView from '@/components/ListView.vue'

export default {
  components: { ListView },
  setup() {
    const { user } = getUser()
    const { documents: playlists } = getCollection(
      'playlists',
      ['userId', '==', user.value.uid] 
    )

    console.log(playlists)

    return { playlists }
  }
}
</script>

<style scoped>
h2 {
  margin-bottom: 2em;
}

</style>