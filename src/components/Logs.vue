<template>
   <div class="small-12 columns">
            <ul>
                <div v-for="(log, key) in logs" :key="key">
                <li class="player-turn">
                    {{ log.player  }}
                </li>
                <li class="monster-turn">
                    {{ log.monster  }}
                </li>
                </div>
            </ul>
        </div>
</template>

<script>
export default {
    props: ['logs']
}
</script>


