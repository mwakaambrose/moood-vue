<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/thinking.png" width="30%" height="60%">
    <Splash title="Moood.."/>
    <div style="margin-top: 80px;">
      <sui-grid :columns="8">
        <template v-for="(mood, index) in usermoods">
          <!-- show only up to 8 columns to match grid -->
          <sui-grid-column v-if="index < 8" v-bind:key="index">
            <Mood :author="mood.author"
                :mood="mood.mood"/>
          </sui-grid-column>
        </template>
      </sui-grid>
    </div>
    <div style="margin-top: 80px;">
      <sui-button @click.native="toggle"
        icon="heart"
        content="Go ahead, complain. Whats on your mind? Click me now.">
        <a is="sui-label" slot="label" basic>2,048</a>
      </sui-button>
      <sui-modal v-model="open">
        <sui-modal-header>Oh, not a complain, luck duck!</sui-modal-header>
        <sui-modal-content>
          <sui-modal-description>
            <sui-form>
              <sui-form-field :required="true">
                <label>Your handle</label>
                <input placeholder="@anonymous" v-model="userhandle">
                <small v-if="userhandleError">You need to provide a handle, if not, use <code>@anonymous</code></small>
              </sui-form-field>
              <sui-form-field :required="true">
                <label>What on your mind?</label>
                <textarea v-model="usermood"></textarea>
                <small v-if="usermoodError">You need to tell us whats on your mind, damn it!</small>
              </sui-form-field>
            </sui-form>
          </sui-modal-description>
        </sui-modal-content>
        <sui-modal-actions>
          <sui-button positive @click.native="publishMood"
            :primary="true">
            Publish it
          </sui-button>
        </sui-modal-actions>
      </sui-modal>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Splash from '@/components/Splash.vue'
import Mood from '@/components/Mood.vue'

import axios from 'axios'

// Fecth last 8
// Production
const api = 'http://api.moood.trustfinity.ltd/moods-limited-eight'
//add new moood
const api_add_moood = 'http://api.moood.trustfinity.ltd/moods'
// Test
// const api = 'http://localhost:3000/moods-limited-eight'

export default {
  name: 'home',
  components: {
    Splash,
    Mood
  },
  data() {
    return {
      open: false,
      userhandle: '',
      usermood: '',
      usermoods: [],
      isPublishing: false,
      userhandleError: false,
      usermoodError: false,
    };
  },
  methods: {
    toggle() {
      this.open = !this.open;
    },
    publishMood(){
      if (this.userhandle.length < 3) {
        this.userhandleError = true
        return
      }

      if (this.usermood.length == 0) {
        this.usermoodError = true
        return
      }

      axios.post(api_add_moood, {
        author: this.userhandle,
        mood: this.usermood
      }).then((response) => {
        console.log(response.data)
        // Add at the beginning if the array
        this.usermoods.unshift(response.data)
      }).catch(error => console.log("Nigga you fucked up somewhere" + error));

      this.open = !this.open
      this.usermoodError = false
      this.userhandleError = false
    },
    fetchLast8() {
      axios.get(api).then(({ data }) => {
        if (data.length) {
          this.usermoods = data;
          console.log(data)
        } else {
          console.log('We do not have data at the moment')
        }
      }).then((p) => {
        console.log(p)
      });
    },
  },

  created() {
    this.fetchLast8()
  }
}
</script>
