<template>
    <div class="item mb-2 rounded bg-info d-flex">
        <div class="form-check">
            <input type="checkbox" 
            @change="updateCheck()"
            v-model="item.completed"
            class="form-check-input">
        </div>
        <p :class="[item.completed ? 'text-secondary text-decoration-line-through' : '', 'itemText text-dark h6 m-auto fst-normal']"> {{ item.name }}</p>
        <button @click="removeItem()" class="bg-info trashcan " >
            <font-awesome-icon icon="trash"/>
        </button>
    </div>
</template>

<script>
export default {
    props: ['item'],
    methods: {
        updateCheck() {
            axios.put('api/item/' + this.item.id, {
                item: this.item
            })
            .then( response => {
                if ( response.status == 200 ) {
                    this.$emit('itemchanged');
                }
            })
            .catch ( error => {
                console.log( error );
            })
        },
        removeItem() {
            axios.delete('api/item/'+this.item.id, {
                item: this.item
            })
            .then( response => {
                if ( response.status == 200) {
                    this.$emit('itemchanged');
                }
            })
            .catch( error => {
                console.log( error );
            })
        }
    }
}
</script>

<style scoped>

.trashcan{
    color: red;
    border: none;
}


</style>