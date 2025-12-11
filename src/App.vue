<script setup>
import { reactive, ref } from 'vue';
import FormInputUser from './components/FormInputUser.vue';
import TableUser from './components/TableUser.vue';

const users = reactive([
  {
    id: 1,
    name: 'Sown',
    email: 'sown@gmail.com',
    password: '123',
    address: 'HCM',
    gender: 0,
  },
  {
    id: 2,
    name: 'Anh',
    email: 'anh@gmail.com',
    password: '111',
    address: 'Vinh Long',
    gender: 1,
  },
]);

const userSelected = ref([
  {
    id: null,
    name: '',
    email: '',
    password: '',
    address: '',
    gender: 0,
  },
]);

const handleSaveUser = (formData) => {
  if (formData.id) {
    //tìm và cập nhật
    const userIndex = users.findIndex(e => e.id === formData.id);
    if (userIndex != -1) {
      users[userIndex] = formData;
    }
  } else {
    //tạo mới
    formData.id = Math.floor(Math.random() * 100) + 1
    users.push(formData);
  }
  userSelected.value = null;
};

const handleRemoveUser = (userId) => {
  const userIndex = users.findIndex(e => e.id === userId)
  if (userIndex != -1) {
    users.splice(userIndex, 1);
  }
  userSelected.value = null;
};

//khi chọn dòng trên table
const handleSelectUser = (user) => {
  userSelected.value = { ...user };
};

</script>

<template>
  <div class="container">
    <h1 class="text-center mb-4">QUẢN LÍ NHÂN VIÊN</h1>
    <div class="col-md-8">
      <FormInputUser :user-selected="userSelected" @save-user="handleSaveUser" @remove-user="handleRemoveUser" />
    </div>
    <hr>
    <h3 class="mb-3">Danh sách:</h3>
    <TableUser :users="users" @select-user="handleSelectUser" />
    <div class="text-center text-muted" v-if="users.length == 0">
      Không có!
    </div>
  </div>
</template>

<style scoped></style>
