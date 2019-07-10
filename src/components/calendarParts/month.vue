<template>
    <tr>
        <calendarBlock type="month" v-bind:value="monthList[month-1]"/>
        
        <calendarBlock type="void" v-bind:key="i" v-for="i in 7" v-bind:value='i'/>
        <calendarBlock type="space"/>
        <calendarBlock type="day" v-bind:key="i" v-for="i in 7" v-bind:value='i'/>
        <calendarBlock type="space"/>
        <calendarBlock type="void" v-bind:key="i" v-for="i in 7" v-bind:value='i'/>
        <calendarBlock type="space"/>
        <calendarBlock type="day" v-bind:key="i" v-for="i in 7" v-bind:value='i'/>
        <calendarBlock type="space"/>
        <calendarBlock type="day" v-bind:key="i" v-for="i in 7" v-bind:value='i'/>
    </tr>    
</template>

<script>
import calendarBlock from './calendarBlock.vue';

export default {
    name: "month",
    props: {
        month: String
    },
    components: {
        calendarBlock
    },

    data() {
        return {
            monthList: [
                "JAN", "FEB",
                "MAR", "APR", "MAY",
                "JUN", "JUL", "AUG",
                "SEP", "OCT", "NOV",
                "DEC"
            ],
            jan: "TEST JAN"
        }
    }
    
}
</script>

<style>

</style>


