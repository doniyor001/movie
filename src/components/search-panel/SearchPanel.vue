<template>
    <Input
    class="search-input"
    placeholder="Kinolarni qidirish"
    v-model="term"
    @input="changeHandler"/>
</template>

<script>
import Input from "@/ui-components/Input.vue";

export default {
    components: {Input},
  props: {
    updateTernHandler: {
      type: Function,
      required: true,
    },
  },
  data() {
    return{
      term: '',
    }
  },
  methods: {
    changeHandler(e){
      this.term = e.target.value
      this.updateTernHandler(this.term)
    },
  },
}
</script>

<style scoped>
  .search-input{
    margin-bottom: 1rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
  }
</style>