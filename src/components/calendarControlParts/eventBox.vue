<template>
    <div id="cntrBox">
        {{loadStandartData(start_date, end_date)}}\
        <div id="dateInfo">
            <h2 id="Datepicker">                   
                FROM
                <Datepicker ref="datepicker_1" v-model="from" @selected="selectStartDate"/>                
            </h2>
            <h2 id="Datepicker">
                TO
                <Datepicker ref="datepicker_2" v-model="to" @selected="selectEndDate"/>                
            </h2>

            <div>
                <h3>DESCRIPTION</h3>
                <textarea rows="10" cols="55" name="comment" form="usrform" v-model="eventDescr">
                    
                </textarea>
                <h3>
                    TYPE
                </h3>
                <select @change="changeEvent($event)">
                    <option value="vacantion">
                        Vacantion
                    </option>
                    <option value="sickLeave">
                        Sick leave
                    </option>
                    <option value="businessTrip">
                        Business Trip
                    </option>
                </select>
                <button @click="$parent.$parent.addEvent(new Date(from.getFullYear(), from.getMonth(), from.getDate()), to, selectedEvent, eventDescr, eventColor)">CONFIRM</button>
                <button @click="$parent.$parent.closeEventBox()">CLOSE</button>
            </div>
            
            
        </div>
    </div>    
</template>

<script>
import Datepicker from 'vuejs-datepicker';
export default {

    name: "eventBox",

    components: {
        Datepicker
    },

    props: {
//        id: Number,
        start_date: Date,
        end_date: Date,
    },

    date() {
        return {
            selectedEvent: "vacantion",
            eventDescr: "",
            eventColor: "rgb(255, 255, 176)",
            from: Date,
            to: Date
        }
    },

    methods: {
        changeEvent: function(event) {
            this.selectedEvent = event.target.value;
            if (event.target.value == "vacantion") {
                this.eventColor = "rgb(255, 255, 176)";
            } else if (event.target.value == "sickLeave") {
                this.eventColor = "lightgreen";
            } else if (event.target.value == "businessTrip") {
                this.eventColor = "rgb(138, 170, 204)";
            }
            
        },

        loadStandartData: function(from, to) { //TO AVOID THE ERROR
            this.selectedEvent = "vacantion";
            this.eventDescr = "";
            this.eventColor = "rgb(255, 255, 176)";
            this.from = from;
            this.to = to;
        }, 

        selectStartDate: function(date) {
            
            this.from = date;
            if (this.to === null) {
                this.to = this.from;
                this.$refs.datepicker_2._data.selectedDate = this.$refs.datepicker_1._data.selectedDate;
            }
            
        },

        selectEndDate: function(date) {            
            //console.log(date);
            this.to = date;
        },

    },

    computed: {
        showFormated: function() {
            return [
                "FROM \"" + this.start_date.getFullYear() + "-" + this.start_date.getMonth() + "-" + this.start_date.getDate() + "\"",
                "TO \"" + this.end_date.getFullYear() + "-" + this.end_date.getMonth() + "-" + this.end_date.getDate() + "\""
            ];
        },

        
    }
}
</script>

<style>
    #Datepicker {        
        margin-left: 10px;
        margin-right: 10px;
        display: inline-block;
    }

    #cntrBox {
        margin: auto;        
    }
    #dateInfo {
        text-align: center;
    }

    textarea {
        resize: none;
    }

    select {
        width: 150px;
        margin: 40px auto 60px;
        display:list-item

    }

    #space {
        margin-top: 350px;
    }
</style>


