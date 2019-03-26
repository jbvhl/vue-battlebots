<template>
    <div>
        <h3>{{botObj.bot}}</h3>
        <p>{{botObj.attack}}</p>
        <p>{{botObj.health}}</p>
        <button @click='selectBot(botObj)'>Select</button>
        <button @click="deleteBot(index)">Retire</button>
        <hr>
    </div>
</template>

<script>
export default {
props: ['botObj', 'deleteBot', 'selectBot', 'index']
}
</script>