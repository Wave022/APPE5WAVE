<template>
    <div>
      <h1>Hello {{ name }}</h1>
      <input type="text" v-model="name">
      <input type="text" v-bind="age">
    </div>
</template>

<script>
export default {
    data() {
        return {
            name:"Earth",
            age: 20,
        }
    }
}
</script>