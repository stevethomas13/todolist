<template>
    <div id="addItem" class="container-fluid p-0 mb-5">
        <form action="#" class="container-fluid">
            <div class="row">
                <input type="text" v-model="item.name" class="col-sm-10 pe-3 rounded" placeholder="Enter item">
                <button @click="addItem()" :class="[item.name ? 'btn btn-success' : 'btn btn-danger', 'btn btn-sm col-sm-2']"> Add
                </button>
            </div>
        </form>
        <!-- <input class="inputItem" type="text" v-model="item.name"> -->
        <!-- <font-awesome-icon 
        :class="[ item.name ? 'active' : 'notactive', 'plus' ]" 
        icon="plus-square"
        @click="addItem()"
        /> -->
        <!-- <button @click="addItem()" :class="[item.name ? 'btn btn-success' : 'btn btn-secondary', 'btn btn-sm']">Add</button> -->
    </div>
</template>

<script>
export default {
    data: function() {
        return {
            item: {
                name: ""
            }
        }
    },
    methods:{
        addItem() {
            if (this.item.name == '') {
                return;
            }

            axios.post('api/item/store', {
                item: this.item
            })
            .then(response=> {
                if (response.status == 201){
                    this.item.name = "";
                    this.$emit('reloadlist');
                }
            })
            .catch(error=> {
                console.log('error');
            })
        }
    }
}
</script>

<style scoped>

</style>