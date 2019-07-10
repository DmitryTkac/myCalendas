<template>
    <td v-if="type == 'day'" class="day">
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
        value: [String, Number]
    }

}
</script>

<style>
    .void {
        background: repeating-linear-gradient(45deg, transparent, transparent 2px,#80808078 2.5px,#80808078 5px    )
    }

    .day {
        background: lightslategray;
        padding: 13px;
        color: white;
    }

    .week {
        background: #5a5a5a;
        padding: 13px;
        font-size: 13pt;
        color: white;
    }

    .month {
        font-size: 16pt;
        padding: 13px;
    }

    .weekSpace {
        padding: 5px;
    }

    .weekMonth {
        padding: 20px;
    }
</style>


