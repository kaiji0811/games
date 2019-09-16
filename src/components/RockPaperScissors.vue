<template>
    <div class="Board">
        <div class="Result">
            <template v-if="isWinner">
                <p>enemy's hand is {{ enemy }}.</p>
                <p>your hand is {{ player }}.</p>
                <p>Winner is : {{ isWinner }}!!</p>
            </template>
        </div>
        <div class="Buttons">
            <div class="Buttons__hands">
                <template v-if="!isWinner">
                    <button @click="handleClickButtons(0)">Rock</button>
                    <button @click="handleClickButtons(1)">Paper</button>
                    <button @click="handleClickButtons(2)">Scissors</button>
                </template>
            </div>
            <div class="Buttons__go">
                <template v-if="isWinner">
                    <button @click="init()">Retry!</button>
                </template>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class RockPaperScissors extends Vue {
    private enemy: string = '';
    private player: string = '';
    private table: string[] = ['rock', 'paper', 'scissors'];
    public created(): void {
        this.init();
    }
    public init(): void {
        this.enemy = '';
        this.player = '';
        const shuffle: number = Math.ceil(Math.random() * 3) - 1;
        this.enemy = this.table[shuffle];
    }
    public handleClickButtons(select: number): void {
        this.player = this.table[select];
    }
    get isWinner(): string {
        let result: string = '';
        if (
            (this.player === 'rock' && this.enemy === 'rock')
            || (this.player === 'paper' && this.enemy === 'paper')
            || (this.player === 'scissors' && this.enemy === 'scissors')
        ) {
            result = 'not yet';
        } else if (
            (this.player === 'rock' && this.enemy === 'scissors')
            || (this.player === 'paper' && this.enemy === 'rock')
            || (this.player === 'scissors' && this.enemy === 'paper')
        ) {
            result = 'player';
        } else if (
            (this.player === 'rock' && this.enemy === 'paper')
            || (this.player === 'paper' && this.enemy === 'scissors')
            || (this.player === 'scissors' && this.enemy === 'rock')
        ) {
            result = 'enemy';
        }
        return result;
    }
}
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

