<template>
  <div v-if="!logon">
    <headerV></headerV>
    <div v-if="registrado">
        <div class="container my-5 border rounded" style="width:550px; background-color: white">
            <div class="row">
                <div class="bg-primary col-12 text-center">
                    <h1 class="py-2 text-light">Ingreso al Sistema</h1>
                </div>
            </div>
            <div class="form-group text-center">
                <label for="email" class="my-2 cols-sm-2 control-label"><h5>Correo</h5></label>
                <div class="cols-sm-12">
                    <div class="input-group">
                        <span class="input-group-addon pt-2 px-3 bg-info" >
                            <i class="fa fa-envelope fa" aria-hidden="true"></i>
                        </span>
                        <input type="text" v-model="correo" class="form-control" id="email" name="email" placeholder="Ingrese el correo">
                     </div>
                </div>
            </div>
            <div class="form-group text-center">
                <label for="password" class="my-2 cols-sm-2 control-label"><h5>Contraseña</h5></label>
                <div lass="cols-sm-12 ">
                    <div class="input-group mb-3">
                        <span class="input-group-addon pt-2 px-3 bg-info">
                            <i class="fa fa-lock fa-lg" aria-hidden="true"></i>
                        </span>
                        <input v-model="clave" type="password" class="form-control" placeholder='Ingrese Contraseña' id="password" name="password">
                    </div>
                </div>
            </div>
            <div class="form-group text-center">
                <button type="button"  @click="ingresar" class="col-12 btn btn-primary my-2">Iniciar Sesión</button>
            </div>
            <div class="usuario_nuevo my-2">
                <a href="#" @click="registrado=false">¿No tienes una cuenta?</a>
            </div>
        </div>
    </div>
    <div v-else>
        <div id="login">
            <div class="container my-3 border rounded" style="width:550px; background-color: white">
                <div class="row">
                    <div id="titulo" class="bg-primary col-12 text-center">
                        <h1 class="py-2">Registro</h1>
                    </div>
                </div>
                <div class="form-group text-center">
                    <label for="name" class="my-2 cols-sm-2 control-label"><h5>Nombre</h5></label>
                    <div class="col-sm-12">
                        <div class="input-group mb-3">
                            <span class="input-group-addon pt-2 px-3 bg-info" >
                                <i class="fa fa-user" aria-hidden="true"></i>
                            </span>
                            <input type="name" placeholder="Ingrese nombre" id="name" name="name" class="form-control">
                        </div>
                    </div>
                </div>
                <div class="form-group text-center">
                    <label for="email" class="my-2 cols-sm-2 control-label"><h5>Correo</h5></label>
                    <div class="cols-sm-12">
                        <div class="input-group mb-3">
                            <span class="input-group-addon pt-2 px-3 bg-info">
                                <i class="fa fa-envelope fa" aria-hidden="true"></i>
                            </span>
                            <input class="form-control" v-model="correo" type="text" id="email" name="email" placeholder="Ingrese un correo válido">
                        </div>
                    </div>
                </div>
                <div class="form-group text-center">
                    <label for="password" class="my-2 cols-sm-2 control-label"><h5>Contraseña</h5></label>
                    <div class="cols-sm-12">
                        <div class="input-group mb-3">
                            <span class="input-group-addon pt-2 px-3 bg-info" >
                                <i class="fa fa-lock fa" aria-hidden="true"></i>
                            </span>
                            <input v-model="clave" type="password" class="form-control" placeholder="Ingrese una contraseña" id="password" name="password">
                        </div>
                    </div>
                </div>
                 <div class="form-group text-center">
                    <label for="password_verif" class="my-2 cols-sm-2 control-label"><h5>Repetir contraseña</h5></label>
                    <div class="cols-sm-12">
                        <div class="input-group mb-3">
                            <span class="input-group-addon pt-2 px-3 bg-info" >
                                <i class="fa fa-lock fa" aria-hidden="true"></i>
                            </span>
                            <input v-model="confirmClave" type="password" class="form-control" placeholder="Ingrese nuevamente la contraseña" id="password_verif" name="password_verif">
                        </div>
                    </div>
                </div>
                <div class="form group text-center">
                    <button @click="manejoClicks($event)" class="btn btn-primary col-12 my-2">Registrarse</button>
                </div>
                <div class="my-2">
                    <a href="#" @click="registrado=true">¿Ya tienes una cuenta?</a>
                </div>
            </div>
        </div>
    </div>
  </div>
  <div v-else>
    <headerV>
    </headerV>
    <div>
        <div class="text-center mt-4 mx-5">
           <div class=" row border rounded bg-info " >
                <h1 class="py-2 text-light">Lista de gastos <button v-if="mostrarLista" @click="mostrarLista=false" class=" btn bg-danger"><i class= "fa fa-minus"></i></button><button v-if="!mostrarLista"  @click="mostrarLista=true" class="btn bg-success"><i class="fa fa-plus"></i></button></h1>
            </div>
        </div>
        <div v-if="mostrarLista">
            <div  class="bg-light border rounded mt-3 mx-5">
                <div class="w-50  container mt-2 ">
                    <div class="componentes py-3">
                        <div class="form-group row mb-3">
                            <label for="nameInput" class="col-sm-3">Nombre del monto</label>
                            <div class="col-sm-9">
                                <input v-if="!editar" v-model='ingresoNombre' type="text" class="form-control" id="nameInput" placeholder="Ingrese el nombre del monto">
                                <input v-if="editar" v-model='nameModified' type="text" class="form-control" id="nameChange" placeholder="Ingrese el nuevo nombre del monto">
                            </div>
                        </div>
                        <div class="form-group row mb-3">
                            <label for="monto" class="col-sm-3">Monto del gasto</label>
                            <div class="col-sm-9">
                                <input v-if="!editar" v-model='ingresoMonto' type="number" class="form-control" id="monto" placeholder="Ingrese nombre del gasto">
                                <input v-if="editar" v-model='montoModified' type="number" class="form-control" id="montoChange" placeholder="Ingrese el nuevo monto">
                            </div>
                            </div>
                        <div class="form-group row mb-3">
                            <label for="type" class="col-sm-3">Tipo de Gasto</label>
                            <div class="col-sm-9">
                                <select v-if="!editar" v-model='ingresoTipo' class="form-select" aria-label="Default select example">
                                    <option value="Hogar">Hogar</option>
                                    <option value="Trabajo">Trabajo</option>
                                    <option value="Otros">Otros</option>
                                </select>
                                 <select v-if="editar" v-model='tipoModified' class="form-select" aria-label="Default select example">
                                    <option value="Hogar">Hogar</option>
                                    <option value="Trabajo">Trabajo</option>
                                    <option value="Otros">Otros</option>
                                </select>
                            </div>
                        </div>
                        <div class="form-group mt-4 text-center">
                            <button v-if="!editar" id="add" v-on:click="manejoClick($event)" class="btn bg-primary text-light">Agregar</button>
                            <button v-if="editar" id="edit" v-on:click="manejoClick($event)" class="btn bg-primary text-light">Actualizar</button>
                            <button v-if="editar" v-on:click="manejoClick($event)" id="cancelar" class="mx-1 btn bg-danger text-light">Cancelar</button>
                        </div>
                    </div>
                </div>
            </div>
            <div  class="border rounded mt-3 mx-5 bg-primary">
            <ul class="nav nav-tabs" id="myTab" role="tablist">
                <li class="nav-item" role="presentation">
                    <a v-bind:class='"nav-link text-dark "+mostrarTodo' id="todo" v-on:click="manejoClick($event)" data-bs-toogle="tab" href="#all">Todo</a>
                </li>
                <li class="nav-item">
                    <a v-bind:class='"nav-link text-dark "+mostrarHogar' id="hogar"  v-on:click="manejoClick($event)" data-bs-toogle="tab" href="#home">Hogar</a>
                </li>
                <li class="nav-item">
                    <a v-bind:class='"nav-link text-dark " +mostrarTrabajo' aria-selected="false" id="work" v-on:click="manejoClick($event)" href="#trabajo">Trabajo</a>
                </li>
                <li>
                    <a v-bind:class='"nav-link text-dark "+mostrarOtros' aria-selected="false" id="others" v-on:click="manejoClick($event)" href="#otros">Otros</a>
                </li>
                </ul>
            </div>
            <div class='row border-bottom border-primary lead font-weight-bold bg-light mx-5 mt-2 py-2'>
                    <div class='col-4 text-center'>Nombre del Gasto</div>
                    <div class='col-3 text-center'>Tipo de Gasto</div>
                    <div class='col-3 text-center'>Monto del Gasto</div>
                    <div class='col-2 text-center'>Accion</div>
            </div>
            <div class="tab-content bg-light mx-5">
                <div role="tabpanel" v-bind:class='"tab-pane fade show " +mostrarTodo ' id="all">
                    <div v-for="(gasto, index) in this.gastos" :key ="index" class='row lead py-2'>
                        <div class='col-4 text-center'>{{gasto.nombre}}</div>
                        <div class='col-3 text-center'>{{gasto.tipo}}</div>
                        <div class='col-3 text-center'>{{gasto.monto}}</div>
                        <div class='col-2 text-center'>
                            <div id='actualizar' class='btn btn-primary fa fa-pencil mx-2' v-on:click="manejoClick($event, idModified= gasto.id,)"></div>
                            <div id='eliminar' class='btn btn-primary fa fa-trash' v-on:click='manejoClick($event,idModified=gasto.id)'></div>
                        </div>
                    </div>
                </div>
                <div role="tabpanel" v-bind:class='"tab-pane fade show " + mostrarHogar' id="home">
                    <div v-for="(gasto, index) in gastosfiltersHogar" :key="index" class="row lead py-2">
                        <div class='col-4 text-center'>{{gasto.nombre}}</div>
                        <div class='col-3 text-center'>{{gasto.tipo}}</div>
                        <div class='col-3 text-center'>{{gasto.monto}}</div>
                        <div class='col-2 text-center'>
                            <div id='actualizar' class='btn btn-primary fa fa-pencil mx-2' v-on:click="manejoClick($event, idModified= gasto.id,)"></div>
                            <div id='eliminar' class='btn btn-primary fa fa-trash' v-on:click='manejoClick($event,idModified=gasto.id)'></div>
                        </div>
                    </div> 
                </div>
                <div role="tabpanel" v-bind:class='"tab-pane fade show " +mostrarTrabajo ' id="trabajo">
                    <div v-for="(gasto, index) in this.gastosfiltersTrabajo" :key ="index" class='row lead py-2'>
                        <div class='col-4 text-center'>{{gasto.nombre}}</div>
                        <div class='col-3 text-center'>{{gasto.tipo}}</div>
                        <div class='col-3 text-center'>{{gasto.monto}}</div>
                        <div class='col-2 text-center'>
                            <div id='actualizar' class='btn btn-primary fa fa-pencil mx-2' v-on:click="manejoClick($event, idModified= gasto.id)"></div>
                            <div id='eliminar' class='btn btn-primary fa fa-trash' v-on:click='manejoClick($event,idModified=gasto.id)'></div>
                        </div>
                    </div>
                </div>
                <div role="tabpanel" v-bind:class='"tab-pane fade show " + mostrarOtros' id="otros">
                    <div v-for="(gasto, index) in this.gastosfiltersOtros" :key ="index" class='row lead py-2'>
                        <div class='col-4 text-center'>{{gasto.nombre}}</div>
                        <div class='col-3 text-center'>{{gasto.tipo}}</div>
                        <div class='col-3 text-center'>{{gasto.monto}}</div>
                        <div class='col-2 text-center'>
                            <div id='actualizar' class='btn btn-primary fa fa-pencil mx-2' v-on:click="manejoClick($event, idModified= gasto.id)"></div>
                            <div id='eliminar' class='btn btn-primary fa fa-trash' v-on:click="manejoClick($event, idModified= gasto.id)"></div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="mx-5 mb-3 border-top border-primary bg-light">
                <div class=" py-2 row text-center lead ">
                    <div class="col-5 border-end border-dark">Total</div>
                    <div class="col-5">{{this.total}}</div>
                </div>
            </div>
            <div class="w-100 text-center my-3">
                <button id="logout" v-on:click="manejoClick($event)" class="btn btn-danger col-2"><span><i class="fa fa-sign-out fa-lg"></i></span></button>
            </div>
        </div>
    </div>
    </div>
</template>

<script>
import firebase from 'firebase/app' 
import 'firebase/firestore'
import "firebase/auth"


import "./assets/style.css"
import Swal from 'sweetalert2';
import headerV  from  "./components/Header.vue";

export default {
  name: 'App',
  data: function(){
    return{
        logon: false,
        coleccionRaiz:"usuario",
        firebase: "",
        db: "",
        editar: false,
        idModified: "",
        mostrarLista:true,
        ingresoNombre:"",
        ingresoMonto: "",
        ingresoTipo: "",
        mostrarTodo: "active",
        mostrarHogar: "",
        mostrarTrabajo:"",
        mostrarOtros:"",
        idUsuarios: "informacion",
        hogar: "hogar",
        otros: "otros",
        salud: "salud",
        trabajo: "trabajo",
        monto:"Monto",
        gastosfiltersHogar:[],
        gastosfiltersTrabajo:[],
        gastosfiltersOtros:[],
        total: 0,
        gastos: [],
        registrado: true,
        correo: "",
        clave: "",
        confirmClave:"",
        nameModified: "",
        montoModified:"",
        tipoModified: "",
    }
  },
  components: {
    headerV
  },
  beforeMount: function () {
    var config = {
      apiKey: "AIzaSyDL8YlNCnO-8gppEtBoGXmmfjwUXwuf7Dc",
      authDomain: "gastos-personales-2179c.firebaseapp.com",
      databaseURL: "https://gastos-personales-2179c-default-rtdb.firebaseio.com",
      projectId: "gastos-personales-2179c",
      storageBucket: "gastos-personales-2179c.appspot.com",
      messagingSenderId: "1062192265552",
      appId: "1:1062192265552:web:7ac26a0f281a3b40c71455",
      measurementId: "G-JVXX7DNP50"
    };
    this.firebase = firebase.initializeApp(config);
    console.log("Conectado a firebase app")
  },
  methods: {
    manejoClick: function (e) {
        if (e.target.id==='todo'){
        this.mostrarTodo='active'
        this.mostrarHogar=''
        this.mostrarTrabajo=''
        this.mostrarOtros = ""
        this.total = 0
        this.gastos.forEach((gasto) =>{
                this.total += parseInt(gasto.monto)
            })
        }
        else if (e.target.id==='hogar'){
        this.mostrarTodo=''
        this.mostrarHogar='active'
        this.mostrarTrabajo=''
        this.mostrarOtros = ""
        this.gastosfiltersHogar = this.gastos.filter(gastos => gastos.tipo === "Hogar")
        this.gastosfiltersHogar.map((gastos) =>{
            this.idGastos = gastos.id
            this.nameGasto = gastos.name
            this.tipoGasto = gastos.tipo
            this.montoGasto = gastos.Monto
            this.total = parseInt(gastos.Monto)
            })
        this.total = 0;
        this.gastosfiltersHogar.forEach((gasto) => {
            this.total += parseInt(gasto.monto);
            });
        }    
        else if(e.target.id==='work'){
        this.mostrarTodo=''
        this.mostrarHogar=''
        this.mostrarTrabajo='active'
        this.mostrarOtros = ""
        this.gastosfiltersTrabajo = this.gastos.filter(gastos => gastos.tipo === "Trabajo")
        this.gastosfiltersTrabajo.map((gastos) =>{
            this.idGastos = gastos.id
            this.nameGasto = gastos.nombre
            this.tipoGasto = gastos.tipo
            this.montoGasto = gastos.Monto
            this.total = parseInt(gastos.Monto)
            })
        this.total = 0;
        this.gastosfiltersTrabajo.forEach((gasto) => {
            this.total += parseInt(gasto.monto);
            });
        }
        else if(e.target.id==="others"){
        this.mostrarTodo=''
        this.mostrarHogar=''
        this.mostrarTrabajo=''
        this.mostrarOtros = "active"
        this.gastosfiltersOtros = this.gastos.filter(gastos => gastos.tipo === "Otros")
        this.gastosfiltersOtros.map((gastos) =>{
            this.idGastos = gastos.id
            this.nameGasto = gastos.nombre
            this.tipoGasto = gastos.tipo
            this.montoGasto = gastos.Monto
            this.total = parseInt(gastos.Monto)
            })
        this.total = 0;
        this.gastosfiltersOtros.forEach((gasto) => {
            this.total += parseInt(gasto.monto);
            });
        }
        else if (e.target.id === "add"){
            if(this.ingresoNombre === "" || this.ingresoMonto === null|| this.ingresoTipo === ""){
            Swal.fire({
                title: "Error",
                text: "Campos Obligatorios.",
                icon: "error",
                confirmButtonText: "Confirmar"
                });   
            }
            else{
                const gastoData = {nombre:this.ingresoNombre, tipo:this.ingresoTipo, Monto:this.ingresoMonto}
                console.log(this.ingresoNombre, this.ingresoMonto, this.ingresoTipo)
                this.db.add(gastoData).then((docReference) => {
                    this.gastos.unshift({id:docReference.id, nombre: gastoData.nombre, tipo: gastoData.tipo, monto: gastoData.Monto});
                    this.total += parseInt(gastoData.Monto);
                 }).catch((Error) => {
                    Swal.fire({
                        title: "Error",
                        text: "No se pudo agregar el gasto al sistema. Error: " + Error.message,
                        icon: "error",
                        confirmButtonText: "Confirmar"
                    });
                });
                    Swal.fire({
                        title: "Agregar",
                        text: "Gasto agregado correctamente.",
                        icon: "success",
                        confirmButtonText: "Confirmar"
                    });
            }
        }
        else if(e.target.id === "actualizar"){
            this.editar=true
        }
        else if(e.target.id === "edit"){
            if(this.nameModified === ""){
                Swal.fire({
                    title: "Error",
                    text: "Ingrese un nombre válido",
                    icon:"error",
                    confirmButtonText: "Confirmar"
                })
            }
            else if(this.tipoModified ===""){
                Swal.fire({
                    title: "Error",
                    text: "Seleccione un tipo de gasto",
                    icon:"error",
                    confirmButtonText: "Confirmar"
                })
            }
            else if(this.montoModified ===""){
                Swal.fire({
                    title: "Error",
                    text: "Ingrese un monto válido",
                    icon:"error",
                    confirmButtonText: "Confirmar"
                })
            }
            const editGasto = {name:this.nameModified, Monto: this.montoModified, tipo:this.tipoModified}
            
            this.db.doc(this.idModified).update(editGasto).then(()=>{
                Swal.fire({
                    title: "Éxito",
                    text: "Cambios efectuados",
                    icon: "success",
                    confirmButtonText: "Confirmar"
                })
                this.editar = false
                console.log(this.gastos)
                this.gastos =[]
                this.total = 0
                this.db.get().then((gastos)=>{
                gastos.forEach((gasto) => {
                this.gastos.push({id:gasto.id, nombre:gasto.data().nombre, tipo:gasto.data().tipo, monto:gasto.data().Monto});
                this.total += parseInt(gasto.data().Monto);
                    });
                });
            }).catch((error) =>{
                Swal.fire({
                    title: "Error",
                    text: "No se ha podido actualizar los elementos " + error,
                    icon: "error",
                    confirmButtonText: "Confirmar"
                })
            })
           
        }
        else if(e.target.id === "cancelar"){
            this.editar = false
            console.log(this.editar)
            console.log(this.gastos)
        }
        else if(e.target.id === "eliminar"){
            this.db.doc(this.idModified).delete().then(() => {
                Swal.fire({
                    title: "Éxito",
                    text: "Elemento eliminado satisfactoriamente",
                    icon: "success",
                    confirmButtonText: "Confirmar"
                })
                this.gastos =[]
                this.total = 0
                this.db.get().then((gastos)=>{
                gastos.forEach((gasto) => {
                this.gastos.push({id:gasto.id, nombre:gasto.data().nombre, tipo:gasto.data().tipo, monto:gasto.data().Monto});
                this.total += parseInt(gasto.data().Monto);
                    });
                });
            }).catch((error)=>{
                Swal.fire({
                    title: "Error",
                    text: "No se ha podido eliminar " + error,
                    icon: "error",
                    confirmButtonText: "Confirmar"
                })
            })
        }
        else if(e.target.id === "logout"){
            firebase.auth().signOut().then(() =>{
                console.log("Se cerro sesion")
                this.logon = false
            })
            
        }
    },
    manejoClicks: function (){
        if(this.clave === this.confirmClave && this.clave.length >6){
            this.firebase.auth().createUserWithEmailAndPassword(this.correo, this.clave)
            .then((response) => {
            console.log(this.correo, this.clave)
            console.log("Registro Correcto" + response.user.email + "Registro: "+ this.registro)
            this.correo = response.user.email;
            this.registrado = true;
            })
            .catch(function(error){
            var errorCode = error.code;
            var errorMessage = error.message;
            console.log("Error: " +errorCode + " - " + errorMessage)
            })
        }
        else if(this.clave.length < 6){
            console.log(this.confirmClave)
            Swal.fire({
                title: "Error",
                text: "La contraseña debe tener mas de 6 caracteres",  
                icon: "error",
                confirmButtonText: "Confirmar"
            })
        }
        else if (this.clave != this.confirmClave){
            console.log("Las contraseñas no coinciden");
            Swal.fire({
                title: "Error",
                text: "Las contraseñas no coinciden",
                icon: "error",
                confirmButtonText: "Confirmar"
            })
        }
    },
    ingresar: function(){
        console.log(this.correo, this.clave)
        this.firebase.auth().signInWithEmailAndPassword(this.correo, this.clave).then((response) =>{
        console.log('Ingreso correcto con User: '+response.user.email)
        this.$emit('ingresoCorrecto',response.user.email)
        this.logon =true;
        this.db = this.firebase.firestore();   
        const settings = {timestampsInSnapshots: true};
        this.db.settings(settings);
        const doc = this.db.collection(this.coleccionRaiz).doc("info")
        const gastos = doc.collection("gastos")
        this.db = gastos
        gastos.get().then((gastos)=>{
            gastos.forEach((gasto) => {
                this.gastos.push({id:gasto.id, nombre:gasto.data().nombre, tipo:gasto.data().tipo, monto:gasto.data().Monto});
                this.total += parseInt(gasto.data().Monto);
                    });
                });
            }).catch((error) => {
            var errorCode = error.code;
            var errorMessage = error.message;
            console.log('Error: '+errorCode+' - '+errorMessage);
               Swal.fire({
                title: "Error de autenticación",
                text: "El correo o la contraseña son incorrectos",
                icon: "error",
                confirmButtonText: "Confirmar"
                })
            })
        }
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.form-control{
    background-color: #F5F1F1 !important;
}
</style>
