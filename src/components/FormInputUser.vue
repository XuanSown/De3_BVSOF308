<template>
    <div class="card p-4 mb-5 bg-light">
        <h3 class="mb-3">Thêm nhân viên</h3>
        <form>
            <div class="mb-3">
                <label class="form-label">Họ và tên</label>
                <input type="text" class="form-control" v-model="formUser.name" required
                    placeholder="Nhập tên vào đây!">
            </div>
            <div class="mb-3">
                <label class="form-label">Email</label>
                <input type="email" class="form-control" v-model="formUser.email" required
                    placeholder="Nhập email vào đây!">
            </div>
            <div class="mb-3">
                <label class="form-label">Mật khẩu</label>
                <input type="password" class="form-control" v-model="formUser.password" required
                    placeholder="Nhập mật khẩu vào đây!">
            </div>
            <div class="mb-3">
                <label class="form-label">Địa chỉ</label>
                <input type="text" class="form-control" v-model="formUser.address" required
                    placeholder="Nhập địa chỉ vào đây!">
            </div>
            <div class="mb-3">
                <label class="form-label">Giới tính</label>
                <select class="form-select" v-model="formUser.gender" required>
                    <option selected value="0">Nam</option>
                    <option value="1">Nữ</option>
                </select>
            </div>
            <button type="button" class="btn btn-success" @click="saveUser">Lưu</button>
            <button type="button" class="btn btn-warning" @click="removeUser">Xóa</button>
        </form>
    </div>
</template>

<script setup>
import { reactive, watch } from 'vue';
const props = defineProps({
    userSelected: {
        type: Object,
        default: null
    }
});

const formUser = reactive({
    id: null,
    name: '',
    email: '',
    password: '',
    address: '',
    gender: '0'
});

// Hàm reset form về rỗng
const resetForm = () => {
    formUser.id = null;
    formUser.username = '';
    formUser.email = '';
    formUser.password = '';
    formUser.address = '';
    formUser.gender = 1;
};

watch(() => props.userSelected, (newUser) => {
    if (newUser) {
        Object.assign(formUser, newUser)
    } else {
        resetForm();
    }
})

const emit = defineEmits(['save-user', 'remove-user']);
const saveUser = () => {
    if (formUser.name ||
        formUser.email ||
        formUser.password ||
        formUser.address
    ) {
        alert("Vui lòng nhập đầy đủ thông tin !");
        return;
    }
    emit('save-user', { ...formUser });
    //reset
    formUser.id = -1;
    formUser.name = '';
    formUser.email = '';
    formUser.password = '';
    formUser.address = '';
    formUser.gender = '0';
};
const removeUser = () => {
    if (confirm('Bạn chắc chắn muốn xóa')) {
        emit('remove-user', formUser.id);
    }
};
</script>