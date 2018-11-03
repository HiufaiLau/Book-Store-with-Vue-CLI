<template>

<div class="book_container d-flex flex-wrap mt-3 mb-3 align-items-center justify-content-start">
    <OneBookComponent 
      v-for="(singleBook, index) in passingAllBooks"  
      :passingOneBook="singleBook"
      :key="index"/>
    <div class="flip-container" ontouchstart="this.classList.toggle('hover');">	
		<div class="flipper d-flex flex-wrap  mt-3 mb-3 align-items-center justify-content-start">
      <div class="front">
         <img class="oneImage" :src="passingOneBook.portada" height="250" width="200">
      </div>
      <div class="back">
          <h4>{{passingOneBook.titulo}}</h4>
          <p>{{passingOneBook.descripcion}}</p>
          <button v-on:click="passingOneBook.portada">More Info</button>
      </div>
		</div>
    </div>
  </div>
  

</template>

<script>
export default {
  name: "oneBook",
  props: ["passingOneBook"],
  mounted() {
    console.log(
      "This log is from one component " + this.passingOneBook.portada
    );
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
	width: 320px;
	height: 480px;
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




</style>