<template>

  <div>
    <OneBookComponent 
      v-for="(singleBook, index) in passingAllBooks"  
      :passingOneBook="singleBook"
      :key="index"/>
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