<template>
<div id="app">
<div class="container">
   <div class="logo">
    <img src="./assets/books.png" height="60" width="80">
     </div>
    <div class="title">
    <span>
     <h1 style="font-family: 'Baloo Bhaijaan', cursive;">Hiu's Book Shop</h1>
    </span>
    </div>
     <div class="searchBar">
    <span>Search by title :   </span>
    <input v-model="searchBook" placeholder="Enter the book name"/>     
    </div>
     <!-- <hr> -->
    <div class="booksBody">
      <div v-if="isLoading">
       <img src="./assets/lodaing.gif" height="60" width="80">
      </div>
      <div v-else>
        <BooksComponent :passingAllBooks="filterTheBooks"/>
      </div>
      <!-- <hr class="line"> -->
      </div>
</div>
<div class="card-footer text-center mt-3 mb-3 bg-secondary text-white rounded-0">
            &copy;2018 Ubiqum| All Rights reserved
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
      searchBook: "",
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
      if (searchOneBook == "") {
        return this.books;
        // console.log("Hiu" + this.books);
      }
      // console.log(this.searchWords);
      return this.books.filter(book =>
        book.titulo.toLowerCase().includes(searchOneBook.toLowerCase())
      );
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

.container {
  display: grid; 
	grid-template-columns: auto auto auto auto auto;
  /* grid-template-columns: 100px 600px auto; */
  grid-gap: 10px;
	padding: 30px;
}

.logo {
  grid-row: 1;
  grid-column: 1;
}
.title {
	grid-row: 1;
  grid-column: 2;
	display: flex;
	align-items: baseline;
}
.searchBar {
  grid-row: 1;
  grid-column: 3;
  display: flex;
	align-items: baseline;
}

.booksBody{
grid-row: 2;
  grid-column: 1/3;
}
/* hr{
  grid-row:2; 
} */

</style>
