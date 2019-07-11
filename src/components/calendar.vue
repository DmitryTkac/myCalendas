<template>
    <div class="calendarFrame">
        <h1>THIS IS CALENDAS</h1>
        <h2> <span v-on:click='prevYear()' class="button">«</span>  {{ customYear }} <span v-on:click='nextYear()' class="button">»</span> </h2>
        <table>
            <weekBar></weekBar>
            <allMonth v-bind:year='customYear'/>
        </table>
    </div>
</template>

<script>

import allMonth from './calendarParts/allMonth.vue';
import weekBar from './calendarParts/weekBar.vue';

//import calendarBlock from './calendarParts/calendarBlock.vue';

export default {
    name: "calendar",

    data() {
        return {
            today: this.getToday(),
            customYear: this.getToday().getFullYear(),
            eventStart: null,
            eventEnd: null
        }        
    },

    components: {
        weekBar,
        allMonth,
        //calendarBlock
    },

    methods: {
        getToday: function() {
            return new Date();
        },

        nextYear: function() {
            this.customYear++;
        },

        prevYear: function() {
            this.customYear--;
        }
    }



}
</script>

<style >
    .button {
        cursor: pointer;
    }

    .calendarFrame {
        border-radius: 5px;
        border: 1px solid black;
        user-select: none;    
        position: relative;
        display: inline-block;
        margin: auto;
        
    }


    table {
        border-collapse: collapse; 
         
        background: repeating-linear-gradient(45deg, transparent, transparent 2px,#80808078 2.5px,#80808078 5px    ) 
    }

    #jan {
        font-size: 16pt;
        padding: 15px;
    }

    #janday {
        padding: 0 10px 0 10px;
        font-size: 15pt;
    }
</style>


