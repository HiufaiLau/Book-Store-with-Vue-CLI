<template>

<div class="book_container ">
    <div class="flip-container" ontouchstart="this.classList.toggle('hover');">	
		<div class="flipper d-flex flex-wrap mb-3 align-items-center justify-content-start">
      <div class="front">
         <img class="oneImage " :src="passingOneBook.portada" height="350" width="280">
      </div>
      <div class="back">
          <h4>{{passingOneBook.titulo}}</h4>
          <p>{{passingOneBook.descripcion}}</p>
          <!-- <button v-on:click="passingOneBook.portada">More Info</button> -->
            <button id="show-modal"  class="btn btn-outline-success" @click="showModal = true">More Info</button>
        
      </div>
		</div>
    
    </div>
     <!-- use the modal component, pass in the prop -->
  <Modal v-if="showModal" @close="showModal = false">
    <!--
      you can use custom content here to overwrite
      default content
    -->
    <h3 slot="header"> <img class="oneImage" :src="passingOneBook.detalle" height="350" width="330"></h3>
  </Modal>
  
  </div>

</template>

<script>
import Modal from '@/components/Modal.vue'
export default {
  name: "oneBook",
  data(){
    return {showModal: false}
  },
  components:{Modal},
  props: ["passingOneBook"],
  mounted() {
    console.log(
      "This log is from one component " + this.passingOneBook.portada
    );
  },

  methods: {
  }
};
</script>

<style>
/* entire container, keeps perspective */
.flip-container {
	perspective: 1000px;
}
	/* flip the pane when hovered */
	.flip-container:hover .flipper, .flip-container.hover .flipper {
		transform: rotateY(180deg);
	
	}

.flip-container, .front, .back {
	width: 300px;
	height: 390px;
	margin-bottom: -6%;
}

/* flip speed goes here */
.flipper {
	transition: 0.6s;
	transform-style: preserve-3d;

	position: relative;
}

/* hide back of pane during swap */
.front, .back {
	backface-visibility: hidden;

	position: absolute;
	top: 0;
	left: 0;
}

/* front pane, placed above back */
.front {
	z-index: 2;
	/* for firefox 31 */
	transform: rotateY(0deg);
}

/* back, initially hidden pane */
.back {
	transform: rotateY(180deg);
}


#modal-body img{
	margin-bottom: 5%;
	margin-top: 5%;
	margin-left: 6%;
	border-radius: 15px;
	width: 440px;
	height: 480px;
}


.flip-container{
	margin-left: 9%;

	
}

.line{
	margin-top: 0%;
}

input{
	/* margin-left:-3%;  */
}


</style>