<template>
  <div class="home">
      <Productos></Productos>
  </div>
</template>

<script>
// @ is an alias to /src
import Productos from '../components/Productos'

export default {
  name: 'home',
  components: {
    Productos
  }
}
</script>
