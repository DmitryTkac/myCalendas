<template>
        <thead id="weekBar">
            <tr>
                
                <calendarBlock type="weekMonth"/>

                <calendarBlock type="week" v-bind:key="i.id" v-for="i in weekDays" v-bind:value='i'/>
                <calendarBlock type="weekS" value='S'/>

                <calendarBlock type="week" v-bind:key="i.id" v-for="i in weekDays" v-bind:value='i'/>
                <calendarBlock type="weekS" value='S'/>

                <calendarBlock type="week" v-bind:key="i.id" v-for="i in weekDays" v-bind:value='i'/>
                <calendarBlock type="weekS" value='S'/>

                <calendarBlock type="week" v-bind:key="i.id" v-for="i in weekDays" v-bind:value='i'/>
                <calendarBlock type="weekS" value='S'/>

                <calendarBlock type="week" v-bind:key="i.id" v-for="i in weekDays" v-bind:value='i'/>
                <calendarBlock type="weekS" value='S'/>

                <calendarBlock type="weekS" v-bind:key="i.id" v-for="i in 2" v-bind:value='weekDays[i-1]'/>

            </tr>
        </thead>
</template>

<script>

import calendarBlock from './calendarBlock.vue';
//import weekBarTitles from './weekBarTitles.vue';

export default {
    name: "weekBar",

    components: {
        //weekBarTitles, | MB DELETE
        calendarBlock        
    },

    data() {
        return {
            //weekDays: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
            weekDays: ["M", "T", "W", "T", "F", "S"]
        }
    }
}

</script>

<style>
    #weekBar {
        background-color: #5a5a5a;
        color: white;

    }
</style>


