<template>
  <div>
    <h1> Show TV for client</h1>
    <div v-if="users.length">
      <h4>จำนวนผู้ใช้งาน {{ users.length }}</h4>
      <p>
        <button v-on:click="navigateTo('/user/create')">
            เพิ่มข้อมูลยี่ห้อโทรทัศน์
          </button>
      </p>
      <div v-for="user in users" v-bind:key="user.id">
        <p>หมายเลขรุ่น: {{ user.id }}</p>
        <p>ยี่ห้อ โทรทัศน์: {{ user.name }} - {{ user.lastname }}</p>
        <p>ขนาดหน้าจอโทรทัศน์ : {{ user.email }}</p>
        <p>ความละเอียดของจอภาพ: {{ user.password }}</p>
        <p>
          <button v-on:click="navigateTo('/user/' + user.id)">
            ดูข้อมูลของจอภาพ
          </button>
          <button v-on:click="navigateTo('/user/edit/' + user.id)">
            แก้ไขข้อมูลของจอภาพ
          </button>
          <button v-on:click="deleteUser(user)">
            ลบข้อมูล
          </button>
        </p>
        <hr />
      </div>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      users: [],
    };
  },
  async created() {
    try {
      this.users = (await UsersService.index()).data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteUser(user){
      let result = confirm("Want to delete")
      if(result){
        try{
          await UsersService.delete(user)
          this.refreshData()
        }catch(error){
          console.log(error)
        }
      }
    },
    async refreshData(){
      this.users = (await UsersService.index()).data
    }
  },
};
</script>
<style scoped>
</style>