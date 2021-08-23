<template>
<div>
    <h1>TV</h1>
    <form v-on:submit.prevent = "createUser">
        <p>หมายเลขรุ่น: <input type="text" v-model="user.name"></p>
        <p>ยี่ห้อ โทรทัศน์: <input type="text" v-model="user.lastname"></p>
        <p>ขนาดหน้าจอโทรทัศน์: <input type="text" v-model="user.email"></p>
        <p>ความละเอียดของจอภาพ: <input type="text" v-model="user.password"></p>
        <p><button type="submit">บันทึกข้อมูลโทรทัศน์</button></p>
    </form>
    <hr>
    <div>
        <p>หมายเลขรุ่น: {{user.name}}</p>
        <p>ยี่ห้อ โทรทัศน์: {{user.lastname}}</p>
        <p>ขนาดหน้าจอโทรทัศน์: {{user.email}}</p>
        <p>ความละเอียดของจอภาพ: {{user.password}}</p>
    </div>
</div>
</template>
<script>
import UsersService from '@/services/UsersService'

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
        async createUser(){
            try{
                await UsersService.post(this.user)
                this.$router.push({
                    name: 'users'
                })
            }catch(error){
                console.log(error)
            }
        }
    }    
}
</script>
<style scoped>


</style>