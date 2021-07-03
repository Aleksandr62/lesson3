<template>
    <div v-if="quantityItems > quantityOnPage" class="pagination">
        <button class="page"
        :disabled="pageNumber === 1"
        @click="prevPage"        
        >
        &lt;
        </button>
        <button class="page"
        :class="{ active_page : pageNumber === n  }"
        v-for="n in countPages" 
        :key="n" 
        @click="selectPage(n)"
        > 
        {{ n }} 
        </button>
        <button class="page"
        :disabled="pageNumber === countPages"
        @click="nextPage"
        >
        &gt;
        </button>        
    </div>
</template>

<script>
export default {
    name: 'Pagination',
    props: {
        quantityOnPage: {
            type: Number,
            default: 1
        },
        quantityItems: {
            type: Number,
            default: 1
        },
    },
    data() {
        return {
            pageNumber: 1,
        }
    },
    computed: {
        countPages() {
            return Math.ceil(this.quantityItems / this.quantityOnPage)
        },
        page() {
            return {
                start: this.pageNumber * this.quantityOnPage - this.quantityOnPage, 
                end: this.pageNumber * this.quantityOnPage
                }
        }
    },
    methods: {
        nextPage(){
            this.pageNumber += 1;
            this.$emit('select-page', this.page);
        },
        prevPage(){
            this.pageNumber -= 1;
            this.$emit('select-page', this.page);
        },
        selectPage(n){
            this.pageNumber = n;
            this.$emit('select-page', this.page);
        }        
    },
    created() {
        this.selectPage(1);
    }
}
</script>

<style scoped>
.pagination {
    margin-top: 12px;
    padding: 8px 20px;
    border: 1px solid #EBEBEB;
    color: #222222;
    display: flex;
    width: fit-content;
}
.page {
    margin-left: 5px;
    margin-right: 5px;
    cursor: pointer;
    border: none;
    background: transparent;
}
.active_page {
    color: red;
}
</style>