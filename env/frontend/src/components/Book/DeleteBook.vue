<template lang="html">
<div>
  <div class="container">
     <div class="row">
          <div class="col">

<h3> ¿Estás seguro que deseas eliminar este disco?</h3>
<p> Disco : {{ this.element.title }}</p>
<p> Artista : {{ this.element.description }}</p>
<p> Código : {{ this.element.album }}</p>
    </div>
        </div>
              </div>

    <div class="row">
    <div class="col">

    <b-button v-on:click="deleteBook" variant="danger">Eliminar</b-button>

    </div>

    </div>
</div>

</template>


<script>
import axios from 'axios';
import swal from 'sweetalert'


export default {
  data () {
    return {
    bookId: this.$route.params.bookId,
      element: {
        title: '',
        description: '',
        album: ''
  }
   }

    },
    methods: {
    getBook (){
        const path = `http://localhost:8000/api/v1.0/books/${this.bookId}/`

        axios.get(path).then((response) => {

        this.element.title = response.data.title
        this.element.description = response.data.description
        this.element.album = response.data.album

        })

        .catch((error) => {
        console.log(error)

        })
    },

    deleteBook () {
      const path = `http://localhost:8000/api/v1.0/books/${this.bookId}/`

      axios.delete(path).then((response) => {
      location.href = '/books'
      })
      .catch((error) => {
      swal("No es posible eliminar el libro", "", "error")

      })
         }

            },

  created() {
    this.getBook()

}

}

</script>

<style lang="css" scoped>


</style>
