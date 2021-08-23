<template>
<div>
    <h1>Edit User</h1>
    <form v-on:submit.prevent = "editUser">
        <p>id Printer: <input type="text" v-model="user.name"></p>
        <p>ชื่อรุ่น รหัสรุ่น: <input type="text" v-model="user.lastname"></p>
        <p>spec Printer: <input type="text" v-model="user.email"></p>
        <p>ราคา: <input type="text" v-model="user.password"></p>
        <p><button type="submit">edit user</button></p>
    </form>
    <hr>
    <div>
        <p>id Printer: {{user.name}}</p>
        <p>ชื่อรุ่น รหัสรุ่น: {{user.lastname}}</p>
        <p>spec Printer: {{user.email}}</p>
        <p>ราคา: {{user.password}}</p>
    </div>
</div>
</template>
<script>import UsersService from '@/services/UsersService'

export default {
    data(){
        return{
            user:{
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
    },
    methods:{
        async editUser(){
            try{
                await UsersService.put(this.user)
                this.$router.push({
                    name: 'users'
                })

            }catch(error){
                console.log(error)
            }
        }
    }, 
    async created(){
        try{
            let userId = this.$route.params.userId
            this.user = (await UsersService.show(userId)).data
        }catch(error){
            console.log(error)
        }
    }
}
</script>
<style scoped>


</style>