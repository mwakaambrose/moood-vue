<template>
  <div class="moods">
    <h1>moods from all over this miserable earth</h1>
    <sui-grid :columns="8">
      <template v-for="(mood, $index) in moods">
        <sui-grid-column style="margin-top: 30px;" v-bind:key="mood.id">
          <MoodHolder :author="mood.author"
              :key="$index"
              :mood="mood.mood"/>
        </sui-grid-column>
      </template>
    </sui-grid>
    <infinite-loading @infinite="infiniteHandler"></infinite-loading>
  </div>
</template>
<script>

import InfiniteLoading from 'vue-infinite-loading';
import axios from 'axios';
import MoodHolder from '@/components/Mood.vue'

// Local
// const api = 'http://localhost:3000/moods';
// Production
const api = 'http://api.moood.trustfinity.ltd/moods';

export default {
  components: {
    InfiniteLoading,
    MoodHolder,
  },
  data() {
    return {
      page: 1,
      moods: [],
    };
  },
  methods: {
    infiniteHandler($state) {
      axios.get(api).then(({ data }) => {
        if (data.length) {
          this.page += 1;
          // this.moods.push(...data.hits);
          this.moods = data;
          $state.loaded();
        } else {
          $state.complete();
        }
      });
    },
  },
}
</script>
<style scoped>
  h1 {
    margin-top: 100px;
    margin-bottom: 100px;
  }
  .moods {
    padding-top: 60px;
  }
</style>
