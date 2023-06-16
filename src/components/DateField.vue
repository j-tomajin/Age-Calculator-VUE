<template>
    <div class="">
        <form
            class="form"
        >
            <div :class="[valid ? '' : 'error', 'input-field']">
                <label 
                    for=""
                    class="label">DAY</label>
                <input 
                    type="number"
                    name="day"
                    v-model="day"
                    placeholder="DD"
                    class="input">
                <p v-if="!valid">Must be valid date</p>
            </div>
            <div class="input-field">
                <label 
                    for=""
                    class="label">MONTH</label>
                <input 
                    type="text"
                    name="month"
                    v-model="month"
                    placeholder="MM"
                    class="input">
            </div>
            <div class="input-field">
                <label 
                    for=""
                    class="label">YEAR</label>
                <input 
                    type="number"
                    name="year"
                    v-model="year"
                    placeholder="YYYY"
                    class="input">
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

    export default {
        name: 'DateField',
        components: {
            Button,
        },
        data: function() {
            return {
                day: '',
                month: '',
                year: '',
                valid: true,
                icon: icon
            }
        },
        methods: {
            checkDate: function() {
                if(!this.day || !this.month || !this.year) {
                    this.valid = false
                } else {
                    this.valid = true
                }
            }
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
    }

    .error {

        .label {
            color: var(--clr-primary-l-red);
        }

        .input {
            border-color: var(--clr-primary-l-red);
        }
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
    }

    .line {
        position: relative;
        background-color: white;
        height: 1px;

        // temp margin
        margin-block: 40px;
    }
</style>