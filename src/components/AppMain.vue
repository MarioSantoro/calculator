<template>
    <div class="phone">
        <div class="volume up"></div>
        <div class="volume down"></div>
        <div class="on-off"></div>
        <div class="header d-flex justify-content-between">
            <div class="left d-flex align-items-center">
                <div class="time d-flex align-items-center">
                    <p class="text-white m-0">{{ currentTime }}</p>
                </div>
                <div class="notify">
                    <i class="fa-brands fa-discord fa-xs text-white ms-1"></i>
                    <i class="fa-solid fa-cloud fa-xs text-white ms-1"></i>
                    <i class="fa-brands fa-twitch fa-xs text-white ms-1"></i>
                </div>
            </div>

            <div class="center">
                <div class="concentric-circle outer-housing">
                    <div class="concentric-circle silver-ring">
                        <div class="concentric-circle inner-housing">
                            <div class="concentric-circle outer-ribbing">
                                <div class="concentric-circle ribbing">
                                    <div class="concentric-circle ribbing">
                                        <div class="concentric-circle ribbing">
                                            <div class="concentric-circle ribbing">
                                                <div class="concentric-circle ribbing">
                                                    <div class="concentric-circle ribbing">
                                                        <div class="concentric-circle ribbing">
                                                            <div class="concentric-circle ribbing">
                                                                <div class="concentric-circle ribbing">
                                                                    <div class="concentric-circle ribbing">
                                                                        <div class="concentric-circle ribbing">
                                                                            <div class="concentric-circle aperture-housing">
                                                                                <div
                                                                                    class="concentric-circle small-lens-outer">
                                                                                    <div
                                                                                        class="concentric-circle small-lens-inner">
                                                                                        <div
                                                                                            class="concentric-circle tiny-lens-outer">
                                                                                            <div
                                                                                                class="concentric-circle tiny-lens-inner">
                                                                                                <div
                                                                                                    class="concentric-circle tiny-lens-inner">
                                                                                                    <div
                                                                                                        class="concentric-circle tiny-lens-inner">
                                                                                                    </div>
                                                                                                </div>
                                                                                            </div>
                                                                                        </div>
                                                                                    </div>
                                                                                </div>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="concentric-circle outer-lens">
                                <div class="shine"></div>
                            </div>
                        </div>
                    </div>
                    <div class="shadow"></div>
                </div>
            </div>

            <div class="right d-flex align-items-center">
                <i class="fa-solid fa-wifi fa-xs text-white me-1"></i>
                <i class="fa-solid fa-signal fa-xs text-white me-1"></i>
                <span class=" text-white me-1">9%</span>
                <div class="battery">
                    <div class="tap">
                    </div>
                    <div class="level">
                    </div>
                </div>
            </div>
        </div>
        <div class="output-general">
            <div class="output">
                <h4>{{ logList + userInput }}</h4>
            </div>
            <div class="answer">
                <h1>{{ answer }}</h1>
            </div>
        </div>
        <div class="container-fluid d-flex flex-wrap justify-content-center input">
            <div class="row">
                <div class="col-3">
                    <button class="clear" @click="clear">C</button>
                </div>
                <div class="col-3">
                    <button class="operator">()</button>
                </div>
                <div class="col-3">
                    <button class="operator">%</button>
                </div>
                <div class="col-3">
                    <button class="operator" @click="divide">/</button>
                </div>
            </div>
            <div class="row">
                <div class="col-3">
                    <button @click="append('7')">7</button>
                </div>
                <div class="col-3">
                    <button @click="append('8')">8</button>
                </div>
                <div class="col-3">
                    <button @click="append('9')">9</button>
                </div>
                <div class="col-3">
                    <button class="operator" @click="times">*</button>
                </div>
            </div>
            <div class="row">
                <div class="col-3">
                    <button @click="append('4')">4</button>
                </div>
                <div class="col-3">
                    <button @click="append('5')">5</button>
                </div>
                <div class="col-3">
                    <button @click="append('6')">6</button>
                </div>
                <div class="col-3">
                    <button class="operator" @click="minus">-</button>
                </div>
            </div>
            <div class="row">
                <div class="col-3">
                    <button @click="append('1')">1</button>
                </div>
                <div class="col-3">
                    <button @click="append('2')">2</button>
                </div>
                <div class="col-3">
                    <button @click="append('3')">3</button>
                </div>
                <div class="col-3">
                    <button class="operator" @click="plus">+</button>
                </div>
            </div>
            <div class="row">
                <div class="col-3">
                    <button @click="sign">+/-</button>
                </div>
                <div class="col-3">
                    <button @click="append('0')">0</button>
                </div>
                <div class="col-3">
                    <button>.</button>
                </div>
                <div class="col-3">
                    <button class="equals" @click="equal">=</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import { store } from '../store.js'
export default {
    data() {
        return {
            answer: '',
            logList: '',
            userInput: '',
            operator: '',
            clicked: true,
            equalClicked: false,
            store,
            currentTime: 0,
        }
    },

    methods: {
        append(number) {
            if (this.equalClicked) {
                this.clear();
                this.equalClicked = false;
            }
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
            this.equalClicked = true;
        },

        clear() {
            this.userInput = "";
            this.logList = "";
            this.answer = "";
            this.clicked = false;
        }
    },
    created() {
        setInterval(() => {
            let DateTime = new Date();
            this.currentTime = DateTime.getHours() + ":" + DateTime.getMinutes();
        }, 1000)
    }
}
</script>
<style lang="scss" scoped>
div.phone {
    width: 300px;
    height: 600px;
    border: 1px solid green;
    background-color: black;
    border-radius: 1rem;
    position: relative;

    div.volume {
        position: absolute;
        height: 50px;
        border-radius: 1rem;
        width: 5px;
        top: 60px;
        right: -3px;
        background-color: black;
    }

    div.input {
        margin-top: 20px;
        height: calc(100% / 2 - 35px);
    }

    div.output-general {
        height: calc(100% / 2 - 35px);
        display: flex;
        flex-direction: column;
        justify-content: end;
        border-bottom: 1px solid #ccc;
        color: white;
    }

    div.volume.down {
        position: absolute;
        height: 50px;
        border-radius: 1rem;
        width: 5px;
        top: 120px;
        right: -3px;
        background-color: black;
    }

    div.on-off {
        position: absolute;
        height: 35px;
        border-radius: 1rem;
        width: 5px;
        top: 200px;
        right: -3px;
        background-color: black;
    }

    div.header {
        font-size: .66rem;
        padding: .44rem .44rem;
        align-items: center;
    }

    div.time {
        margin-left: .55rem;
    }

    div.battery {
        height: 12px;
        width: 9px;
        margin-right: .55rem;
        border: 1px solid white;
        border-radius: .16rem;
        position: relative;

        div.tap {
            height: 3px;
            border-bottom: 1px solid black;
            border-left: 1px solid white;
            border-right: 1px solid white;
            border-top: 1px solid white;
            width: 5px;
            position: absolute;
            left: 15%;
            top: -3px;
            border-radius: .10rem;
        }

        div.level {
            background-color: red;
            height: 20%;
            width: 100%;
            position: absolute;
            bottom: 0;
        }
    }


    div.row {
        height: 50px;
        width: 100%;
    }

    div.col-3 {
        height: 50px;
        padding: 0;
        display: flex;
        justify-content: center;

        button {
            border-radius: 50%;
            height: 50px;
            width: 50px;
            border: none;
            background-color: rgb(29, 27, 27);
            color: white;
        }

        button.equals {
            background-color: rgb(43, 134, 43);
        }

        button.operator {
            color: rgb(43, 134, 43);
        }

        button.clear {
            color: orangered;
        }
    }


}

.concentric-circle {
    border-radius: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
}

.outer-housing {
    width: 20px;
    height: 20px;
    background: linear-gradient(0deg, rgb(80, 80, 80), rgb(0, 0, 0));
    border: 2px solid rgb(80, 80, 80);
}

.silver-ring {
    width: 96%;
    height: 96%;
    background: linear-gradient(45deg, rgb(200, 200, 200), rgb(100, 100, 100), rgb(200, 200, 200));
    box-shadow: 1px 1px rgb(240, 240, 240) inset;
}

.inner-housing {
    width: 97%;
    height: 97%;
    background: radial-gradient(ellipse at 70% 50%, rgb(80, 80, 80), rgb(40, 40, 40));
    box-shadow: 2px 2px rgb(210, 220, 220), 0 6px rgb(40, 40, 40) inset;
}

.outer-lens {
    width: 80%;
    height: 80%;
    background: linear-gradient(0deg, rgba(80, 200, 140, 0.2), rgba(120, 80, 200, 0.2)), radial-gradient(circle at 10% 10%, rgba(40, 220, 40, 0.8) 0%, rgba(80, 200, 140, 0.6) 10%, transparent 40%), radial-gradient(circle at 0% 40%, rgba(120, 80, 200, 0.8) 0%, rgba(120, 80, 200, 0.6) 10%, transparent 30%), radial-gradient(circle at 90% 90%, rgba(40, 100, 200, 0.4) 0%, rgba(40, 100, 200, 0.2) 10%, transparent 20%);
    z-index: 100;
}

.outer-ribbing {
    width: 75%;
    height: 75%;
    background: rgb(40, 40, 40);
    box-shadow: 0 4px 4px rgb(0, 0, 0, 0.4) inset;
    z-index: 1;
}

.ribbing {
    border: 1px solid rgb(10, 10, 10);
    background: rgb(60, 60, 60);
    width: calc(100% - 8px);
    height: calc(100% - 8px);
    z-index: 1;
}

.aperture-housing {
    width: 100%;
    height: 100%;
    background: rgb(80, 80, 80);
    box-shadow: 0 -10px 10px rgb(255, 255, 255, 0.1) inset
}

.small-lens-outer {
    width: 85%;
    height: 85%;
    background: linear-gradient(0deg, rgb(30, 30, 30), rgb(0, 0, 0));
    box-shadow: 0 2px 0px rgb(255, 255, 255, 0.4)
}

.small-lens-inner {
    background: rgb(0, 0, 0);
    width: 70%;
    height: 70%;
    background: conic-gradient(rgba(0, 0, 0, 0), rgba(0, 0, 0, 0), rgba(80, 180, 200, 0.6), rgba(100, 240, 100, 0.6), rgba(0, 0, 0, 0), rgba(0, 0, 0, 0), rgba(0, 0, 0, 0), rgba(200, 200, 140, 0.3), rgba(200, 240, 100, 0.2), rgba(0, 0, 0, 0), rgba(0, 0, 0, 0)), radial-gradient(circle at 10% 10%, rgba(255, 220, 220, 0.8) 0%, rgba(220, 120, 100, 0.6) 20%, transparent 40%);
    box-shadow: 0 1px 1px 1px rgb(255, 255, 255, 0.4)
}

.tiny-lens-outer {
    width: 70%;
    height: 70%;
}

.tiny-lens-inner {
    width: 60%;
    height: 60%;
    border: 2px solid rgb(0, 0, 0, 0.6);
    filter: blur(1px)
}

.shine {
    position: absolute;
    background: linear-gradient(0deg, rgba(255, 255, 255, 0), rgba(255, 255, 255, 0.5));
    width: 7px;
    height: 4px;
    top: 1.6px;
    left: 0.8px;
    border-radius: 100% 100% 0 0;
    transform: rotate(-40deg);
}

.shadow {
    width: 16px;
    height: 10px;
    background: rgba(0, 0, 0, 0.7);
    position: absolute;
    bottom: -2px;
    z-index: -1;
    border-radius: 100%;
    filter: blur(40px)
}
</style>


