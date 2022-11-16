
<script setup lang="ts"></script>

<template>

    <section class="container-fluid p-4">
        <div class="row dark">
            <div class="col-md-12">
                <div class="container-fluid p-4">
                    <h1>
                        Gestion des etudients
                    </h1>
                    <!-- Button trigger modal -->
                    <button type="button" class="btn btn-primary align-items-center pull-right m-2"
                        data-bs-toggle="modal" data-bs-target="#addmodal">
                        Ajouter <i class="fa fa-plus fa-x"></i>
                    </button>

                    <!-- AddModal -->
                    <div class="modal fade" id="addmodal" tabindex="-1" aria-labelledby="addmodalLabel"
                        aria-hidden="true">
                        <div class="modal-dialog">
                            <div class="modal-content">
                                <div class="modal-header">
                                    <h1 class="modal-title fs-5" id="addmodalLabel">Ajouter</h1>
                                    <button type="button" class="btn-close" data-bs-dismiss="modal"
                                        aria-label="Close"></button>
                                </div>
                                <form class="form-floating" method="POST" action="" @click.prevent>

                                    <div class="modal-body">

                                        <label class="p-2">ID</label>
                                        <input type="number" class="form-control" name="id" id="id" v-model="id" >

                                        <label class="p-2">Nom</label>
                                        <input type="text" class="form-control" name="nom" id="nom" v-model="nom"
                                            placeholder="votre nom" >

                                        <label class="p-2">Prenom</label>
                                        <input type="text" class="form-control" name="prenom" id="prenom" v-model="prenom"
                                            placeholder="votre prenom"  >
                                            
                                        <label class="p-2">Email</label>
                                        <input type="email" class="form-control" name="email" id="email" v-model="email"
                                            placeholder="email@gmail.fr"  >

                                        <label class="p-2">Classe</label>
                                        <input type="text" class="form-control" name="classe" id="classe" v-model="classe"
                                            placeholder="MDW - DSI"  >

                                        <label class="p-2">Moyenne</label>
                                        <input type="number" class="form-control" name="moyenne" id="moyenne" v-model="moyenne"
                                            placeholder="Moyenne"  >
                                        <br>
                                        <span class="alert alert-success" role="alert"> {{msg}}</span>
                                        <div class="modal-footer m-2">
                                            <button type="button" class="btn btn-danger"
                                                data-bs-dismiss="modal">Annuler</button>
                                            <button type="submit" @click="addEt()"  class="btn btn-success" id="submit">Ajouter</button>
                                        </div>
                                    </div>
                                </form>
                            </div>
                        </div>
                    </div>
                </div>
<table class="table caption-top">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Nom</th>
      <th scope="col">Prenom</th>
      <th scope="col">Email</th>
      <th scope="col">Classe</th>
      <th scope="col">Moyenne</th>
    </tr>
  </thead>
  <tbody>

    <tr v-for="et of etudients" :key="et.id">
      <th scope="row">{{ et.id }}</th>
      <td>{{ et.nom }}</td>
      <td>{{ et.prenom }}</td>
      <td>{{ et.email }}</td>
      <td>{{ et.classe }}</td>
      <td>{{ et.moyenne }}</td>
    </tr>
   
  </tbody>
</table>

</div>
</div>
</section> 
</template>



<script>
import axios from "axios";

export default {
    name:'tab',
    data() {
        return {
        etudients: [{
            "id": "",
            "nom": "",
            "prenom": "",
            "email": "",
            "classe":"",
            "moyenne": "",
            }],

            "id": "",
            "nom": "",
            "prenom": "",
            "email": "",
            "classe":"",
            "moyenne": "",
            "msg" : ""
        };
    },
    
    async mounted(){
        let res= await axios.get('http://localhost:3000/etudients')
        this.etudients=res.data;
    },
    methods: {
        async getEt(){
        let res= await axios.get('http://localhost:3000/etudients')
        this.etudients=res.data;
    },
    async addEt() {
                let result = await axios.post('http://localhost:3000/etudients', 
                {
                    id: this.id,
                    nom: this.nom,
                    prenom: this.prenom,
                    email: this.email,
                    classe: this.classe,
                    moyenne: this.moyenne,
                });
                if(result.status == 201){
                     this.msg = "utilisateur ajouté";
                    this.nom="";
                    this.email="";
                    this.prenom="";
                   
                    this.getEt();
                }
                else{
                    this.msg = "utilisateur non ajouté";
                }
            }
            
        },
};
</script>
