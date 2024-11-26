<template>
    <div class="container mt-4">
        <div class="row">
            <!-- Form thêm hoặc sửa học sinh -->
            <div class="col-md-4">
                <form @submit.prevent="submitForm">
                    <h3 class="mb-4">{{ isEditing ? 'Cập nhật học sinh' : 'Thêm học sinh' }}</h3>
                    <div class="mb-3">
                        <label for="name" class="form-label">Họ tên:</label>
                        <input type="text" class="form-control" v-model="student.name" id="name" required />
                    </div>
                    <div class="mb-3">
                        <label for="score" class="form-label">Điểm:</label>
                        <input type="number" max="10" min="0" class="form-control" v-model="student.score" id="score" required />
                    </div>
                    <div class="mb-3">
                        <label for="dob" class="form-label">Ngày sinh:</label>
                        <input type="date" class="form-control" v-model="student.dob" id="dob" required />
                    </div>
                    <button type="submit" class="btn btn-success w-100">
                        {{ isEditing ? 'Cập nhật' : 'Thêm' }}
                    </button>
                </form>
            </div>

            <!-- Danh sách học sinh -->
            <div class="col-md-8">
                <h3 class="mb-4">Danh sách học sinh</h3>
                <table class="table table-hover">
                    <thead>
                        <tr>
                            <th>Họ và tên</th>
                            <th>Điểm</th>
                            <th>Ngày sinh</th>
                            <th></th>
                            <th></th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(stu, index) in students" :key="index">
                            <td>{{ stu.name }}</td>
                            <td>{{ stu.score }}</td>
                            <td>{{ stu.dob }}</td>
                            <td>
                                <button class="btn btn-warning" @click="editStudent(index)">Sửa</button>
                            </td>
                            <td>
                                <button class="btn btn-danger" @click="deleteStudent(index)">Xóa</button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script setup>
    import { ref } from 'vue';

    // Mảng lưu danh sách học sinh
    const students = ref([
        { name: 'Nguyễn Hữu Khoa', score: 9, dob: '2005-11-05' },
        { name: 'Phạm Thị Lan', score: 8, dob: '2006-05-15' }
    ]);

    // Đối tượng lưu dữ liệu học sinh nhập vào form
    const student = ref({
        name: '',
        score: null,
        dob: ''
    });

    // Trạng thái chỉnh sửa
    let isEditing = ref(false);
    let editingIndex = ref(null);

    // Hàm xử lý form
    function submitForm() {
        if (isEditing.value) {
            // Cập nhật học sinh
            students.value[editingIndex.value] = { ...student.value };
            isEditing.value = false;
            editingIndex.value = null;
        } else {
            // Thêm mới học sinh
            students.value.push({ ...student.value });
        }
        resetForm();
    }

    // Hàm chỉnh sửa học sinh
    function editStudent(index) {
        student.value = { ...students.value[index] };
        isEditing.value = true;
        editingIndex.value = index;
    }

    // Hàm xóa học sinh
    function deleteStudent(index) {
        students.value.splice(index, 1);
    }

    // Hàm reset form
    function resetForm() {
        student.value = {
            name: '',
            score: null,
            dob: ''
        };
    }
</script>
