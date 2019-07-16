<template>
    <div id="cntrBox">
        <div id="dateInfo">
            <h2>
                {{showFormated[0]}}
            </h2>
            <h2>
                {{showFormated[1]}}
            </h2>

            <div>
                {{loadStandartData()}}
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
                <button @click="$parent.$parent.addEvent(start_date, end_date, selectedEvent, eventDescr)">CONFIRM</button>
                <button @click="$parent.$parent.closeEventBox()">CLOSE</button>
            </div>
            
            
        </div>
    </div>    
</template>

<script>
export default {

    name: "eventBox",

    props: {
//        id: Number,
        start_date: Date,
        end_date: Date,
    },

    date() {
        return {
            selectedEvent: "vacantion",
            eventDescr: ""
        }
    },

    methods: {
        changeEvent: function(event) {
            this.selectedEvent = event.target.value;
        },

        loadStandartData: function() { //TO AVOID THE ERROR
            this.selectedEvent = "vacantion";
            this.eventDescr = "";
        }
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


