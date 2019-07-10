<template>
    <tbody>
        <month v-bind:key="i" v-for="i in 12" v-bind:month='i'/>
    </tbody>
</template>

<script>
import month from "./month.vue";
export default {
    name: "allMonth",
    components: {
        month
    },

    props: {
        year: Number

        //monthDayCount: JAN: 31, FEB: 28 |>4 29, MAR: 31, APR: 30, MAY: 31, JUN: 30, JUL: 31
        //               AUG: 31, SEP: 30, OCT: 31, NOV: 30, DEC: 31
    }
}
</script>

<style>

</style>


