<template >
<div class="cajaMayor">
  <div class="tienda">

    <div >
      <h2 class="promociones">PROMOCIONES</h2>
      <div class="itemPadre" @click="agregarPedido" >
        <div class="item" v-for="arrayPane in arrayPanes" :key="arrayPane.id">
          <img src="https://www.bembos.com.pe/media/catalog/product/cache/1/thumbnail/172x148/9df78eab33525d08d6e5fb8d27136e95/p/r/promo-bembos-clasica.webp" width="200px" alt=""> 
          <p class="clasePan">{{arrayPane.name}}</p>
          <p >{{arrayPane.price}}</p>
        </div>
        
      </div>
    </div>
    
    <div id="guardarOrdenes" class="guardarOrden">
      <p class="tituloCajaOrdenes">Ordenes Pedidas</p>
      <div class="ordenesPedidas" v-for="OrdenCogida in OrdenCogidas" :key="OrdenCogida.id">
           <div>
              <p>{{OrdenCogida.tiposPan}}</p>
              <p>{{OrdenCogida.precios}}</p>
          </div>
          <span @click="eliminar" >
            <img class="btn" src="https://image.flaticon.com/icons/svg/1632/1632602.svg" width="20px" alt="">
          </span>
      </div>
    </div>

  </div>
</div>  
</template>

<script>
import axios from 'axios'

export default {
  name:'Tienda',
  data() {
    return {
      arrayPanes:[],
      OrdenCogidas:[]

    }
  },

  methods: {
    ingresarApi(){
      axios.get('https://api.myjson.com/bins/1008dw')
      .then(response=>{this.arrayPanes=response.data[0].category01
      
      console.log(this.arrayPanes)
      })
      
    },

        
    agregarPedido(e){
          class datosOrden{
          constructor(tiposPan){
            this.tiposPan=tiposPan;
            
            
          }
        }
        
        
        let seleccionarOrden=e.target.parentElement;
        let elemPnombre=seleccionarOrden.querySelector('.clasePan').textContent;
        let orden=new datosOrden(elemPnombre)

        this.OrdenCogidas.push(orden);
               
        
      },

    eliminar(e){
      if(e.target.classList.contains('btn')){
        e.target.parentElement.parentElement.remove();  
        console.log(e.target)
      }
      
    }  

},

  created() {
    this.ingresarApi()
  }
}
</script>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.cajaMayor{
  display: flex;
  justify-content: center;
}

.tienda{
  max-width: 1000px;
  height: 1000px;
  border: 1px solid #26419a;
  border-radius: 7px;
}

.promociones{
  max-width: 970px;
  height: 50px;
  border: 1px solid #26419a;
  border-radius: 7px;
  margin: 2px;
  background: #FFB500;
  color: #26419a;
  padding-top: 7px;
}

.itemPadre{
  display: flex;
  justify-content: space-around;
  
}

.item{
  width: 221px;
  height: 270px;
  border: 1px solid #FFB500;
  border-radius: 7px;
  margin: 15px;
  

}

.clasePan{
  font-family: 'Oswald', sans-serif;
  font-size: 17px;
  width: 200px;
  height: 33px;
  border: 1px solid #FFB500;
  border-radius: 7px;
  color: #26419a;
  margin: 13px auto;
}

.guardarOrden{
  width: 200px;
  height: 200px;
  border: 1px solid #FFB500;
  border-radius: 7px;
  position: fixed;
  overflow-x: hidden;
}

.ordenesPedidas{
  display: flex;
  width: 150px;
  height: 35px;
  border: 1px solid #FFB500;
  border-radius: 7px;
  color: #26419a;
  font-family: 'Oswald', sans-serif;
  margin: 5px;
  padding: 3px;
  justify-content: space-between;
}

.tituloCajaOrdenes{
  color: #26419a;
  font-family: 'Oswald', sans-serif;
  font-size: 17px;
}

</style>