<template>
   <div>
      <h1>Edit word</h1>
      <form action="" @submit.prevent="onSubmit">
         <div class="ui labeled input fluid">
            <div class="ui label"><i class="united kingdom flag"></i>English</div>
            <input type="text" required v-model="word.english"/>
         </div>
         <br />
         <div class="ui labeled input fluid">
            <div class="ui label"><i class="germany flag"></i>German</div>
            <input type="text" required v-model="word.german"/>
         </div>
         <br />
         <button class="ui primary button">Submit</button>
      </form>
   </div>
</template>

<script>
import { ViewVocabById, UpdateVocab } from '../helpers/api';
export default {
   name: "Edit",
   data() {
      return {
         word: {}
      }
   },
   async mounted() {
      this.word = await ViewVocabById(this.$route.params.id);
   },
   methods: {
      onSubmit: async function () {
         //update database
         await UpdateVocab(this.$route.params.id, this.word)
         //display message
         this.flash("Edit word succeed !")
         //redirect page
         this.$router.push(`/words`)
      }
   }
}
</script>