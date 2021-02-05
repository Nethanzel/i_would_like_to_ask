<template>
    <div class="overview">
        <h1>Alcance logrado</h1>
        <p>En términos generales, el estado del proyecto se podria resumir en el siguiente gráfico, donde 
          <span id="reached">■</span> representa el alcance logrado y <span id="rest">■</span> representa lo que falta por lograr.</p>
        <cirChart :styles="cirChartStyles" v-bind:progress="summary[0]" />
        <p>Siendo un poco más especifico, el objectivo es alcanzar <strong>{{max}} personas</strong> en cada provincia del país, aqui podras ver 
          la evolución del alcance en cada lugar:
        </p>
        <barsChart :styles="barChartStyles" v-bind:data="summary[1]" />
        <p>Esta información se actualizará cada 5 minutos.</p>
    </div>
</template>

<script>
import axios from 'axios'
import barsChart from '@/components/barsChart.vue'
import cirChart from '@/components/cirChart.vue'

export default {
  components: {
    barsChart,
    cirChart
  },

  data() {
    return {
      summary: []
    }
  },

  created() {
    this.getData()
    setInterval(() => {this.getData()}, 300000)
  },

   computed: {

     barChartStyles() {
      return {
        height: '1100px',
        width: '98vw',
        'min-width': '360px',
        'max-width': '1366px',
        'align-self': 'left',
        'margin-right': 'auto'
      }
    },

    cirChartStyles() {
      return {
        height: '30vh',
        width: '30vw',
        'align-self': 'center',
        'margin-top': '5px',
        'min-width': '350px',
        'min-height': '350px'
      }
    },

    max() {
      try {
       if(this.summary[1][1][1]) {
         return parseInt(this.summary[1][1][0])
       }
        return parseInt(this.summary[1][1][0])
      } catch (error) {
        return 0
      }
    }
   },
   methods: {

      getData() {
        let token = this.clienttoken()
        axios.get("/api/summary", {headers: {"token": token}})
        .then(res => {
          this.summary = res.data.data
        })
        .catch(err =>{
          let e = String(err).toLowerCase()
          if(e.includes("network error")) {
              this.messageBox("Servidor fuera de alcance.", 2)
          } else if (e.includes("code 401")) {
              this.messageBox("Autenticación requerida o invalida.", 0)
          } else if (e.includes("code 404")) {
              this.messageBox("Solictud invalida.", 0)
          } else if(e.includes("code 500")) {
              this.messageBox("Estamos teniendo algunos problemas con el servidor.", 2)
          } else {
            this.messageBox("Error desconocido.", 0)
          }
        })
    }
   }
}
</script>

<style scoped>

.overview {
  display: flex;
  flex-direction: column;
}

p {
  text-align: center;
}

h1 {
  text-align: center;
}

#reached {
  color: rgba(83, 255, 120, 0.75);
  font-size: 30px;
}


#rest {
  color: rgba(50, 150, 50, 0.35);
  font-size: 30px;
}


@media only screen and (max-width: 750px) {
  .overview {
    height: auto;
    cursor: default;
    padding-top: 10vh;
  }

   p {
     font-size: 17px;
      margin: 10px 5px 10px 5px;
  }

  h1 {
    margin: 0 0 10px 0;
  }

}

@media only screen and (min-width: 751px) {
  .overview {
    height: auto;
    cursor: default;
    margin: 0 0px 15px 0px;
    padding-top: 8vh;
  }

  p {
    margin: 10px 5px 10px 5px;
    font-size: 19px;
  }

  h1 {
    margin: 0 0 15px 0;
  }
}
</style>