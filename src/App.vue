<template>
   <div id="app">
  <!--   <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/> -->
     
    <h1>Hiu's Book Shop</h1>
    <label>Search:</label>
    <input v-model="searchBooks" placeholder="Enter the Book Name"/>
      <div v-if="isLoading">
        <p>Wait</p>
      </div>
      <div v-else>
        <BooksComponent :BooksComponent="filterTheBook"/>
      </div>
  

  </div>
</template>

<script>
import BooksComponent from "@/components/BooksComponent.vue";
export default {
  name: "app",
  data() {
    return {
      books: [],
      searchBooks:'',
      isLoading: true
    };
  },
  components: {
    BooksComponent
  },
     computed: {
        filterTheBook() {
      //     const mySearch = this.searchBooks
      //     console.log("nami: " + mySearch);
      // return this.books.filter(function(book) {
      //   console.log("hiu: " + JSON.stringify(book));
      //   let matchTheBook = new RegExp('(' + mySearch + ')', 'i');
      //     console.log("nami: " + matchTheBook);
      //   return book.titulo.match(matchTheBook);
      let bookSearch= this.searchBooks;
          if(bookSearch==''){
            
            return this.books;
            console.log(this.books)
          }else { return this.books.filter(allBooks=>allBooks.titulo.toLowerCase().includes(bookSearch.toLowerCase()))

          // data.filter(book => book.titulo.toLowerCase().includes(searchtxt.toLowerCase()))
          console.log(bookSearch + "test")}
        
         }

      }
    ,
 
  created() {
    this.getFetch();
  },
  methods: {
    getFetch: function() {
      fetch("https://api.myjson.com/bins/udbm5", {
        method: "GET"
      })
        .then(response => {
          return response.json();
        })
        .then(data => {
          this.books = data.books;
          console.log(this.books);
          this.isLoading = false;
        });
    }
  }
};
</script>



<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}
#nav a {
  font-weight: bold;
  color: #2c3e50;
}
#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
