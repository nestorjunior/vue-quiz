<template>
    <div>
        Player <span>{{this.winCount}}</span> X <span>{{this.loseCount}}</span> Computer
    </div>
</template>

<script>
export default {
    props: ['winCount', 'loseCount']
}
</script>

<style lang="sass" scoped>

</style>