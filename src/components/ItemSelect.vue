<template>
    <el-dialog v-model="dialogVisible" title="商品选择" width="800">
        <el-form :inline="true" :model="form" class="item-search-form">
            <el-form-item label="标题或id">
                <el-input v-model="form.title" autocomplete="off" />
            </el-form-item>
            <el-form-item label="上架状态">
                <el-select v-model="form.approveStatus" placeholder="" clearable>
                    <el-option label="出售中" value="shanghai" />
                    <el-option label="仓库中" value="beijing" />
                </el-select>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="onSubmit">查询</el-button>
            </el-form-item>
        </el-form>
        <el-table :data="gridData">
            <el-table-column property="date" label="Date" width="150" />
            <el-table-column property="name" label="Name" width="200" />
            <el-table-column property="address" label="Address" />
        </el-table>
        <template #footer>
            <div class="dialog-footer">
                <el-button @click="dialogVisible = false">Cancel</el-button>
                <el-button type="primary" @click="dialogVisible = false">
                    Confirm
                </el-button>
            </div>
        </template>
    </el-dialog>
</template>

<script lang="ts" setup>
import { reactive, ref } from 'vue'
import axios from 'axios';

const dialogVisible = ref(false)
defineExpose({
    dialogVisible
})
const formLabelWidth = '100px'

const form = reactive({
    title: '',
    approveStatus: '',
    date1: '',
    date2: '',
    delivery: false,
    type: [],
    resource: '',
    desc: '',
})

const onSubmit = () => {
    // axios.post('/item/getItems', {
    axios.post('/api/test/getItems', {
        title: form.title,
        approveStatus: form.approveStatus,
        with_sku: 1
    })
}

const gridData = [
    {
        date: '2016-05-02',
        name: 'John Smith',
        address: 'No.1518,  Jinshajiang Road, Putuo District',
    },
    {
        date: '2016-05-04',
        name: 'John Smith',
        address: 'No.1518,  Jinshajiang Road, Putuo District',
    },
    {
        date: '2016-05-01',
        name: 'John Smith',
        address: 'No.1518,  Jinshajiang Road, Putuo District',
    },
    {
        date: '2016-05-03',
        name: 'John Smith',
        address: 'No.1518,  Jinshajiang Road, Putuo District',
    },
]
</script>
<style scoped>
.item-search-form .el-select {
    --el-select-width: 100px;
}
</style>