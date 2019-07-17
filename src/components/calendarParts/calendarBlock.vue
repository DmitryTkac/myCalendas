<template>
    <td v-if="type == 'day'" 
        v-bind:class="checkDay()"  
        v-on:click='getYouChoose(eventType)'
        v-bind:style="{background: statusColor}"
    >
        {{ value }}
    </td>
    <td v-else-if="type == 'void' || type == 'space'" class="void">

    </td>
    <td v-else-if="type == 'month'" class="month">
        {{ value }}
    </td>
    <th v-else-if="type == 'week'" class="week">
        {{ value }}
    </th>
    <th v-else-if="type == 'weekS'" class="weekS"> 
        {{ value }}
    </th>
    <th v-else-if="type == 'weekSpace'" class="weekSpace">
        
    </th>
    <th v-else-if="type == 'weekMonth'" class="weekMonth">
        
    </th>
</template>

<script>
export default {
    name: "calendarBlock",

    props: {
        type: String, //Month, weekMonth, week, weekSpace, space, day, void
        value: [String, Number],
        date: Date,
        eventType: String,
        isApproved: Boolean,
        eventRegisterHelper: Boolean,
        eventColor: String
    },

    data() {
        return {
            statusColor: "white",
        }
    },
    
    methods: {
        getYouChoose: function(eventType) {
            if (eventType == "day") {
                this.$parent.$parent.$parent.chooseDate = this.$parent.$parent.$parent.processDate(this.date);
                this.$parent.$parent.$parent.registerEvent(this.date);    
            }
            
            
            //this.$parent.$parent
        },

        checkEvented: function() {
            let type = "hover";            
            
            if (this.eventType == "day" && this.eventRegisterHelper) {
                this.statusColor = "lightcoral";
                
            } else if (this.eventType == "day") {
                this.statusColor = "";
                
                type += " day"
            } else { 
                   
                this.statusColor = this.eventColor;                
            }
            
            if (this.date.getDate() == new Date().getDate() 
                && this.date.getMonth() == new Date().getMonth() 
                && this.date.getFullYear() == new Date().getFullYear()) {
                type += " today";
            }
            return type;
        },

        checkDay: function() {
            let classes = this.checkEvented();
            if (this.date.getDay() == 0) {
                classes += " sunday";
            } else if (this.date.getDay() == 6) {
                classes += " holiday";
            } 

            
            return classes;
        }
  
    }

}
</script>

<style>

    
    .void {

    }

    .today {
        animation-name: today;
        animation-duration: 2s;
    }

    @keyframes today {        
        50% {background: orange; color: white}        
    }

    .helperMarker {
        background: lightcoral;

        
    }
    /*  EVENTS NAMES
    vacantion - atvaļinājums -, sick_leave - slimība, business trip - komandējums */
    .hover:hover {
        filter: grayscale(50%)
    }

    .vacantion {
        background: rgb(255, 255, 176);  

        min-width: 12px;
        font-size: 9pt;
        padding: 9px;      
    }
    
    

    .vacantion_approved {
        background: rgb(255, 255, 89);

        min-width: 12px;
        font-size: 9pt;
        padding: 9px;
    }

    .sickLeave {
        background: lightgreen;
        
        min-width: 12px;
        font-size: 9pt;
        padding: 9px;
    }


    .sickLeave_approved {
        background: rgb(75, 209, 75);

        min-width: 12px;
        font-size: 9pt;
        padding: 9px;
    }
    
    .businessTrip {
        background: rgb(138, 170, 204);
        
        min-width: 12px;
        font-size: 9pt;
        padding: 9px;
    }

    .businessTrip_approved {
        background: rgb(87, 127, 170);

        min-width: 12px;
        font-size: 9pt;
        padding: 9px;
    }

    .holiday {
        font-weight: bold;
        
        min-width: 12px;
        font-size: 9pt;
        
    }
    .sunday {
        border: solid;
        border-right-width: 9px;
        border-top: hidden;
        border-bottom: hidden;
        border-left: hidden;
        border-right-color: lightgrey;
        /* background: rgb(252, 113, 113); */        
        
        font-weight: bold;
        
        min-width: 12px;
        font-size: 9pt;
        
    }

    .day {
        background: rgb(255, 255, 255);
        
        color: rgb(78, 73, 73);
        cursor: pointer;
        
        min-width: 12px;
        font-size: 9pt;
        
    }

    .day:hover{
        background: rgb(203, 205, 206);
    }

    .week {
        background: #5a5a5a;
        
        color: white;
        
        min-width: 13px;
        font-size: 9pt;
        padding: 9px;
    }

    .weekS { /*Week part: SUNDAY*/
        background: #5a5a5a;
        
        min-width: 17px;
        padding: 9px;
        
        color: white;
    }

    .month {
        font-size: 9pt;
        padding: 11px;
        background: white;
        font-weight: bold;
    }

    .weekSpace {
        padding: 5px;
    }

    .weekMonth {
        padding: 16px;
    }
</style>


