<template>
    <el-breadcrumb>
        <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>商品或sku定时上下架 </el-breadcrumb-item>
        <el-breadcrumb-item>新建任务</el-breadcrumb-item>
    </el-breadcrumb>
    <div style="margin: 20px 0;">
        <el-alert title="可对商品或sku执行定时上下架任务，如果选择了sku则执行sku的上下架，否则执行商品上下架" type="info" show-icon />
    </div>
    <el-form :model="form" label-width="auto" style="max-width:800px">
        <el-form-item label="任务名称">
            <el-input v-model="form.name" placeholder="方便自己后期管理和识别不同任务" />
        </el-form-item>
        <el-form-item label="商品及sku">
            <div style="margin-bottom:0px">
                <el-button type="primary" plain size="small" @click="addItems()">添加商品</el-button>
            </div>
            <el-table :data="tableData" row-key="id" default-expand-all>
                <el-table-column type="selection" width="55" />
                <el-table-column prop="img" label="主图" />
                <el-table-column prop="title" label="标题" />
                <el-table-column label="操作">
                    <template #default="scope">
                        <el-button size="small" type="danger" @click="handleDelete(scope.$index, scope.row)">
                            Delete
                        </el-button>
                    </template>
                </el-table-column>
            </el-table>
        </el-form-item>
        <el-form-item label="上架时间">
            <el-date-picker v-model="form.date1" type="datetime" placeholder="留空则不执行上架操作" style="width: 100%" />
        </el-form-item>
        <el-form-item label="下架时间">
            <el-date-picker v-model="form.date2" type="datetime" placeholder="留空则不执行下架操作" style="width: 100%" />
        </el-form-item>
        <el-form-item label="重复周期">
            <el-radio-group v-model="form.repeat">
                <el-radio :value="0">不重复，只执行一次</el-radio>
                <el-radio :value="1">每天</el-radio>
                <el-radio :value="2">每周</el-radio>
                <el-radio :value="3">每月</el-radio>
            </el-radio-group>
        </el-form-item>
        <el-form-item label="备注">
            <el-input v-model="form.desc" type="textarea" />
        </el-form-item>
        <el-form-item>
            <el-button type="primary" @click="onSubmit">创建</el-button>
            <el-button>取消</el-button>
        </el-form-item>
    </el-form>

</template>
<script lang="ts" setup>
import { reactive } from 'vue'

// do not use same name with ref
const form = reactive({
    name: '',
    region: '',
    date1: '',
    date2: '',
    delivery: false,
    type: [],
    repeat: 0,
    desc: '',
})

const onSubmit = () => {
    console.log('submit!')
}

interface User {
    id: number
    img: string
    title: string
    hasChildren?: boolean
    children?: User[]
}
const tableData: User[] = [
    {
        id: 1,
        img: '2016-05-02',
        title: 'wangxiaohu',
    },
    {
        id: 2,
        img: '2016-05-04',
        title: 'wangxiaohu',
    },
    {
        id: 3,
        img: '2016-05-01',
        title: 'wangxiaohu',
        children: [
            {
                id: 31,
                img: '2016-05-01',
                title: 'wangxiaohu',
            },
            {
                id: 32,
                img: '2016-05-01',
                title: 'wangxiaohu',
            },
        ],
    },
    {
        id: 4,
        img: '2016-05-03',
        title: 'wangxiaohu',
    },
]
const addItems = () => {

}

const handleDelete = (index: number, row: User) => {
    console.log(index, row)
}
</script>
<style scoped>
/* .el-form {
    margin-top: 40px
} */
</style>