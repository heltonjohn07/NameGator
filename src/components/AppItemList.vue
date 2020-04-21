<template>
  <div>
    <h5>{{ title }} <span class="badge badge-info">{{ items.length }}</span></h5>
    <div class="card">
      <div class="card-body">
        <ul class="list-group">
          <li class="list-group-item" v-for="item in items" :key=item>
            <div class="row">
              <div class="col-md">
                {{ item }}
              </div>
              <div class="col-md text-right">
                <button v-on:click="deleteItem(item)" class="btn btn-info" > <span class="fa fa-trash"></span> </button>
              </div>
            </div>
          </li>
        </ul>
        <br />
        <div class="input-group">
          <input v-model="item" v-on:keyup.enter="addItem(item)" type="text" class="form-control" placeholder="Digite o item">
          <div class="input-group-append">
            <button class="btn btn-info" v-on:click="addItem(item)"> <span class="fa fa-plus"></span> </button>
          </div>
        </div>             
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppitemList",
  props: ["items", "title"],
  data: function(){
    return{
      item: [],
    };
  },
  methods: {
    addItem(item){
      this.$emit("addItem", item);
      this.item = "";
    },
    deleteItem(item){
      this.$emit("deleteItem", item);
      this.item = "";
    }
  },
};
</script>

<style scoped>

</style>
