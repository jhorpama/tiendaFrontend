<template>
   <div>
     <b-navbar variant="dark" type="light">
       <b-navbar-brand>Sesion de productos</b-navbar-brand>
     </b-navbar>
     <b-card class="mt-5">
        <b-form-group label="Producto">
          <b-form-file @change="cargarImagen"></b-form-file>
        </b-form-group>
        <b-form-group label="Titulo" description="titulo del producto">
             <b-form-input
             v-model="titulo"
             type="text"
             required
             placeholder="titulo del producto"
             ></b-form-input>
        </b-form-group>
        <b-form-group label="Descripcion" description="descripcion del producto">
             <b-form-input
             v-model="descripcion"
             type="text"
             required
             placeholder="descripcion del producto"
             ></b-form-input>
        </b-form-group>
        <b-form-group label="Precio" description="Precio del producto">
             <b-form-input
             v-model="precio"
             type="number"
             required
             placeholder="precio del producto"
             ></b-form-input>
        </b-form-group>
        <b-button variant="outline-primary" @click="subirImagen">Agregar producto</b-button>
     </b-card>
     <b-progress v-if="estado" class="mr-5 ml-5 mt-5" :value="value" :max="max" show-progress animated></b-progress>
   </div>
</template>
<script>
  const axios = require('axios');
  export default{
      name: 'CrearProducto',
      data() {
          return {
            titulo: null,
            descripcion: null,
            imagen: null,
            value: 1,
            max: 100,
            estado: false,
            precio: null,
          }
      },
      methods: {
        cargarImagen(e){
           const type = e.target.files[0].type;
           if(type === 'image/jpeg' || type === 'image/png') {
             this.imagen = e.target.files[0];
           }else{
             console.log('Este formato no es valido');
           }
           console.log(this.imagen);
        },
        subirImagen() {
            const email = 'administrador@gmail.com';
            const name = 'administrador';

            const fd = new FormData();

            fd.append('image', this.imagen);
            fd.append('email', email);
            fd.append('name', name);
            fd.append('titulo', this.titulo);
            fd.append('descripcion', this.descripcion);
            fd.append('precio', this.precio);
             
            axios.post('http://localhost:3000/api/producto', fd, {
              onUploadProgress: ProgressEvent => {
                this.estado = true
              }
            }).then(res => {
              this.imagen = null;
              this.estado = null;
              this.titulo = null;
              this.descripcion = null;
              this.precio = null;
              console.info(res);
            }).catch(err => {
              console.error(err);
            });
            
            console.log('subiendo');
        }
      },
  }
</script>