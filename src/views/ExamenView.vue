<template>
    <div class="examen">
        <label for="nombre">Nombre: <input type="text" class="campotexto" id="nombre" v-model="nombre"></label>
        <br>
        <label for="email">Email: <input type="text" class="campotexto" id="email" v-model="email" @blur="validarEmail"></label><label for="error" class="error" v-if="emailerror">{{ emailerror }}</label>
        <br>
        <label for="contrasena">Contrasena: <input type="text" class="campotexto" id="contrasena" v-model="contrasena" @keypress="validarContrasena"></label>
        <br>
        <button id="botonciego" @click="nuevoAlumno">Nuevo Alumno/a</button>
        <br>
        <br>
        <tr v-for="(perfil, index) in perfil " :key="index">
        

            <td>{{ perfil.nombre }}</td>
            <td>{{ perfil.email }}</td>
            <td>{{ perfil.contrasena }}</td>
            
        
        </tr>
    </div>
</template>
  
<script>


export default {
    name: 'ExamenView',
    data() {

        return {

            perfil:[],
            nombre: '', 
            email: '',
            emailerror: '',
            contrasena: '',
            contrasenaerror: '',
            perfilNuevo:{ nombre: '', email: '', contrasena: ''},

            

            

        };

    },

    methods: {

        validarEmail() {
            
            let emailPattern = /^[^\s@]+@[^\s@]+.[^\s@]+$/;
            if (!emailPattern.test(this.email)) {

                this.emailerror = 'mal';

            }else{

                this.emailerror = '';

            
            }
        },


        validarContrasena() {

            let botoncito = document.getElementById("botonciego");
            let contrasenaPattern = /^[a-zA-Z0-9]{8,}$/;
            if (!contrasenaPattern.test(this.contrasena)) {

                botoncito.style.display = "none";
                console.log("hola");
            }else{

                botoncito.style.display = "block";

            
            }
        },  


        nuevoAlumno() {

             this.perfilNuevo.nombre = this.nombre;
             this.perfilNuevo.email = this.email;
             this.perfilNuevo.contrasena = this.contrasena;
            this.perfil.push(this.perfilNuevo);

             this.nombre = '';
             this.email = '';
             this.contrasena = '';
            

            console.log(this.perfil);
            this.validarContrasena();

        },

    

    }
}
</script>

<style>
#botonciego {

    display: none;
}

.error{

    color: red;

}
</style>