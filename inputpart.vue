<template>
    <!-- 定义好的搜索条件组件1 -->
    <!-- 查询条件 -->
    <div
        class="query"
        style="
            margin-top: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
        "
    >
        <!-- 搜索条件 -->
        <div class="query_1">
            <div class="query_1_1" style="width: 400px; margin-right: 50px">
                <!-- 机构代码: -->
                <a-input
                    size="large"
                    :addon-before="string_a"
                    placeholder="请输入数字"
                    v-model="search_a"
                    >{{ search_a }}</a-input
                >
            </div>
            <div class="query_1_2" style="width: 400px; margin-right: 50px">
                <!-- 机构名称: -->
                <a-input
                    size="large"
                    :addon-before="string_b"
                    placeholder="请输入名称"
                    v-model="search_b"
                    >{{ search_b }}</a-input
                >
            </div>
        </div>

        <a-button
            icon="search"
            ghost
            type="primary"
            style="margin-right: 50px"
            @click="searchForm()"
            >搜索</a-button
        >

        <!-- 选择器1(不包含 全部) -->
        <div v-show="visible">
        <!-- <div> -->
            <span style="margin-right: 15px">业务类</span>
            <a-select
                default-value="1"
                size="large"
                style="width: 120px"
                @change="handleChange"
            >
                <a-select-option value="1"> 人民币 </a-select-option>
                <a-select-option value="2"> 外币 </a-select-option>
                <a-select-option value="3"> 本外币 </a-select-option>
                <a-select-option value="4"> 其他 </a-select-option>
            </a-select>
        </div>

        <!-- 选择器2(包含 全部) -->
        <div v-show="visibleTwo">
        <!-- <div> -->
            <span style="margin-right: 15px">业务类</span>
            <a-select
                default-value="0"
                size="large"
                style="width: 120px"
                @change="handleChange"
            >
                <a-select-option value="0"> 全部 </a-select-option>
                <a-select-option value="1"> 人民币 </a-select-option>
                <a-select-option value="2"> 外币 </a-select-option>
                <a-select-option value="3"> 本外币 </a-select-option>
                <a-select-option value="4"> 其他 </a-select-option>
            </a-select>
        </div>

        <!-- 导出excel功能 -->
        <div  style="margin-left: 30px">
            <download-excel
                class="export-btn"
                :data="tableData"
                :fields="jsonFields"
                type="xls"
                :header="headerTitle"
                :name="`${headerTitle}.xls`"
            >
                <a-tooltip placement="bottomLeft">
                    <template slot="title">
                        <span>导出excel</span>
                    </template>
                    <a-button icon="folder-open"> </a-button>
                </a-tooltip>
            </download-excel>
        </div>
        
    </div>
</template>

<script>
export default {
    // props: ["string_a", "string_b"],
    props: {
        // 搜索条件
        string_a:  String,   
        string_b:  String,

        // 下拉框显隐条件
        visible: {
            type: Boolean,
            default: false
        },
        visibleTwo: {
            type: Boolean,
            default: false
        },

        // 导出excel条件
        tableData: Array,
        jsonFields: Object,
        headerTitle: String,

    },
    data() {
        return {
            search_a: "",
            search_b: "",
        };
    },
    methods: {
        // 两个条件的搜索方法
        searchForm() {
            // 搜索条件信息
            console.log(this.search_a, this.search_b);
            this.$emit('searchForm', {
                sinstcode:   this.search_a,
                sinstname:   this.search_b
            })
        },
        // 选择器的选择值
        handleChange(value) {
            console.log(`selected ${value}`);
            this.$emit('handleChange', value);
        },
       
    },
};
</script>

<style lang="less" scoped>
.query_1 {
    display: flex;
    align-items: flex-end;
    .query_1_1 {
        display: flex;
        align-items: center;
    }
    .query_1_2 {
        display: flex;
        align-items: center;
    }
}

.query {
    display: flex;
    justify-content: space-between;
}
</style>
