<template>
    <ul>
        <li v-for="(music,index) in musicList" :key="index">
                  {{music.title}}
        </li>
    </ul>
</template>
<script>

export default {
   props:[musicList] 
}

</script>
<style lang="sass" scoped>

</style>

