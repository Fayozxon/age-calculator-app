<template>
    <form class="form-box" :class="{'error': !isFormValid}" @submit.prevent>
        <label class="error">Day
            <input
                type="number"
                placeholder="DD"
                :value="dateDay"
                @input="dateDay = $event.target.value"
                min="1"
            />
            <p class="error-msg">Must be a valid date</p>
        </label>
        <label>Month
            <input
                type="number"
                placeholder="MM"
                :value="dateMonth"
                @input="dateMonth = $event.target.value"
                min="1"
            />
        </label>
        <label>Year
            <input
                type="number"
                placeholder="YYYY"
                :value="dateYear"
                @input="dateYear = $event.target.value"
                min="1"
            />
        </label>
    </form>
    <div class="btn-box">
        <span class="line"></span>
        <button
            class="btn"
            @click="sendTheDate"
        >
            <img src="../assets/images/icon-arrow.svg" alt="">
        </button>
    </div>
        
</template>

<script>
export default {
    emits: ['calcTheAge'],
    data() {
        return {
            dateDay: '',
            dateMonth: '',
            dateYear: '',
            isFormValid: true
        }
    },
    computed: {
        isInputsValid() {
            let currentYear = new Date().getFullYear(),
                days31 = [1,3,5,7,8,10,12],
                days30 = [4,6,9,11];

            if (this.dateDay && this.dateMonth && this.dateYear) {
                if (this.dateYear <= currentYear && this.dateMonth <= 12 && this.dateYear > 0 && this.dateMonth > 0 && this.dateDay > 0) {
                    if (days31.includes(Number(this.dateMonth))) {
                        return this.dateDay <= 31;
                    } else if (days30.includes(Number(this.dateMonth))) {
                        return this.dateDay <= 30;
                    } else {
                        return this.dateDay <= 29;
                    }
                }
            }
            return false;
        }
    },
    methods: {
        sendTheDate() {
            if (this.isInputsValid) {
                let dob = `${this.dateYear}-${this.dateMonth}-${this.dateDay}`;
                this.$emit('calcTheAge', dob);
            } else {
                this.isFormValid = false;
            }
        }
    },
    watch: {
        dateDay() {
            if (this.isInputsValid) {
                this.isFormValid = true;
            }
        },
        dateMonth() {
            if (this.isInputsValid) {
                this.isFormValid = true;
            }
        },
        dateYear() {
            if (this.isInputsValid) {
                this.isFormValid = true;
            }
        }
    }
}
</script>

<style scoped>
/* Form Box Styles */
.form-box {
    display: flex;
}
.form-box label {
    position: relative;
    display: flex;
    flex-direction: column;
    padding-right: 30px;
    text-transform: uppercase;
    font-weight: 700;
    letter-spacing: 2.5px;
    color: var(--clr-grey);
}
/* Input Styles */
.form-box input {
    width: 160px;
    outline: none;
    border: 1px solid var(--clr-lt-grey);
    border-radius: 7px;
    padding: 10px 20px;
    margin-top: 5px;
    font-size: 32px;
    font-weight: 700;
    transition: all 0.23s;
    caret-color: var(--clr-purple);
}
.form-box input:focus {
    border-color: var(--clr-purple);
}
/* Error Message Styles */
.form-box.error label {
    color: var(--clr-red);
}
.form-box.error input, .form-box.error input:focus {
    border-color: var(--clr-red);
}
.error-msg {
    width: 200%;
    position: absolute;
    bottom: -25px;
    font-size: 14px;
    text-transform: initial;
    letter-spacing: initial;
    font-weight: 400;
    font-style: italic;
    color: var(--clr-red);
    display: none;
    word-wrap: normal;
}
.form-box.error .error-msg {
    display: block;
}
/* Button Styles */
.btn-box {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 130px;
    padding-top: 20px;
}
.btn {
    position: absolute;
    right: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 80px;
    height: 80px;
    border-radius: 50%;
    border: none;
    cursor: pointer;
    background: var(--clr-purple);
    transition: all 0.23s;
}
.btn img {
    width: 40px;
}
.btn:focus {
    background: var(--clr-dark);
}
.line {
    width: 100%;
    display: block;
    flex-shrink: 1;
    height: 1px;
    background: var(--clr-lt-grey);
}
/* RWD Styles */
@media only screen and (max-width: 820px) {
    /* Form */
    .form-box label {
        font-size: 14px;
    }
    .form-box input {
        width: 105px;
        font-size: 22px;
    }
    /* Button */
    .btn-box .btn {
        right: unset;
        left: 50%;
        transform: translateX(-50%);
    }
}
</style>