<template>
    <!-- 对eltable设置一个名为draggable-table的class -->
    <el-table
        :data="tableData"
        border
        row-key="date"
        class="draggable-table"
        style="width: 100%"
    >
        <el-table-column prop="date" label="日期" width="180"> </el-table-column>
        <el-table-column prop="name" label="姓名" width="180"> </el-table-column>
        <el-table-column prop="address" label="地址"> </el-table-column>
    </el-table>
</template>

<script>
import Sortable from "sortablejs";

export default {
    data() {
        return {
            tableData: [
                // 略去数据，与前段代码一直
            ],
        };
    },
    mounted() {
        // 需要支持拖动效果的列表容器，在这里我们设置为el-table组件的tbody，
        // 注意：最前面的一段为前面el-table的class: draggable-table，主要为了防止如果页面有多个table，多个table同时实现拖拽效果
        // 当然，如果多个table都需要拖拽效果，选择器中最前面的.draggable-table可以去除。
        const tbody = document.querySelector(".draggable-table .el-table__body-wrapper tbody");
        new Sortable(tbody, {
            animation: 150,
            // 需要在odEnd方法中处理原始eltable数据，使原始数据与显示数据保持顺序一致
            onEnd: ({ newIndex, oldIndex }) => {
                const targetRow = this.tableData[oldIndex];
                this.tableData.splice(oldIndex, 1);
                this.tableData.splice(newIndex, 0, targetRow);
                console.table(this.tableData);
            },
        });
    },
};
</script>
<style scoped>
</style>
