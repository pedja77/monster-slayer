<template>
    <div class="small-6 columns">
        <h1 class="text-center">{{ player }}</h1>
        <div class="healthbar">
            <div class="healthbar text-center"
             style="background-color: green; margin: 0; color: white;"
             :style="{width: health  + '%'}">

            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['player', 'health']

    }
</script>