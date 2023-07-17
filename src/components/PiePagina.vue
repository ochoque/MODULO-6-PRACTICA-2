<template>
   <footer :style="'background-color:' + configuracionPagina.footerColor">
    
    PIE DE PAGINA
    
    </footer>
</template>
    
    <script>
    export default {
      name: 'PiePagina',
      data() {
          return {
              configuracionPagina:{
                 
                  footerColor: "slategrey",
                 
                 },
  
              }
          }
      
  }
    </script>
