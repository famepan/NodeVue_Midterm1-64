<template>
  <div>
    <h1>Show TV for client</h1>
    <p>หมายเลขรุ่น: {{ userId }}</p>
    <p>ยี่ห้อ โทรทัศน์: {{ user.name }} - {{ user.lastname }}</p>
    <p>ขนาดหน้าจอโทรทัศน์: {{ user.email }}</p>
    <p>ความละเอียดของจอภาพ: {{ user.password }}</p>
  </div>
</template>
<script>
import UserService from "@/services/UsersService";
export default {
  data() {
    return {
      user: null,
    };
  },
  async created() {
    try {
      let userId = this.$route.params.userId;
      this.user = (await UserService.show(userId)).data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
<style scoped>
</style>