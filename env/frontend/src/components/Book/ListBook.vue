<template lang="html">
  <div class="container">
    <div class="row">
      <div class="col text-left">

      <div class="">

        <h2>Listado de Discos</h2>

        <b-button size="sm" :to="{name: 'NewBook'}" variant="primary">
            Nuevo Disco
            </b-button>

            </div>
            <br>

        <div class="col-md-12">
          <b-table striped hover :items="books" :fields="fields">
            <template slot="action" slot-scope="data">
              <b-button size="sm" variant="primary" :to="{ name:'EditBook', params: {bookId: data.item.id } }">
              Editar
              </b-button>
              <b-button size="sm" variant="danger":to="{ name:'DeleteBook', params: {bookId: data.item.id } }">
              Eliminar
              </b-button>

              </template>


            </b-table>

        </div>
      </div>
    </div>
</div>
</template>

<script>
import axios from 'axios';

export default {
  data () {
    return {
      fields: [
        { key: 'title', label: 'Disco' },
        { key: 'description', label: 'Artista' },
        { key: 'album', label: 'Código' },
         { key: 'action', label: 'Accion' }

      ],
      books:[]

     }
   },
   methods: {

        getBooks () {

          const path = 'http://localhost:8000/api/v1.0/books/'
          axios.get(path).then((response) => {
            this.books = response.data
          })

          .catch((error) => {
            console.log(error)
          })

        }

      },

      created(){
        this.getBooks()
      }

}
</script>

<style lang="css" scoped>
</style>
