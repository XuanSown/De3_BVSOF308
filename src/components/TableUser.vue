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
                <tr v-for="user in users" :key="user.id" @click="selectUser(userRow)" style="cursor: pointer;">
                    <td>{{ user.id }}</td>
                    <td>{{ user.name }}</td>
                    <td>{{ user.email }}</td>
                    <td>{{ user.password }}</td>
                    <td>{{ user.address }}</td>
                    <td>{{ user.gender == 1 ? 'Nam' : 'Nữ'}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup>
import { defineEmits, defineProps } from 'vue';
const props = defineProps({
    users: {
        type: Array,
        required: true,
        default: () =>[]
    },
});
const emit = defineEmits(['select-user']);
const selectUser = (userId) => {
    let userRow = props.users.find(e => e.id === userId);
    emit('select-user', {...userRow});
};
</script>