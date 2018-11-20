<template>
  
</template>

<script>

import axios from 'axios'

export default {
  name: 'EditBook',
  data () {
    return {
      book: {}
    }
  },
  created () {
    axios.get(`http://localhost:3000/book/` + this.$route.params.id)
    .then(response => {
      this.book = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  },
  methods: {
    onSubmit (evt) {
      evt.preventDefault()
      axios.put(`http://localhost:3000/book/` + this.$route.params.id, this.book)
      .then(response => {
        this.$router.push({
          name: 'ShowBook',
          params: { id: this.$route.params.id }
        })
      })
      .catch(e => {
        this.errors.push(e)
      })
    }
  }
}
</script>