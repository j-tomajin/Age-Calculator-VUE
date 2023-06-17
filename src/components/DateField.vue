<template>
    <div class="">
        <form
            class="form"
        >
            <!-- DAY -->
            <div :class="[(validDay) ? '' : 'error', 'input-field', (withinDay) ? '' : 'error', 'input-field']">
                <label 
                    for="day"
                    class="label">DAY</label>
                <input 
                    type="number"
                    name="day"
                    v-model="day"
                    placeholder="DD"
                    class="input"
                    id="day">
                
                <small class="error-date">
                    <!-- When input field is blank  -->
                    <span v-if="!validDay">This field is required</span>
                    <!-- When day is greater than 31 -->
                    <span v-else-if="!withinDay">Must be a valid date</span>
                </small>
            </div>

            <!-- MONTH -->
            <div :class="[(validMonth) ? '' : 'error', 'input-field', (withinMonth) ? '' : 'error', 'input-field']">
                <label 
                    for="month"
                    class="label">MONTH</label>
                <input 
                    type="text"
                    name="month"
                    v-model="month"
                    placeholder="MM"
                    class="input"
                    id="month">

                <small class="error-date">
                    <!-- When input field is blank  -->
                    <span v-if="!validMonth">This field is required</span>
                    <!-- When day is greater than 31 -->
                    <span v-else-if="!withinMonth">Must be a valid date</span>
                </small>
            </div>

            <!-- YEAR -->
            <div :class="[(withinYear) ? '' : 'error', 'input-field', (validYear) ? '' : 'error', 'input-field']">
                <label 
                    for="year"
                    class="label">YEAR</label>
                <input 
                    type="number"
                    name="year"
                    v-model="year"
                    placeholder="YYYY"
                    class="input"
                    id="year"
                    required>
                
                <small class="error-date">

                    <span v-if="!withinYear">
                        Must be in the past
                    </span>
                
                <!-- When input field is blank  -->
                    <span v-else-if="!validYear">
                        This field is required
                    </span>
                </small>
            </div>
        </form>

        <div class="line">
            <Button 
                text="" 
                :src="icon" 
                class="btn-cta"
                @btn-click="checkDate" />
        </div>
    </div>
</template>

<script>
    import Button from './Button.vue';
    import icon from '../assets/images/icon-arrow.svg'
import { withMemo } from 'vue';

    export default {
        name: 'DateField',
        components: {
            Button,
        },
        props: {
            isValidYear: Boolean
        },
        data: function() {
            return {
                day: '',
                month: '',
                year: '',
                icon: icon,
                validDay: true,
                validMonth: true,
                validYear: true,

                withinDay: true,
                withinMonth: true,
                withinYear: true,
            }
        },
        methods: {
            checkDate: function() {
                // check if the day and month are valid
                let maxDay = 31
                
                const date = new Date()
                const yearNow = date.getFullYear()
                
                if(this.month == 1 || this.month == 3 || this.month == 5 || this.month == 7 || this.month == 8 || this.month == 10 || this.month == 12) {
                    maxDay = 30
                } 
                if(this.month == 2) {
                    maxDay = 28
                    
                    if((0 == this.year % 4) && (0 != this.year % 100) || (0 == this.year % 400)) {
                        maxDay = 29
                    }
                }

                if(this.month > 12) {
                    this.withinMonth = false
                    this.validMonth = true
                } else if(!this.month) {
                    this.withinMonth = true
                    this.validMonth = false
                } else {
                    this.withinMonth = true
                    this.validMonth = true
                }

                if(this.year > yearNow) {
                    this.withinYear = false
                    this.validYear = true
                } else if(!this.year) {
                    this.withinYear = true
                    this.validYear = false
                } else {
                    this.validYear = true
                    this.withinYear = true
                }

                if(this.day > maxDay) {
                    this.withinDay = false
                    this.validDay = true
                } else if(!this.day) {
                    this.withinDay = true
                    this.validDay = false
                } else {
                    this.withinDay = true
                    this.validDay = true
                }

                if(this.validDay && this.validMonth && this.validYear && this.withinDay && this.withinMonth && this.withinYear) {
                    this.$emit('check-date', this.day, this.month, this.year)
                }
                
            },
        },
    }
</script>

<style lang="scss" scoped>
    @use '../assets/scss/utilities' as *;

    .form {
        display: flex;
        align-items: center;
        justify-content: start;
        gap: clampf(16, 780, 24);
    }

    .input-field {
        display: grid;
        grid-template-columns: 1;
        gap: rem(8);

        position: relative;
    }

    .error {

        .label {
            color: var(--clr-primary-l-red);
        }
        
        .input {
            border-color: var(--clr-primary-l-red);
        }
    }
    
    .error-date {
        color: var(--clr-primary-l-red);

        position: absolute;
        bottom: rem(-24);
        left: 0;
    }

    .label {
        font-size: clampf(12, 780, 14);
        letter-spacing: 3px;
        color: var(--clr-neutral-s-grey);
    }

    .input {
        outline: 0;
        border: 1px solid var(--clr-neutral-l-grey);
        width: clampf(90, 780, 160);
        padding: rem(8) rem(10);
        border-radius: rem(8);

        &::-webkit-outer-spin-button,
        &::-webkit-inner-spin-button {
            -webkit-appearance: none;
        }

        &:focus {
            border-color: var(--clr-neutral-s-grey);
        }

        &::placeholder {
            color: var(--clr-neutral-s-grey);
        }
    }

    .btn-cta {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);

        background-color: var(--clr-primary-purple);
        padding: rem(12);
        width: clampf(50, 780, 70);
        border-radius: rem(50);
        transition: all 300ms ease-out;

        &:hover {
            background-color: var(--clr-neutral-offblack);
        }

        @include breakpointMin(medium-screen) {
            left: 100%;
        }
    }

    .line {
        position: relative;
        background-color: var(--clr-neutral-l-grey);
        height: clampf(1, 780, 2);
        margin-block: clampf(40, 780, 80);
    }
</style>