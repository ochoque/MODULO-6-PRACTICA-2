<template>


<div class="container"  v-for="item in items" :key="item.id">
        <div class="row">
            <h3>{{item.nombre}}</h3>
        </div>
        <div class="row">
            <div class="col-12 col-sm-6 col-md-4 ">
                <img :src=item.imagen style="max-width:100%;width:auto;height:auto;">
            </div>
            <div class="col-12 col-sm-6  col-md-8">
            
               <h6 v-html="item.descripcion"></h6>
               <div class="p-3 mb-2 text-white" :style="precioEstilos">
                Precio: {{item.precio}} BOB 
            </div>
                <h5>Colores</h5>
                <div>
                    <div class="color-box clic" v-for="colorx in item.colores" :style="'background:'+ colorx" v-on:click="pedido.color=colorx" >{{pedido.color}}</div>
                    
                </div>
                
                <h5>Cantidad</h5>
                <div class="quantity">
                    
                    <button  v-on:click="pedido.cantidad--">-</button> <div>{{pedido.cantidad}}</div> 
                    <button v-on:click="pedido.cantidad++">+</button>
                </div>
                
                <div class="buy-box">
                    
                    <button type="button" class="btn btn-primary" v-if="pedido.cantidad > 0 && pedido.color !== null" enabled v-on:click.once="enviar()">Comprar</button>
                    <button type="button" class="btn btn-primary" v-else disabled>Comprar</button>
                </div>
                
            </div>
        </div>
    </div>



</template>
     
     <script>
     export default {

       name: 'Producto',
       data() {
        const api = process.env.VUE_APP_API;
           return {
            api,
            items:[],
            precioEstilos: "background: orangered; color: white; font-weight: bold; text-align:left;",
            pedido: {
                id:null,
                cantidad:1,
                color:null,
                },
               }
           },
    mounted() {
     this.getItems();
    },

    methods: {
    getItems() {

      this.axios({
      method: 'get',
      url:this.api + '/Productos?id=1'
      //url: "http://localhost:3000/Productos"
    })
    .then((response) => {
        this.items = response.data;
        console.log(response);
    })
    .catch((error) => { console.log(error) })
    .finally(() => { });
     },
      enviar(){
        this.pedido.id=1;
                alert("* id producto:" + this.pedido.id + "\n * cantidad producto: " + this.pedido.cantidad + " \n * color producto:" + this.pedido.color);
            }
       }
       
   }
     </script>
     
     <!-- Add "scoped" attribute to limit CSS to this component only -->
     <style scoped lang="scss">
          .color-box {
                   width: 40px;
                   height: 40px;
                   border-radius: 50%;
                   margin: 7px;
                   display: inline-block;
               }
   
               .clic{
                   cursor: pointer;
               }
   
               .quantity button{
                   border-radius: 50%;
                   display: inline-block;
                   width: 30px;
               }
               .quantity div{
                   text-align: center;
                   min-width: 30px;
                   display: inline-block;
                   font-weight: bold;
               }
               .buy-box{
                   margin: 20px;
               }
               footer {
                   
                   text-align: center;
                   padding: 30px 10px;
                   margin-top: 50px;
                   min-height: 100px;
               }
               .container{
                   margin-top: 50px;
                   justify-content: left;
               }
               .producto-relacionado-precio{
                   background: orangered;
                   color: white;
                   text-align: center;
                   padding: 10px; 
               }
               h3 {text-align: left}
               div { 
                justify-items: left;
                justify-content: left;
              }
     </style>