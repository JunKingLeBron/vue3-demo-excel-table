<template>
    <div>
        <el-table :data="dataList" style="width: 100%">
            <el-table-column  :label="item ? item.name : ''" width="180" v-for="(item, index) in title" :key="index">
                <template  #header>
                    <span>{{item ? item.name : ''}}</span>
                </template>
                <template #default="scope">
                    <span>{{scope.row[index]}}</span>
                </template>
            </el-table-column>
        </el-table>
    </div>
</template>

<script>
    import { reactive, toRefs } from 'vue';
    import { data } from '../util/data'
    const tableData = [
        {
            date: '2016-05-03',
            name: 'Tom',
            address: 'No. 189, Grove St, Los Angeles',
        },
        {
            date: '2016-05-02',
            name: 'Tom',
            address: 'No. 189, Grove St, Los Angeles',
        },
        {
            date: '2016-05-04',
            name: 'Tom',
            address: 'No. 189, Grove St, Los Angeles',
        },
        {
            date: '2016-05-01',
            name: 'Tom',
            address: 'No. 189, Grove St, Los Angeles',
        },
    ]

    const useGenerListEffect = () => {
         const data1 = reactive(data)
         let obj = {}
         let newData = []
         let title = ['']
         let obj2 = {}
         for( let key in data1) {
            obj2 = {}
            obj2.name = key
            obj2.lang = []
            for (let key2 in data1[key]) {
                obj2.lang.push({
                    name: key2,
                    value: data1[key][key2]
                })
            }
            newData.push(obj2)
         }
         newData.forEach(item => {
            title.push({name: item.name})
            item.lang.forEach(l => {
                let value = l.value
                if (obj[l.name]) {
                    obj[l.name] = [...obj[l.name], value]
                } else {
                    obj[l.name] = [value]
                }
            })
         })
         let dataList = []
         for(let key in obj) {
            dataList.push([key, ...obj[key]])
         }
         return { newData, title, dataList }
    }

    export default {
        name: 'TableShow',
        setup() {
            const { newData, title, dataList } = useGenerListEffect()
            console.log('title', title)
            console.log('dataList', dataList)
            return {
                tableData,
                title,
                dataList,
                newData
            }
        }
    }
</script>

<style scoped>


</style>