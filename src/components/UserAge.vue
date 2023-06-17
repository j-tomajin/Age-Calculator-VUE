<template>
    <div class="age-field">
        <!-- YEAR -->
        <h1 class="date">
            <span 
                v-if="yearsOld == 0" 
                class="primary-text">
            --
            </span>

            <span 
                v-else 
                class="primary-text">
            {{ yearsOld }}
            </span>
            years
        </h1>

        <!-- MONTH -->
        <h1 class="date">
            <span 
                v-if="monthsOld == 0" 
                class="primary-text">
            --
            </span>

            <span 
                v-else 
                class="primary-text">
            {{ monthsOld }}
            </span>
            months
        </h1>

        <!-- DAY -->
        <h1 class="date">
            <span 
                v-if="daysOld == 0" 
                class="primary-text">
            --
            </span>

            <span 
                v-else 
                class="primary-text">
            {{ daysOld }}
            </span>
            days
        </h1>
    </div>
</template>

<script>
    export default {
        name: 'UserAge',
        props: {
            yearsOld: Number,
            monthsOld: Number,
            daysOld: Number,
        }
    }
</script>

<style lang="scss" scoped>
    @use '../assets/scss/utilities/' as *;

    .date {
        font-size: clampf(44, 780, 88);
        color: var(--clr-neutral-offblack);
        font-weight: 800;
        font-style: italic;
    }

    .primary-text {
        color: var(--clr-primary-purple);
    }
</style>