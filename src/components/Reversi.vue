<template>
    <ul class="Board">
        <li v-for="i in BOARD_NUM" :key="i">
            <div class="Stone" :class="board[i].stone"  @click="changeStone(i)"></div>
        </li>
    </ul>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class Reversi extends Vue {
    private BOARD_ROW: number = 8;
    private BOARD_COLUMN: number = 8;
    private BOARD_NUM: number = this.BOARD_ROW * this.BOARD_COLUMN;
    private board: any = [];
    private created(): void {
        this.init();
    }
    private init(): void {
        this.initialBoardSetting();
    }
    private initialBoardSetting(): void {
        const obj: any = [];
        for (let i = 0, len = this.BOARD_NUM; i <= len; i++) {
            obj[i] = {
                id: i,
                stone: this.isInitialStone(i),
            };
        }
        this.board = [...obj];
    }
    private changeStone(i: number): void {
        if (this.board[i].stone !== '') {
            return;
        }
        // 石を置くことのできる条件：
        // 1.　縦、横、斜めのラインにひっくり返す事のできる石が存在すること
        // 2.　縦、横、斜めの隣接するセルに石が置かれていること
        // 3. 石が置かれていないこと
        if (!this.isArroundCellEmpty(i)) {
            alert('そこはおけん！');
            return;
        }
    }
    get isInitialStone(): any {
        return (i: number) => {
            if (
                i === (this.BOARD_NUM / 2) - (this.BOARD_ROW / 2)
                || i === (this.BOARD_NUM / 2) + (this.BOARD_ROW / 2 + 1)
            ) {
                return 'white';
            } else if (
                i === (this.BOARD_NUM / 2) - (this.BOARD_ROW / 2 - 1)
                || i === (this.BOARD_NUM / 2) + (this.BOARD_ROW / 2)
            ) {
                return 'black';
            } else {
                return '';
            }
        };
    }
    get isArroundCellEmpty(): any {
        return (i: number) => {
            if (
                // left
                this.board[i - 1].stone === ''
                // right
                && this.board[i + 1].stone === ''
                // up
                && this.board[i - this.BOARD_ROW].stone === ''
                // down
                && this.board[i + this.BOARD_ROW].stone === ''
                // up left
                && this.board[i - this.BOARD_ROW - 1].stone === ''
                // up right
                && this.board[i - this.BOARD_ROW + 1].stone === ''
                // down left
                && this.board[i + this.BOARD_ROW - 1].stone === ''
                // down right
                && this.board[i + this.BOARD_ROW + 1].stone === ''
            ) {
                return false;
            } else {
                return true;
            }
        };
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.Board {
    display: flex;
    flex-wrap: wrap;
    width: 800px;
    height: 800px;
    margin: 0 auto;

    > li {
        width: 12.5%;
        display: flex;
        align-items: center;
        justify-content: center;
        border: 1px solid #ccc;
        border-collapse: collapse;
    }
}
.Stone {
    padding: 16px;
    &.white {
        border: 1px solid #ccc;
        border-radius: 100%;
        background-color: #fff;
        box-shadow: 0 0 6px #ccc;
    }
    &.black {
        border: 1px solid #333;
        border-radius: 100%;
        background-color: #333;
        box-shadow: 0 0 6px #ccc;
    }
}
</style>

