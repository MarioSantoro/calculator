<template>
    <div class="answer">{{ answer }}</div>
    <div class="output">
        <h1>{{ logList + userInput }}</h1>
    </div>
    <div class="container d-flex flex-wrap justify-content-center">
        <div class="row">
            <div class="col-12">
                <button @click="clear">C</button>
                <button @click="sign">+/-</button>
                <button>%</button>
                <button @click="divide">/</button>
            </div>
            <div class="col-12">
                <button @click="append('7')">7</button>
                <button @click="append('8')">8</button>
                <button @click="append('9')">9</button>
                <button @click="times">*</button>
            </div>
            <div class="col-12">
                <button @click="append('4')">4</button>
                <button @click="append('5')">5</button>
                <button @click="append('6')">6</button>
                <button @click="minus">-</button>
            </div>
            <div class="col-12">
                <button @click="append('1')">1</button>
                <button @click="append('2')">2</button>
                <button @click="append('3')">3</button>
                <button @click="plus">+</button>
            </div>
            <div class="col-12">
                <button @click="append('0')">0</button>
                <button @click="equal">=</button>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            answer: '',
            logList: '',
            userInput: '',
            operator: '',
            clicked: true,
        }
    },

    methods: {
        append(number) {
            if (this.clicked) {
                this.userInput = "";
                this.clicked = false;
            }
            this.userInput = `${this.userInput}${number}`;
        },
        addtoLog(operator) {
            if (this.clicked == false) {
                this.logList += `${this.userInput} ${operator} `;
                this.userInput = "";
                this.clicked = true;
            }
        },
        sign() {
            if (this.userInput != "") {
                this.userInput =
                    this.userInput.charAt(0) === "-"
                        ? this.userInput.slice(1)
                        : `-${this.userInput}`;
            }
        },

        divide() {
            this.addtoLog("/");
        },

        times() {
            this.addtoLog("*");
        },

        minus() {
            this.addtoLog("-");
        },

        plus() {
            this.addtoLog("+");
        },

        equal() {
            if (this.clicked == false) {
                this.answer = eval(this.logList + this.userInput);
            } else {
                this.answer = "WHAT?!!";
            }
        },

        clear() {
            this.userInput = "";
            this.logList = "";
            this.answer = "";
            this.clicked = false;
        }
    }
}
</script>
<style lang="scss" scoped>
div.button {
    width: calc(100% / 3);
    display: flex;
    align-items: center;
    justify-content: center;

    button {
        width: 100%;
    }
}
</style>