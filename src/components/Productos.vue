<template>
    <div>
         <b-navbar variant="dark" type="light">
            <b-navbar-brand>Productos</b-navbar-brand>
         </b-navbar>
        <b-container>
            <b-row>
                <b-col md="12">
                   <b-card bg-variant="dark" text-variant="white" v-for="producto in productos" :key="producto._id" no-body class="overflow-hidden mt-5">
                        <b-row no-gutters>
                        <b-col md="6">
                            <b-card-img :src="`http://localhost:3000${producto.path}`" class="rounded-0"></b-card-img>
                        </b-col>
                        <b-col md="6">
                            <b-card-body :title="`${producto.titulo}`">
                            <b-card-text>
                                
                                 <h2 style="font-size: 20px; font-weight: bold; color: #e20613;">Especificaciones</h2>
                                 <p>{{producto.descripcion}}</p>
                                {{producto.precio}}
                            </b-card-text>
                            </b-card-body>
                            <b-button variant="success">Ver detalle</b-button>
                            <b-button class="ml-1" variant="primary">Agregar el carrito</b-button>
                        </b-col>
                        </b-row>
                    </b-card>
                </b-col>
            </b-row>
        </b-container>
    </div>
</template>
<script>
  const axios = require('axios');
  export default{
      name: 'Productos',
      data() {
          return {
            productos: [],
          }
      },
      mounted() {
          axios.get('https://api-store-new.herokuapp.com/api/productos')
               .then(res => {
                   console.log(res);
                   this.productos = res.data;
               }).catch(err => {
                   console.log(err);
               })
      },
  }
</script>