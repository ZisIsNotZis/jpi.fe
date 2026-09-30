<template>
  <table>
    <thead>
      <th v-for="(_, i) in Array.isArray(model) ? model[0] : model">
        {{ i }}
        <button @click="delcol(i)">&lt;</button>
      </th>
      <th>
        <button @click="col()">&gt;</button>
      </th>
    </thead>
    <tbody>
      <tr v-for="(o, i) in Array.isArray(model) ? model : [model]">
        <td v-for="(_, j) in Array.isArray(model) ? model[0] : model">
          <Tables v-model="o[j]" v-if="o[j] instanceof Object"/>
          <input v-model="o[j]" v-else />
        </td>
        <td v-if="Array.isArray(model)">
          <button @click="save(i)">💾</button>
          <button @click="delrow(i)">^</button>
        </td>
      </tr>
      <tr v-if="Array.isArray(model)">
        <td>
          <button @click="row()">V</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
const model = defineModel()
</script>
<script>
export default {
  methods: {
    row() {
      this.modelValue.push({})
    },
    col() {
      let name = prompt();
      (Array.isArray(this.modelValue) ? this.modelValue : [this.modelValue]).forEach(o => o[name] = '')
      console.log(this.modelValue)
    },
    delrow(i) {
      this.$emit("del", i)
      this.modelValue.splice(i, 1)
    },
    delcol(i) {
      (Array.isArray(this.modelValue) ? this.modelValue : [this.modelValue]).forEach(o => delete o[i])
    },
    save(i) {
      this.$emit("save", i)
    }
  }
};
</script>

<style scoped>
table {
  /* width: 100%; */
  text-align: center;
}

input {
  /* width: 100%; */
  text-align: center;
}
</style>
