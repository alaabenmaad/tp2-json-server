
<script setup lang="ts"></script>

<template>

    <section class="container-fluid p-4">
        <div class="row dark">
            <div class="col-md-12">
                <div class="container-fluid p-4">
                    <span v-if="showMsg" class="alert alert-success" role="alert"> {{msg}} </span>
                    <h1>
                        <br>
                        Gestion Des Etudients
                        <br>
                    </h1>
                    <!-- Button trigger modal -->
                    <button type="button" class="btn btn-primary align-items-center pull-right m-2"
                        data-bs-toggle="modal" data-bs-target="#addmodal">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-plus-circle-fill" viewBox="0 0 16 16">
                            <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM8.5 4.5a.5.5 0 0 0-1 0v3h-3a.5.5 0 0 0 0 1h3v3a.5.5 0 0 0 1 0v-3h3a.5.5 0 0 0 0-1h-3v-3z"/>
                        </svg>
                         Ajouter un etudiant 
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
                                <form class="form-floating" method="POST" action="" >

                                    <div class="modal-body">

                                        <label class="p-2">Nom</label>
                                        <input type="text" class="form-control" name="nom" id="nom" v-model="nom"
                                            placeholder="votre nom" required >

                                        <label class="p-2">Prenom</label>
                                        <input type="text" class="form-control" name="prenom" id="prenom" v-model="prenom"
                                            placeholder="votre prenom" required >
                                            
                                        <label class="p-2">Email</label>
                                        <input type="email" class="form-control" name="email" id="email" v-model="email"
                                            placeholder="email@gmail.fr" required >

                                        <label class="p-2">Classe</label>
                                        <select name="classe" class="form-control"  v-model="classe">
                                            <option value="MDW" selected>MDW</option>
                                            <option value="DSI">DSI</option>
                                        </select>
                                        <label class="p-2">Moyenne</label>
                                        <input type="number" class="form-control" name="moyenne" id="moyenne" v-model="moyenne"
                                            placeholder="Moyenne" required >
                                        
                                        
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
      <th scope="col">Editer</th>
      <th scope="col">Supprimer</th>
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
      <td>
        <button type="button" class="btn btn-success align-items-center" data-bs-toggle="modal"
        v-bind:data-bs-target=editbs+et.id>
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-pencil-square" viewBox="0 0 16 16">
  <path d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"/>
  <path fill-rule="evenodd" d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"/>
</svg>
        </button>
        <!-- editModal -->
    
<div class="modal fade" v-bind:id=edit+et.id tabindex="-1"
                                    aria-labelledby="editmodalLabel" aria-hidden="true">
                                    <div class="modal-dialog">
                                        <div class="modal-content">
                                            <div class="modal-header">
                                                <h1 class="modal-title fs-5" id="editmodalLabel">Modifier</h1>
                                                <button type="button" class="btn-close" data-bs-dismiss="modal"
                                                    aria-label="Close"></button>
                                            </div>
                                            <form class="form-floating" id="editform" @click.prevent
                                                v-bind:key="et.id">
                                                <div class="modal-body">
                                                    <label class="p-2">id</label>
                                                    <input type="text" v-model=et.id class="form-control"
                                                        name="id" id="id" disabled>
                                                    <label class="p-2">nom</label>
                                                    <input type="text" v-model=et.nom class="form-control"
                                                        name="nom" id="nom" required>

                                                    <label class="p-2">prenom</label>
                                                    <input type="text" v-model=et.prenom class="form-control"
                                                        name="nom" required>


                                                    <label class="p-2">email</label>
                                                    <input type="email" v-model=et.email class="form-control"
                                                        id="email" name="email">
                                                    
                                                        <label class="p-2">Classe</label>
                                                        <select name="classe" class="form-control"  v-model="et.classe">
                                                            <option value="MDW" selected>MDW</option>
                                                            <option value="DSI">DSI</option>
                                                        </select>
                                                        
                                                        <label class="p-2">Moyenne</label>
                                                        <input type="number" class="form-control" name="moyenne" id="moyenne" v-model="et.moyenne"
                                                            placeholder="Moyenne" required >

                                                    <div class="modal-footer m-2">
                                                        <button type="button" class="btn btn-danger"
                                                            data-bs-dismiss="modal">Annuler</button>
                                                        <button type="submit" class="btn btn-success" id="submit"
                                                            v-bind:key="et.id"
                                                            v-on:click="updateEt(et.id,et.nom,et.prenom,et.email,et.classe,et.moyenne)">Confirmer</button>
                                                    </div>
                                                </div>
                                            </form>

                                        </div>
                                    </div>
                                </div>
      </td>
      <td>
        <button type="button" class="btn btn-outline-danger" data-bs-toggle="modal"
        v-bind:data-bs-target=rmbs+et.id>
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-trash-fill" viewBox="0 0 16 16">
  <path d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0z"/>
</svg>
        </button>
        <!-- Modal -->

        <div class="modal fade" v-bind:id=rm+et.id tabindex="-1"
                                    aria-labelledby="exampleModalLabel" aria-hidden="true">
                                    <div class="modal-dialog">
                                        <form class="form-floating" v-bind:key="et.id">

                                            <div class="modal-content">
                                                <div class="modal-header">
                                                    <h1 class="modal-title fs-5" id="exampleModalLabel"> <i
                                                            class="fa fa-warning text-danger fa-2x"></i></h1>
                                                    <button type="button" class="btn-close" data-bs-dismiss="modal"
                                                        aria-label="Close"></button>
                                                </div>

                                                <div class="modal-body">
                                                    voulez-vous supprimé l'etudiant {{et.prenom}} {{et.nom}}!
                                                </div>
                                                <div class="modal-footer">
                                                    <button type="button" class="btn btn-danger"
                                                        data-bs-dismiss="modal">Annuler</button>
                                                    <button type="submit" class="btn btn-outline-danger"
                                                        v-bind:key="et.id" v-on:click="deleteEt(et.id);">Supprimer<i
                                                            class="fa fa-trash"></i></button>
                                                </div>
                                            </div>
                                        </form>
                                    </div>
                                </div>
      </td>
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
            "msg" : "",
            "showMsg": false,
            editbs: "#editmodal",
            edit: "editmodal",
            rmbs: "#delete",
            rm: "delete"
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
                    this.msg = "L'etudiant "+this.prenom+" "+this.nom+" est ajouté avec succès";
                    this.nom = "";
                    this.prenom = "";
                    this.email = "";
                    this.classe = "";
                    this.moyenne = "";
                    this.showMsg = true;
                    this.getEt();
                }
                else{
                    this.msg = "etudiant non ajouté";
                }
            },
            
    async deleteEt(id) {
            axios.delete('http://localhost:3000/etudients/' + id);
            this.msg = "Etudiant supprimer avec succès";
            this.showMsg = true;
            this.getEt();
        },
        
    async updateEt(id,nom,prenom,email,classe,moyenne) {
        //   let rep=  await axios.get('http://localhost:3000/user/' + id);
        //   this.user= rep.data;
         let rep = await axios.put('http://localhost:3000/etudients/' + id , {nom:nom,prenom:prenom,email:email,classe:classe,moyenne:moyenne});
         if (rep.status == 201) {
                    this.msg = "Etudiant modifier avec succès";
                    this.showMsg = true;
                    
                }
                else {
                    this.msg = "erreur";
                }
                this.getEt();
        }
            
        },
};
</script>
