<template>
    <tr>    
        <!-- v-bind:isEvented='evented($parent.$parent.event.start.normalDate, $parent.$parent.event.end.normalDate, new Date(year, month-1, i))' -->
        <calendarBlock type="month" v-bind:value="monthList[month-1]"/>
        <calendarBlock type="space" v-bind:key="i.id" v-for="i in spacing"/>
        <calendarBlock type="day" 
            v-bind:key="i.id" 
            v-for="i in (new Date(year, month, 0).getDate())" 
            v-bind:value='i' 
            v-bind:date='new Date(year, month-1, i)'
            
            v-bind:eventType="loadEvents($parent.$parent.events, new Date(year, month-1, i))[0]"
            v-bind:isApproved="loadEvents($parent.$parent.events, new Date(year, month-1, i))[1]"
        />
        <calendarBlock type="space" v-bind:key="i.id" v-for="i in 37-spacing-(new Date(year, month, 0).getDate())"/>
    </tr>    
</template>

<script>
//REMEMBER: new Date(2019, 12, 0) == new Date(2019, 11, 31)
//                             ^^ = month MAX day count

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
        evented: function(rangeStart, rangeEnd, date) {
            if (rangeStart > rangeEnd) {
                let buff = rangeStart;
                rangeStart = rangeEnd;
                rangeEnd = buff;
            }
            if (rangeStart <= date && date <= rangeEnd) {
                return true;
            } 
            return false;
        },

        loadEvents: function(eventObj ,date) {
            let i = 0;
            for (i in eventObj) {
                if (eventObj[i].start_date <= date && date <= eventObj[i].end_date) {
                    return [eventObj[i].type, eventObj[i].approved];
                }                
            }
            return ["day", false];
            
        }
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