<template>
      <label>
        <p v-if="type != 'submit'">{{ libelle }}</p>
        <input v-if="type === 'submit'" type="submit" v-bind:value="libelle">
        <textarea @input="handleInput" v-else-if="type === 'textarea'" :value="value"></textarea>
        <input @input="handleInput" v-else :value="value" :type="type" contenteditable="true">
      </label>
</template>

<script>
  export default {
    props: {
        libelle: String,
        type:{
            default: 'text',
            type: String
        },
        placeholder: String,
        name: String,
        value: String
    },
    data () {
        return {
        }
    },
    methods: {
        handleInput (e) {
            this.$emit('input', e.target.value)
        }
    }
  }
</script>