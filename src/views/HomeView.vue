<template>
      <Menu/>
      <Producto/>
      <ProductosRelacionados/>
      <PiePagina/>
</template>

<script>
// @ is an alias to /src
import Menu from '@/components/Menu.vue'
import PiePagina from '@/components/PiePagina.vue'
import Producto from '@/components/Producto.vue'
import ProductosRelacionados from '@/components/ProductosRelacionados.vue'

export default {
  name: 'HomeView',
  
  components: {
    Menu,
    PiePagina,
    Producto,
    ProductosRelacionados
  }
}
</script>
