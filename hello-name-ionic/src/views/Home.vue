<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Olá, Usuário! </ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content>
      <h2>Adivinhe o número que estou pensando</h2>

      <ion-grid>
        <ion-row>
          <ion-col>
            <ion-label>Número: </ion-label>  
          </ion-col>
        </ion-row>

        <ion-row>
          <ion-col>
            <ion-button v-on:click="numeroGerado = randomNumber(); contador = 0;" expand="block" > Gerar número </ion-button>  
          </ion-col>
        </ion-row>

        <ion-row>
          <ion-col>
            <ion-input type="text" id="numero" placeholder="Digite um número" v-model="numero"></ion-input>  
          </ion-col>
        </ion-row>


        <ion-row>
          <ion-col>
            <ion-button v-on:click="contador += 1" expand="block" @click="adivinhar()"> Acertei? </ion-button>  
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonGrid, IonRow, IonCol, IonLabel, IonInput, IonButton, alertController } from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonGrid,
    IonRow,
    IonCol,
    IonLabel,
    IonInput,
    IonButton
  },
  data(){
    return {
      numero: '',
      contador: 0,
      numeroGerado: ''
    }
  },
  methods: {

    randomNumber: function () {
      return Math.floor(Math.random() * (10 - 1 + 1)) + 1;
    },
    
    async adivinhar() {
      const numeroGerado = this.numeroGerado.toString()
        if (this.contador < 3){

          if (this.numero === numeroGerado){ 
            const alerta = await alertController
            .create({
              header: 'Acertou miseravi',
              subHeader: 'O número era: ' + numeroGerado,
              //message: 'Contador: ' + this.contador
            });
          await alerta.present();
          this.contador = 0;
        }
        else {
          const alerta = await alertController
          .create({
            header: 'Errou!',
            // message: 'Contador: ' + this.contador + ' Numero: ' + numeroGerado
          });
        await alerta.present();
        }
      }
      else {
            const alerta = await alertController
            .create({
              header: 'Errou 3x',
              subHeader: 'O número era: ' + numeroGerado,
              // message: 'Contador: ' + this.contador
            });
          await alerta.present();
          this.contador = 0;
      }
    }  
  }
});
</script>

<style scoped>
#container {
  text-align: center;
  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}

ion-input{
  border: 1px solid lightgrey;
  border-radius: 5px;
}
</style>
