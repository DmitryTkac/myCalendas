<template>
    <div class="calendarFrame">
        <h1>THIS IS CALENDAS</h1>
        <h2> <span v-on:click='prevYear()' class="button">«</span>  {{ customYear }} <span v-on:click='nextYear()' class="button">»</span> 
        </h2>
        <table>
            <weekBar></weekBar>
            <allMonth 
                v-bind:year='customYear' 

            />
        </table>
        <h1>YOUR CHOOSE: {{datums}}</h1>
        <h1>EVENT RANGE: {{ event.start.formatedDate }} - {{ event.end.formatedDate }} </h1>
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

            event: {
                start: {
                    formatedDate: '',
                    normalDate: null,
                    isEvent: true
                },
                end: {
                    formatedDate: '',
                    normalDate: null,
                    isEvent: false
                }
            },

            range: "NONE",
            datums: 0,
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
        },

        registerEvent: function(date) {
            
            if (this.event.start.isEvent) {
                this.event.start.formatedDate = this.event.end.formatedDate = '';
                
                this.event.start.formatedDate = this.processDate(date);
                this.event.start.normalDate = date;
                this.event.start.isEvent = !this.event.start.isEvent;

                this.event.end.normalDate = this.event.start.normalDate;
            } else {
                this.event.end.formatedDate = this.processDate(date);
                this.event.end.normalDate = date;
                this.event.start.isEvent = !this.event.start.isEvent;
                
                if (!confirm("Make event? [ FROM " + this.event.start.formatedDate + " TO " +  this.event.end.formatedDate + " ]")) {
                    this.event.start.formatedDate = this.event.end.formatedDate = '';
                    this.event.end.normalDate = this.event.start.normalDate = null;
                }
            }
        },

        processDate: function(date) {
            return date.getDate() + "-" + (date.getMonth()+1) + "-" + date.getFullYear();
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


