<script setup>
import { reactive } from 'vue';
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
]);

const handleSaveUser = (user) => {
  newUser.id = Math.floor(Math.random() * 100) + 1
  users.push(newUser);
};

const handleRemoveUser = (user) => {
  users.splice(index, 1);
};

const handleSelectUser = (user) => {

};

</script>

<template>
  <div class="container">
    <h1 class="text-center mb-4">QUẢN LÍ NHÂN VIÊN</h1>
    <div class="col-md-8">
      <FormInputUser :user="currentUser" @save-user="handleSaveUser" @remove-user="handleRemoveUser" />
    </div>
    <hr>
    <div>
      <h3 class="mb-3">Danh sách:</h3>
      <TableUser :users="users" @select-user="handleSelectUser" />
      <div class="text-center text-muted" v-if="users.length == 0">
        Không có!
      </div>
    </div>
  </div>
</template>

<style scoped></style>
