<template>
    <div>
        <div v-for="(item, index) in items" :key="index">
            <list-item
                :item="item"
                class="item"
                v-on:itemchanged="$emit('reloadlist')">
            </list-item>
        </div>
    </div>
</template>

<script>
import listItem from "./listItem"

export default {
    components: {
        listItem
    },
    props: ['items'],
}
</script>


<style scoped>

.item{
    padding: 5px;
}

</style>