<template>
    <div id="cntrBox">
        FROM: 
    </div>    
</template>

<script>
export default {

    name: "eventBox",

    props: {
        id: Number,
        start_date: Date,
        end_date: Date,
        description: String
    }
}
</script>

<style>
    #cntrBox {
        margin: auto;        
    }


</style>


