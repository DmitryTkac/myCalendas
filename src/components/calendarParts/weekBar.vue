<template>
        <thead id="weekBar">
            <tr>

                <calendarBlock type="weekMonth"/>

                <calendarBlock type="week" v-bind:key="i" v-for="i in weekDays" v-bind:value='i'/>

                <calendarBlock type="weekSpace"/>

                <calendarBlock type="week" v-bind:key="i" v-for="i in weekDays" v-bind:value='i'/>
                
                <calendarBlock type="weekSpace"/>

                <calendarBlock type="week" v-bind:key="i" v-for="i in weekDays" v-bind:value='i'/>
                
                <calendarBlock type="weekSpace"/>

                <calendarBlock type="week" v-bind:key="i" v-for="i in weekDays" v-bind:value='i'/>

                <calendarBlock type="weekSpace"/>

                <calendarBlock type="week" v-bind:key="i" v-for="i in weekDays" v-bind:value='i'/>

            </tr>
        </thead>
</template>

<script>

import calendarBlock from './calendarBlock.vue';
//import weekBarTitles from './weekBarTitles.vue';

export default {
    name: "weekBar",

    components: {
        //weekBarTitles,
        calendarBlock        
    },

    data() {
        return {
            //weekDays: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
            weekDays: ["M", "T", "W", "T", "F", "S", "S"]
        }
    }
}

</script>

<style>
    #weekBar {
        background-color: #5a5a5a;
        color: white;

    }

    #weekPad {
        padding: 5px;
    }

    #weekMonPad {


        padding: 20px;
    }

</style>


