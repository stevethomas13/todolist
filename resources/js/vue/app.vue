<template>
    <div class="container rounded bg-black col-sm-4 p-10 mt-2">
        <div id="heading" class="container-fluid">
            <h2 id="title" class="container-fluid text-white display-3">Todo List</h2>
            <add-item-form v-on:reloadlist="getList()">
            </add-item-form>
        </div>
         <list-view class="container-fluid pb-10px"
         :items="items"
         v-on:reloadlist="getList()"> </list-view>
    </div>
</template>

<script>
import addItemForm from "./addItemForm"
import listView from "./listView"

export default {
  components: {
      addItemForm,
      listView,
  },
  data: function() {
      return {
          items: []
      }
  },
  methods: {
      getList() {
          axios.get('api/items')
          .then( response => {
              this.items = response.data
          })
          .catch ( error=> {
              console.log( error );
          })
      }
  },
  created() {
      this.getList();
  }
}
</script>


<style scoped>
*{
    justify-content: center;
    text-align: center;
}

#title{
    font-family: 'Times New Roman', Times, serif;
    text-align: center;
}

@import'~bootstrap/dist/css/bootstrap.css'

</style>