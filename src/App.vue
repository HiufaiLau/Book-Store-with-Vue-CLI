<template>
   <div id="app">
  <!--   <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/> -->
     
    <h1>Hiu's Book Shop</h1>
    <span>Search by title :</span>
<input v-model="searchBook" placeholder="Enter the book name"/>
    
  

     
  
    
      <div v-if="isLoading">
        <p>Wait</p>
      </div>
      <div v-else>
        <BooksComponent :passingAllBooks="filterTheBooks"/>
      </div>
  

  </div>
</template>

<script>
import BooksComponent from "@/components/BooksComponent.vue";
import OneBookComponent from "@/components/OneBookComponent.vue";
export default {
  name: "app",
  data() {
    return {
      books: [],
      searchBook:'',
      isLoading: true
    };
  },
  components: {
    BooksComponent,
    OneBookComponent
  },
  computed: {
		filterTheBooks() {
      var searchOneBook = this.searchBook;
			if (searchOneBook== "") {
        return this.books;
        console.log("Hiu" + this.books);
			} 
				// console.log(this.searchWords);
				return this.books.filter(book => book.titulo.toLowerCase().includes(searchOneBook.toLowerCase()));
		}
	},
 
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
