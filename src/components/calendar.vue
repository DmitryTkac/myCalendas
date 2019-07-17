<template>
    <div class="calendarFrame">

        <v-dialog/>

        <modal name="eventBox" :height="500" :width="700">
            <eventBox 
                v-bind:start_date="marking.start.normalDate"
                v-bind:end_date="marking.end.normalDate"
            />
        </modal>

        <h1>THIS IS CALENDAS</h1>
        
        <h2> <span v-on:click='prevYear()' class="button">«</span>  {{ customYear }} <span v-on:click='nextYear()' class="button">»</span> 
        </h2>
        <table>
  
            <weekBar></weekBar>
            <allMonth 
                v-bind:year='customYear' 

            />
        </table>
        <h1>YOUR CHOOSE: {{chooseDate}}</h1>
        <h1>EVENT RANGE: {{ marking.start.formatedDate }} - {{ marking.end.formatedDate }} </h1>

        <hr>

        <button @click="eraseMarking()"><h2>ERASE MARKING</h2></button>
        <button @click="todayButton()"><h2>TODAY</h2></button>
        <button @click="show()"><h2>REGISTER EVENT</h2></button>
        
        <hr>
        
        <colorTable eColor="rgb(255, 255, 176)" colorName="Vacantion"/>
        <colorTable eColor="rgb(255, 255, 89)" colorName="Vacantion Approved"/>
        <colorTable eColor="lightgreen" colorName="Sick Leave"/>
        <colorTable eColor="rgb(75, 209, 75)" colorName="Sick Leave Approved"/>
        <colorTable eColor="rgb(138, 170, 204)" colorName="Business Trip"/>
        <colorTable eColor="rgb(87, 127, 170)" colorName="Business Trip Approved"/>
        
        
    </div>
</template>

<script>

import VModal from 'vue-js-modal'
import Vue from 'vue'; 
Vue.use(VModal,{ dialog: true }, { dynamic: true, dynamicDefaults: { clickToClose: true } });


import allMonth from './calendarParts/allMonth.vue';
import weekBar from './calendarParts/weekBar.vue';
import eventBox from './calendarControlParts/eventBox.vue';
import colorTable from './calendarParts/colorTable.vue';

//import calendarBlock from './calendarParts/calendarBlock.vue';

export default {
    name: "calendar",

    data() {
        return {
            today: this.getToday(),
            customYear: this.getToday().getFullYear(), //-271821 - 275760

            marking: {
                start: {
                    formatedDate: '',
                    normalDate: null,
                    isEvent: true
                },
                end: {
                    formatedDate: '',
                    normalDate: null,
                }
            },

            range: 0,
            chooseDate: 0,

            events: [                
                {
                    type: "vacantion",
                    start_date: new Date(2019, 7, 15),
                    end_date: new Date(2019, 7, 25),
                    statusColor: "rgb(255, 255, 176)"
                },
                {
                    type: "vacantion",
                    start_date: new Date(2019, 9 ,15),
                    end_date: new Date(2019, 9, 25),
                    statusColor: "rgb(255, 255, 89)"
                },
                {
                    type: "sickLeave",
                    start_date: new Date(2018, 11, 1),
                    end_date: new Date(2019, 1, 10),
                    statusColor: "lightgreen"
                },
                {
                    type: "sickLeave",
                    start_date: new Date(2019, 2, 12),
                    end_date: new Date(2019, 2, 14),
                    statusColor: "rgb(75, 209, 75)"
                },
                {
                    type: "businessTrip",
                    start_date: new Date(2019, 3, 3),
                    end_date: new Date(2019, 4, 1),
                    statusColor: "rgb(138, 170, 204)"                    
                },
                {
                    type: "businessTrip",
                    start_date: new Date(2019, 4, 14),
                    end_date: new Date(2019, 4, 15),
                    statusColor: "rgb(87, 127, 170)"
                },
            ]

        }       
    },

    components: {
        weekBar,
        allMonth,
        eventBox,
        colorTable
        //calendarBlock
    },

    methods: {

        show () {

            //  if (this.marking.start.normalDate == null) {
            //     this.$modal.show('dialog', {            
            //     title: 'Event register ERROR',
            //     text: 'Please select some date or date range to make event!',
            //     buttons: [                
            //         {
            //             title: 'Cancel'
            //         }
            //     ]
            //     })
            //     return;
            // }

            let i = 0;
            for (i in this.events) {
                if (this.marking.start.normalDate <= this.events[i].start_date && this.events[i].end_date <= this.marking.end.normalDate) {
                    this.$modal.show('dialog', {            
                    title: 'Event register ERROR',
                    text: 'Your marked event are in existing event!',
                    buttons: [                
                        {
                            default: true,
                            title: 'Cancel'
                        }
                    ]
                    })
                    return;
                }
            }
        
                        
            this.$modal.show('dialog', {            
            title: 'Event register',
            text: 'Do you want to make event?',
            buttons: [
                {
                    title: 'YES',
                    default: true,
                    handler: () => { 
                        this.$modal.hide('dialog');
                        this.$modal.show('eventBox');                        
                    }
                },                
                {
                    title: 'Cancel'
                }
            ]
            })
           
            //this.$modal.show('hello-world');
        },

        addEvent: function(from, to, selection, description, color) {
            //console.log(from + " \n " + to  + " \n " +  selection  + " \n " +  description);
            if (from > to) {
                let buff = from
                from = to;
                to = buff;
            }
            let i = 0;
            for (i in this.events) {
                if (
                    //(from <= this.events[i].start_date && this.events[i].end_date <= to)
                    !((from < this.events[i].start_date && to < this.events[i].start_date)
                    ||
                    (from > this.events[i].end_date && to > this.events[i].start_date))
                ) {
                    this.$modal.show('dialog', {            
                    title: 'Event register ERROR',
                    text: 'Your marked event are in existing event!',
                    buttons: [                
                        {   
                            default: true,
                            title: 'Cancel'
                        }
                    ]
                    })
                    this.$modal.hide('eventBox');
                    return;
                }
            }

            let eventPack = {
                type: selection,
                start_date: from,
                end_date: to,
                approved: false,
                statusColor: color
            }
            this.events.push(eventPack);
            this.closeEventBox();
            this.eraseMarking();
        },

        closeEventBox: function() {
            this.$modal.hide('eventBox');
        },

        nextYear: function() { //Incrase the year value to change the year to the next
            this.customYear++;
        },

        prevYear: function() { //Decrase the year value to change the year to the previous
            this.customYear--;
        },

        getToday: function() {
            return new Date();            
        },

        //CALENDAR BUTTON FUNCTIONAL/EVENTS

        todayButton: function() {  //ARE USED TO RERENDER THE CALENDAR FOR "TODAY" CLASS ANIMATION PLAYING, WHEN USER PRESS TODAY BUTTON
            this.customYear++;
            this.$nextTick( () => { 
                this.customYear = this.getToday().getFullYear();
            });
            
        },

        eraseMarking: function() {
            this.marking.start.formatedDate = this.marking.end.formatedDate = '';
            this.marking.start.normalDate = this.marking.end.normalDate = null;
            this.marking.start.isEvent = true;
        },

        registerEvent: function(date) {            
            if (this.marking.start.isEvent) {
                this.marking.start.formatedDate = this.marking.end.formatedDate = '';
                
                this.marking.start.formatedDate = this.processDate(date);
                this.marking.start.normalDate = date;
                this.marking.start.isEvent = !this.marking.start.isEvent;

                this.marking.end.normalDate = this.marking.start.normalDate;
            } else {
                this.marking.end.formatedDate = this.processDate(date);
                this.marking.end.normalDate = date;
                this.marking.start.isEvent = !this.marking.start.isEvent;         

                if (this.marking.start.normalDate > this.marking.end.normalDate) { //make sorting
                    let buff = this.marking.start.normalDate;
                    this.marking.start.normalDate = this.marking.end.normalDate
                    this.marking.end.normalDate = buff;

                    buff = this.marking.start.formatedDate;
                    this.marking.start.formatedDate = this.marking.end.formatedDate;
                    this.marking.end.formatedDate = buff;
                }

            } 
        }, 

        //FORMAT DATE
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
        font-size: 9pt;
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

    button {
        background-color: white; /* Green */
        border: 1px solid gray;
        color: rgb(78, 74, 74);
        padding: 15px 37px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        margin: 0px 10px 7px 10px
    }
</style>


