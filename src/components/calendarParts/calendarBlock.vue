<template>
    <td v-if="type == 'day' && date.getDay()==0" id="sunday" class="day">
        {{ value }}
    </td>
    <td v-else-if="type == 'day'" class="day">
        {{ value }}
    </td>
    <td v-else-if="type == 'void'" class="void">

    </td>
    <td v-else-if="type == 'space'" class="void">
        
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
        date: Object
    }

}
</script>

<style>
    .void {

    }

    #sunday {
        border: solid;
        border-right-width: 13px;
        border-top: hidden;
        border-bottom: hidden;
        border-left: hidden;
        border-right-color: lightgrey;
        background: rgb(252, 113, 113);
    }

    #sunday:hover{
        background: rgb(255, 157, 157);
    }

    .day {
        background: rgb(156, 172, 189);
        padding: 12px;
        color: white;
    }

    .day:hover{
        background: rgb(202, 202, 202);
    }

    .week {
        background: #5a5a5a;
        padding: 13px;
        font-size: 13pt;
        color: white;
    }

    .weekS {
        background: #5a5a5a;
        padding: 13px;
        font-size: 13pt;
        color: white;
    }

    .month {
        font-size: 15pt;
        padding: 13px;
        background: white;
    }

    .weekSpace {
        padding: 5px;
    }

    .weekMonth {
        padding: 20px;
    }
</style>


