<template>
  <div >
    <div id="slogan" class="text-center">
      <h1>NameGator</h1>
      <br />
      <h6 class="text-secondary">Gerador de Nomes Utilizando VueJS, bootstrap, GraphQL e NodeJS</h6>
    </div>
    <div id='main'>
      <div class="container">
        <div class="row">

          <div class="col-md">
            <h5>Prefixos <span class="badge badge-info">{{ prefixes.length }}</span></h5>
            <div class="card">
              <div class="card-body">

                <ul class="list-group">
                  <li class="list-group-item" v-for="prefix in prefixes" :key=prefix>
                    <div class="row">
                      <div class="col-md">
                        {{ prefix }}
                      </div>
                      <div class="col-md text-right">
                        <button v-on:click="deletePrefix(prefix)" class="btn btn-info" > <span class="fa fa-trash"></span> </button>
                      </div>
                    </div>
                  </li>
                </ul>

                <br />

                <div class="input-group">
                  <input v-model="prefix" v-on:keyup.enter="addPrefix(prefix)" type="text" class="form-control" placeholder="Digite o Prefixo">
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addPrefix(prefix)"> <span class="fa fa-plus"></span> </button>
                  </div>
                </div>
                
              </div>
            </div>
          </div>

          <div class="col-md">
            <h5>Sufixos <span class="badge badge-info">{{ sufixes.length }}</span> </h5>
            <div class="card">
              <div class="card-body">

                <ul class="list-group">
                  <li class="list-group-item" v-for="sufix in sufixes" :key=sufix>
                    <div class="row">
                      <div class="col-md">
                        {{ sufix }}
                      </div>
                      <div class="col-md text-right">
                        <button v-on:click="deleteSufix(sufix)" class="btn btn-info" > <span class="fa fa-trash"></span> </button>
                      </div>
                    </div>
                  </li>
                </ul>

                <br />

                <div class="input-group">
                  <input v-model="sufix" v-on:keyup.enter="addSufix(sufix)" type="text" class="form-control" placeholder="Digite o Sufixo">
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addSufix(sufix)"> <span class="fa fa-plus"></span> </button>
                  </div>
                </div>

              </div>
            </div>
          </div>
          
        </div>

        <br />
        <h5>Dominios <span class="badge badge-info">{{ domains.length }}</span> </h5>
        <div class="card">
          <div class="card-body">
            <ul class="list-group">
              <li class="list-group-item" v-for="domain in domains" :key=domain>
                {{ domain }}
              </li>
            </ul>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";

export default {
	name: "App",
	data: function(){
		return{
      prefix:"",
      sufix:"",
			prefixes:["Air","Jet", "Flight"],
			sufixes:["Hub","Station","Mart"],
			domains:[]
		};
  },
  methods:{
    addPrefix(prefix){
      if (prefix==="") return;
      this.prefixes.push(prefix);
      this.generate();
      this.prefix="";
    },
    deletePrefix(prefix){
      this.prefixes.splice(this.prefixes.indexOf(prefix),1);
      this.generate();
    },
    addSufix(sufix){
      if (sufix==="") return;
      this.sufixes.push(sufix);
      this.generate();
      this.sufix="";
    },
    deleteSufix(sufix){
      this.sufixes.splice(this.sufixes.indexOf(sufix),1);
      this.generate();
    },
    generate() {
      this.domains=[];
      this.prefixes.forEach(prefix => {
        this.sufixes.forEach(sufix => {
          this.domains.push(prefix+sufix);
        });
      });
    },
  },
  created: function(){
    this.generate();
  }
  
};
</script>

<style>
#slogan{
  margin-top: 30px;
  margin-bottom: 30px;
}
#main{
  background-color: #F1F1F1;
  padding-top: 30px ;
  padding-bottom: 30px;
}

</style>
