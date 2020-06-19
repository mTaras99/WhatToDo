<!--v-for wyglada tylko jakby byl napisany oddzielnie ale musi w czyms byc
akurat tutaj jest w komponencie planing,bo go zdefiniowalem w planing.vue-->
<!--odwolujesz sie do jakiejs funkcji, zaczynaj od malpy @@@@, jednej-->
<!--v-for dziala jak for.each, po przecinku w nawiasie jest index
bo chcemy indexowac, dla kazdego eventu nadajemy klucz tak jak sie robi w zwyklej petli-->
<!--Modal tak jak wszystko zawsze w divie ograniczacym go od template
jeszcze raz JEDEN GLOWNY DIV NA WSZYSTKO-->
<template>
  <mdb-container>
    <mdb-row>
      <mdb-col col="9">
        <planing
        v-for="(event,index) in planing"
        :time="event.time"
        :title="event.title"
        :location="event.location"
        :description="event.description"
        :key="index"
        @delete="handleDelete"
        />
      <mdb-row>
      <mdb-col xl="3" md="6" class="mx-auto text-center">
        <mdb-btn @click.native="modal=true" color="info">Add Event</mdb-btn>
      </mdb-col>
      </mdb-row>
    </mdb-col>
      <mdb-col col="3">
          <h3 class="text-uppercase my-3">Schedule</h3>
          <h6 class="my-3">
              It's going to be chilly today. You have
              <b>{{planing.length}} events</b> today but take it easy.
          </h6>
          <h1 class="my-3">
            <mdb-row>
              <mdb-col col="3" class="text-center">
                <mdb-icon far icon="sun"/>
              </mdb-col>
              <mdb-col col="9">Sunny</mdb-col>
            </mdb-row>
            <mdb-row>
              <mdb-col col="3" class="text-center">
                <mdb-icon icon="thermometer-three-quarters"/>
              </mdb-col>
              <mdb-col col="9">25°C</mdb-col>
            </mdb-row>
          </h1>
        <p>
          Don't forget to put a smile on your face,
          becoming big sunshine and you have to be happy
          when it will become.
        </p>
      </mdb-col>
    </mdb-row>
    <mdb-modal v-if="modal" @close="modal = false">
      <mdb-modal-header>
        <mdb-modal-title tag="h4" class="w-100 text-center font-weight-bold">Add new event</mdb-modal-title>
      </mdb-modal-header>
      <mdb-modal-body>
      <form class="mx-3 grey-text">
        <mdb-input
          name="time"
          label="Time"
          icon="clock"
          placeholder="19:00"
          type="text"
          @input="handleInput($event, 'time')"
        />
        <mdb-input
          name="title"
          label="Title"
          icon="edit"
          placeholder="Chillin"
          type="text"
          @input="handleInput($event, 'title')"
        />
        <mdb-input
          name="location"
          label="Location (optional)"
          icon="map"
          type="text"
          @input="handleInput($event, 'location')"
        />
        <mdb-Textarea
          name="description"
          label="Description"
          icon="sticky-note"
          @input="handleInput($event, 'description')"
        />
      </form>
      </mdb-modal-body>
      <mdb-modal-footer class="justify-content-center">
        <mdb-btn @click.native="addEvent" color="info">Add</mdb-btn>
      </mdb-modal-footer>
    </mdb-modal>
    
  </mdb-container>
</template>
<!--Funkcje dodawaj w metodach, wrzucajac je po prostu do scriptu nie zadzialaja-->
<script>
import {mdbContainer, mdbCol, mdbRow,mdbIcon,mdbBtn, mdbModal, mdbModalHeader, mdbModalTitle, mdbModalBody, mdbModalFooter, mdbInput, mdbTextarea} from "mdbvue";
import planing from "./components/planing";
export default {
  name: "App",
  components: {
    mdbContainer,
    mdbRow,
    mdbCol,
    mdbIcon,
    mdbBtn,
    mdbModal,
    mdbModalHeader,
    mdbModalTitle,
    mdbModalBody,
    mdbModalFooter,
    mdbInput,
    mdbTextarea,
    planing
  },
  data(){
    return{
      planing: [
        {
          time: "9:00",
          title:"wake up",
          location:"home",
          description:"Rozpoczecie dnia"
        },
        {
          time: "9:00-14:00",
          title:"learning",
          description:"Odin project"
        },
        {
          time: "14:00",
          title:"lunch",
          location:"hommy",
          description:"spaghetti carbonara"
        },
        {
          time: "15:00",
          title:"skate",
          location:"orient",
          description:"some triczki"
        },
        {
          time: "17:00",
          title:"meeting with lukasz",
          location:"Warszawa",
          description:"Chess, philozophy, beeeers"
        },
        {
          time: "21:00",
          title:"Gothic art gallery",
          location:"Warszwa",
          description:"Some fun with nostalgy"
        },
        {
          time: "23:00",
          title:"learning",
          location:"Hommy erectus",
          description:"ODIN ADIN"
        }
      ],
      modal: false,
      newValues: []
    };
  },
  methods: {
    handleDelete(eventIndex){
      this.planing.splice(eventIndex, 1)
    },
    handleInput(val,type){
      this.newValues[type] = val;
      console.log(this.newValues);
    },
    addEvent() {
      this.planing.push({
        time: this.newValues["time"],
        title: this.newValues["title"],
        location: this.newValues["location"],
        description: this.newValues["description"]
      });
    }
  }
  
}
</script>
<!--Dlaczego modal jest tam jeszcze nie doszedlem
ale chyba po prostu zwraca modal jako modal false i jest gites
moze modal mozna tak zapisac bo zawsze na poczatku zwraca false 
a po prostu trzeba go zdefiniowac?--> 
<!--pushuj z tymi nawiasami {}-->
<style>

</style>