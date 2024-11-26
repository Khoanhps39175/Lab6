<template>
    <div class="container mt-5">
        <h1 class="text-center mb-4">Kiến thức sức khỏe cộng đồng</h1>
        <div class="row g-4">
            <div class="col-sm-4 d-flex" v-for="(item, index) in items" :key="index">
                <div class="card border-secondary shadow-sm flex-grow-1">
                    <img :src="item.image" class="card-img-top img-fluid" alt="Hình ảnh" />
                    <div class="card-body d-flex flex-column">
                        <h5 class="card-title">{{ item.title }}</h5>
                        <p class="card-text flex-grow-1">{{ item.content }}</p>
                        <button class="btn btn-info btn-bottom">Xem chi tiết</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

import img1 from '../assets/image/img1.jpg';
import img2 from '../assets/image/img2.jpg';
import img3 from '../assets/image/img3.jpg';
import { ref } from 'vue';

const items = ref([
    {
        id: 1,
        title: '8 loại rau củ quả giàu canxi',
        content: 'Canxi là...',
        image: img1
    },
    {
        id: 2,
        title: 'Các loại gia vị tốt cho sức khỏe',
        content: 'Một số loại...',
        image: img2
    },
    {
        id: 3,
        title: '9 loại đậu bổ dưỡng nên dùng nhiều',
        content: 'Đậu lăng...',
        image: img3
    },
]);
</script>
