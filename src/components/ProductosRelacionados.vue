<template>

<div class="container"  >

<div class="row">
    <h4>Productos relacionados</h4>
</div>
    <div class="row" >
       
        <div class="col" v-for="producto in items" :key="producto.id" >
            <div class="card" style="width: 18rem;"  v-if="producto.id !=1">
            <div class="card-body">
                <h5 class="card-title">{{producto.nombre}}</h5>
                <img :src=producto.imagen style="max-width:100%;width:auto;height:auto;">
                <p class="card-text">{{producto.descripcion}}</p>
                    <div class="producto-relacionado-precio" >Precio:{{producto.precio}} BOB</div>
                <div>
                    <div>
                        <div class="color-box clic" v-for="colory in producto.colores" :style="'background:'+ colory"></div>
                    </div>
                    <div class="buy-box">
          
                    <button type="button" class="btn btn-primary" v-on:click.once="caracteristicas(producto.id,producto.nombre,producto.colores,producto.precio,producto.descripcion)">Caracteristicas</button>
                    
                </div>
                </div>
            </div>
        </div>
    </div>
  
    </div>
</div>    
    
    </template>
         
         <script>
         export default {
    
           name: 'ProductosRelacionados',
           data() {
            const api = process.env.VUE_APP_API;
               return {
                api,
                items:[],
                precioEstilos: "background: orangered; color: white; font-weight: bold",
                caracteristicasDron: {
                    id:null,
                    nombre:null,
                    colores:null,
                    precio:0,
                    descrip:""
                    },
                   }
               },
        mounted() {
         this.getItems1();
        },
    
        methods: {
        getItems1() {
    
          this.axios({
          method: 'get',
          url:this.api + '/Productos'
          //url: "http://localhost:3000/Productos"
        })
        .then((response) => {
            this.items = response.data;
            console.log(response);
        })
        .catch((error) => { console.log(error) })
        .finally(() => { });
         },
          caracteristicas(id,nombre,colores,precio,descrip){
            this.caracteristicasDron.id=id;
            this.caracteristicasDron.nombre=nombre;
            this.caracteristicasDron.colores=colores;
            this.caracteristicasDron.precio=precio;
            this.caracteristicasDron.descrip=descrip;
                    alert("* id producto:" + this.caracteristicasDron.id + "\n * nombre producto: " + this.caracteristicasDron.nombre + " \n * colores producto:" + this.caracteristicasDron.colores+ " \n * precio producto:" + this.caracteristicasDron.precio + " \n * descripcion producto:" + this.caracteristicasDron.descrip);
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
                       justify-content:space-between;
                   }
                   .producto-relacionado-precio{
                       background: orangered;
                       color: white;
                       text-align: center;
                       padding: 10px; 
                   }
         </style>