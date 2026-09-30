<template>
  <div v-if="Array.isArray(model)">
    <table>
      <tr v-for="(o, i) in model">
        <td class="btn">
          <button @click="$emit('save',i)">💾</button>
          <button @click="$emit('del',i);model.splice(i, 1)">-</button>
          <button @click="model.push(o)">+</button>
        </td>
        <td>
          <Trees v-model="model[i]" />
        </td>
      </tr>
    </table>
    <button @click="model.push({})">+</button>
  </div>
  <div v-else-if="(model instanceof Object)">
    <div v-for="(o, i) in model">
      <table>
        <tbody>
          <tr>
            <td>
              <button @click="delete model[i]">-</button>
              <button @click="model[prompt()]={...o}">+</button>
              {{ i }}
            </td>
            <td>
              <Trees v-model="model[i]" />
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <button @click="model[prompt()] = null">+</button>
  </div>
  <div v-else-if="model == null">
    <button @click="model = {}">{</button>
    <button @click="model = [{}]">[</button>
    <button @click="model = ''">t</button>
  </div>
  <input v-else v-model="model" />
</template>

<script setup>
const model = defineModel()
</script>
<script>
export default {
  methods: {
    prompt() {
      return prompt()
    },
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
.btn button {
  display: block;
}

table {
  text-align: center;
  vertical-align: middle;
}

input {
  text-align: center;
  vertical-align: middle;
}
</style>
