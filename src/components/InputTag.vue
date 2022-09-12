<script>
   export default {
      // props: ['onTagsChange'],
      emits: ['onTagsChange'],

      data() {
         return {
            currentValue: "",
            tags: [],
         };
      },

      methods: {
         handleSubmit(e) {
            if (this.currentValue !== '') {
               const exist = this.tags.some((item) => item === this.currentValue);
               if (!exist) {
                  this.tags.push(this.currentValue);
                  this.currentValue = '';
                  // this.onTagsChange(this.tags);
                  this.$emit('onTagsChange', this.tags);
               }
            }
         },

         handleKeyDown(e) {
            if (e.key === 'Backspace' && this.currentValue === '') {
               this.tags.pop();
               // this.onTagsChange(this.tags);
               this.$emit('onTagsChange', this.tags);
            }
         },

         deleteTag(tag) {
            this.tags = this.tags.filter((item) => item !== tag);
            // this.onTagsChange(this.tags);
            this.$emit('onTagsChange', this.tags);
         },
      },
   };
</script>

<template>
   <div class="inputTag">
      <div class="tags">
         <span class="tag" v-for="(tag, index) in tags" :key="index">
            {{ tag }}
            <button @click="deleteTag(tag)">X</button>
         </span>
      </div>
      <form @submit.prevent="handleSubmit">
         <input type="text" v-model="currentValue" @keydown="handleKeyDown" />
      </form>
   </div>
</template>

<style scoped></style>