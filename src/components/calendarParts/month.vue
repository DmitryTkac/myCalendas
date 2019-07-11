<template>
    <tr>    
        
        <calendarBlock type="month" v-bind:value="monthList[month-1]"/>
        <calendarBlock type="space" v-bind:key="i.id" v-for="i in spacing"/>
        <calendarBlock type="day" 
            v-bind:key="i.id" 
            v-for="i in (new Date(year, month, 0).getDate())" 
            v-bind:value='i' 
            v-bind:date='new Date(year, month-1, i)'/>
        <calendarBlock type="space" v-bind:key="i.id" v-for="i in 37-spacing-(new Date(year, month, 0).getDate())"/>
    </tr>    
</template>

<script>
//REMEMBER: new Date()

import calendarBlock from './calendarBlock.vue';

export default {
    name: "month",
    props: {
        month: Number,
        year: Number,
        spacing: Number //IF SPACING == 6 THEN IT IS SUNDAY MY BRUDA
    },
    components: {
        calendarBlock
    },

    methods: {

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
            
        }
    }
    
}
</script>

<style>

</style>