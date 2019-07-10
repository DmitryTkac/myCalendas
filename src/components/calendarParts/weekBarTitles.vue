<template>
    <div id="weekBarTitles">
    <th v-bind:key="weekBar" v-for="weekBar in weekDays">
        <span>
            {{ weekBar }}
        </span>
    </th>      
    </div>                              
</template>

<script>

export default {
    name: "weekBarTitles",

    data() {
        return {
            weekDays: ["M", "T", "W", "T", "F", "S", "S"]
        }
    }
}

</script>

<style>
    #weekBarTitles {
        padding: 10px;   
        font-size: 15pt; 
        font-weight: 400;    
    }

    #weekBarTitles th {
        padding: 0 10px 0 10px;
    }
    
</style>


