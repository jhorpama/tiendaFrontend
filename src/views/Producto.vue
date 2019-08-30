<template>
  <div>
      <CrearProducto></CrearProducto>
  </div>
</template>
<script>
 import CrearProducto from '../components/CrearProducto'
 export default{
     name: 'Producto',
     components: {
         CrearProducto
     },
     data() {
         return {

         }
     }
 }
</script>