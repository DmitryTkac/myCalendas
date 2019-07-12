<template>
    <tbody>
        {{renderQ()}}
        <month 
            v-bind:key="i.id" 
            v-for="i in 12" 
            v-bind:month='i' 
            v-bind:year='year'
            v-bind:spacing='configureSpacing(i)' 
        />
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
        year: Number,        
    },

    methods: {
        configureSpacing: function(month) {
            let spacing = new Date(this.year, month-1, 1).getDay()-1;
            if (spacing == -1) {
                return 6;
            }
            return spacing;
        },
        renderQ: function() {
            if (this.eventStart > this.eventEnd) {
                let buff = this.eventStart;
                this.eventStart = this.eventEnd;
                this.eventEnd = buff;
            }
            
            //return this.eventStart + " " + this.eventEnd;            
        }
    },
    

    date() {
        return {
            
            //monthDayCount: JAN: 31, FEB: 28 |>4 29, MAR: 31, APR: 30, MAY: 31, JUN: 30, JUL: 31
            //               AUG: 31, SEP: 30, OCT: 31, NOV: 30, DEC: 31        
        }
    }
}
</script>

<style>

</style>


