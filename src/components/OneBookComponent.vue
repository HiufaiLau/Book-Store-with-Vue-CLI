<template>
<div>
  
  <div class="front">
  <img :src="passingOneBook.portada" height="380" width="330">
  </div>
  <div class="back">
    <h4>{{passingOneBook.titulo}}</h4>
    <p>{{passingOneBook.descripcion}}</p>
     <button v-on:click="passingOneBook.portada">More Info</button>
</div>
  </div>
  

</template>

<script>
export default {
  name: "oneBook",
  props: ["passingOneBook"],
  mounted() {
    console.log("This log is from one component " + this.passingOneBook.titulo);
  },

  methods: {
    // putImgInModal: function (event) {
    // }
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
	width: 350px;
	height: 480px;
}

/* flip speed goes here */
.flipper {
	transition: 0.6s;
	transform-style: preserve-3d;

	position: relative;
}
</style>