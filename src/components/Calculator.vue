<script>
export default {
    data() {
        return {
            currentInput: '',
            prevInput: null,
            operator: null,
            presentValue: 0,
            buttons: ["C", "%", "/", "*", 7, 8, 9, "-", 4, 5, 6, "+", 1, 2, 3, 0, ".", "="]
        }
    },
    methods: {
        handleCalc(num) {

            if (!isNaN(num) || num === ".") {
                this.currentInput += num + '';
            }
            if (num === "C") {
                this.currentInput = '';
            }
            if (num === "%") {
                this.operator = "%"
                this.prevInput = this.currentInput;
                this.currentInput = '';
            }
            if (['/', '*', '-', '+',].includes(num)) {
                this.operator = num;
                this.prevInput = this.currentInput;
                this.currentInput = '';
            }
            if (num === "=") {
                this.currentInput = eval(
                    this.prevInput + this.operator + this.currentInput
                )

                if (this.operator === "%") {
                    this.currentInput = eval(
                        this.prevInput + "/" + "100" + "*" + this.currentInput
                    )
                    // this.currentInput = eval(
                    //     this.presentValue + "*" + this.currentInput
                    // )

                    // this.currentInput = "";
                    alert(this.currentInput)
                }
            }



        }
    },
}

</script>

<template>
    <div class="container">
        <div class="calc_div">
            <div class="display">{{ currentInput || 0 }}</div>
            <div class="btns">
                <button v-for="btnNum in buttons" class="numBtns"
                    :class="{ 'green': ['C', '%', '/', '*', '-', '+'].includes(btnNum) }" @click="handleCalc(btnNum)">{{
                        btnNum }}</button>
            </div>
        </div>
    </div>
</template>

<style>
.calc_div {
    width: 400px;
    height: 600px;
    background-color: #fff;
    box-sizing: border-box;
    padding: 10px;
}

.display {
    widows: 100%;
    border: 1.2px solid rgb(4, 19, 38);
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    padding: 0 10px;
    font-size: 22px;
}

.btns {
    /* border: 1px solid red; */
    widows: 100%;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: space-between;
    margin-top: 10px;
    /* height: 100%; */
}

.numBtns {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 90px;
    height: 90px;
    background-color: aliceblue;
    margin-bottom: 7px;
    border: 1px solid #00000098;
    background-color: #fff;
    font-size: 23px;
    cursor: pointer;
}

.numBtns:hover {
    background-color: rgb(195, 203, 210);
}

.numBtns:last-child {
    flex-grow: 1;
    margin-left: 7px;
    background-color: rgb(2, 19, 107);
    color: #fff;
    font-size: 50px;
    /* widows: 100px; */
}

.green {
    background-color: rgba(3, 115, 3, 0.77);
    color: #fff;
}
</style>