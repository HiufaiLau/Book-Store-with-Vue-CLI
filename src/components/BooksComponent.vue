<template>

  <div class="book_container d-flex flex-wrap ">
    <OneBookComponent 
      v-for="(singleBook, index) in passingAllBooks"  
      :passingOneBook="singleBook"
      :key="index"/>
      
  
  <!-- <div class="front">
  <img :src="passingOneBook.portada" height="380" width="330">
  </div>
  <div class="back">
    <h4>{{passingOneBook.titulo}}</h4>
    <p>{{passingOneBook.descripcion}}</p>
     <button v-on:click="passingOneBook.portada">More Info</button>
</div>
  </div> -->
  </div>
  
</template>

<script>

import OneBookComponent from '@/components/OneBookComponent.vue'
export default {
  name: 'books',
  props: ['passingAllBooks'],
  components: {
    OneBookComponent
  },
  
  mounted(){
    console.log(this.books)
  }
/*   created() {
    getBookList();
  },
  methods: {
    getBookList: function() {
      console.log(books)
    }
  } */
}
</script>