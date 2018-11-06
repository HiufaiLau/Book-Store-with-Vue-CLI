<template>
<div id="app" class="container">
<div class="row" style=" margin-top: 2%;">
   <div class="navbar col-1">
        <img src="./assets/books.png" height="60" width="80">
   </div>
    <div class="col-6" style=" padding-top: 20px;">
      <span>
        <h1 style="font-family: 'Baloo Bhaijaan', cursive;">Hiu's Book Shop</h1>
      </span>
    </div>
    <div class="col-2" style=" padding-top: 35px;">
       <span style="font-family: 'Poor Story', cursive;">Search by title :   </span>
    </div>
    <div class="col-1" style=" padding-top: 30px;">
       <form class="form-inline">
         <input class="form-control " v-model="searchBook" placeholder="Enter the book name"/>     
       </form>
    </div>
</div>    
     <hr class="footerline">

      <div v-if="isLoading">
       <img src="./assets/lodaing.gif" height="80" width="80">
      </div>
      <div v-else>
        <BooksComponent class="books" :passingAllBooks="filterTheBooks"/>
      </div>
      <!-- <hr class="line"> -->

<hr>
<div class="text-center mt-3 mb-3 rounded-0" style="font-family: 'Poor Story', cursive;">
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

.books{
  margin-left: 7%;
  /* margin-bottom: 3%; */
}

h1{
  margin-top: 3%;
}

/* .navbar{
	margin-left:7.5%;
	margin-top:3%;
} */
hr .footerline{
  margin-top:-1%;
}

</style>
