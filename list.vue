<template>
    <h1>เเสดงข้อมูลนักศึกษา {{ username }}</h1>
</template>

<script>
export default {
    data:() => ({
        id: '',
        username: '',
        password: '',
        email: '',
        picture: '',
        status: ''

    }),
    async created() {
        const response = await fetch('http://localhost:7000/list')
        console.log(response);
        const data = await response.json()
        console.log('data => ',data)
        this.username = data.row[0].username
    }
}
</script>
