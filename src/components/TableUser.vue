<template>
    <div class="container">
        <table class="table table-striped table-hover">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Họ và tên</th>
                    <th>Email</th>
                    <th>Mật khẩu</th>
                    <th>Địa chỉ</th>
                    <th>Giới tính</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="user in listUser" :key="user.id" @click="selectUser(user)">
                    <td>{{ info.id }}</td>
                    <td>{{ info.name }}</td>
                    <td>{{ info.email }}</td>
                    <td>{{ info.password }}</td>
                    <td>{{ info.address }}</td>
                    <td>{{ info.gender }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup>
import { defineEmits, defineProps } from 'vue';
const props = defineProps({
    listUser: {
        type: Array,
        required: true
    },
});
const emit = defineEmits(['select-user']);
const selectUser = (user) => {
    emit('select-user', {...user});
};
</script>