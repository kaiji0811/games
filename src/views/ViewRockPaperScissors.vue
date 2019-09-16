<template>
    <div class="Board">
        <h1>Rock Paper Scissors!</h1>
        <RockPaperScissors />
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import RockPaperScissors from '@/components/RockPaperScissors.vue';

@Component({
  components: {
    RockPaperScissors,
  },
})
export default class ViewRockPaperScissors extends Vue {}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.Result {
    font-size: 22px;
    font-weight: bold;
}
</style>
