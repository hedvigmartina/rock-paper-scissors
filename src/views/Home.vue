<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h3>Choose Your option to start playing</h3>
    <form @submit.prevent="sendUserSelection">
      <radio-button
        v-for="(choice, index) in choices"
        :key="index"
        :value="choice"
        required
        name="choice"
      />
      <the-button
        type="submit"
        text="Play!"
      />
    </form>
    <result
      v-if="showResult"
      :result="isUserWinner"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import { mapGetters, mapActions } from 'vuex';
import RadioButton from '@/components/RadioButton.vue';
import TheButton from '@/components/TheButton.vue';
import Result from '@/components/Result.vue';

export default {
  name: 'home',
  components: {
    RadioButton,
    TheButton,
    Result,
  },
  computed: {
    ...mapGetters([
      'choices',
      'showResult',
      'isUserWinner',
    ]),
    //    choices() {
    //      return this.$store.getters.choices;
    //   },
    //    showResult() {
    //      return this.$store.getters.showResult;
    //    },
    //    isUserWinner() {
    //      return this.$store.getters.isUserWinner;
    //    },
  },
  methods: {
    ...mapActions([
      'playGame',
    ]),
    sendUserSelection() {
      this.playGame(this.$el.querySelector('.radio:checked').value);
    },
  },
};
</script>
