<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/thinking.png" width="30%" height="60%">
    <Splash title="Moood.."/>
    <div style="margin-top: 80px;">
      <sui-grid :columns="8">
        <template v-for="(i, index) in [1,3,2,5,4, 5, 6, 7]">
          <sui-grid-column>
            <Mood author="mwkams"
                mood="If something is especially relatable, one might say 'Big Mood.' This implies that your whole being is one and the same with whatever you are commenting on."/>
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
              <sui-form-field required="true">
                <label>Your handle</label>
                <input placeholder="@anonymous" v-model="userhandle">
              </sui-form-field>
              <sui-form-field required="true">
                <label>What on your mind?</label>
                <textarea v-model="usermood"></textarea>
              </sui-form-field>
            </sui-form>
          </sui-modal-description>
        </sui-modal-content>
        <sui-modal-actions>
          <sui-button positive @click.native="publishMood"
            primary="true">
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
      isPublishing: false
    };
  },
  methods: {
    toggle() {
      this.open = !this.open;
    },
    publishMood(){
      this.open = !this.open;
    }
  },
}
</script>
