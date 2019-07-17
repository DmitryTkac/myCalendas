<template>
    <div class="colorInfoBox">
    
        <div v-bind:style="{background: eColor} " class="color">

        </div>
        <div class="colorName">
            {{colorName}}
        </div>
    </div>    
</template>

<script>
export default {
    name: "colorTable",

    props: {
        eColor: String,
        colorName: String
    }
}
</script>

<style>

    .colorInfoBox {
        width: 140px;
        display: inline-block;
        margin: 20px;
    }

    .color {
        height: 60px;
    }
    .colorName {
        height: 50px;
    }
</style>


