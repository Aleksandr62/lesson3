<template>
    <div v-if="countPages > 1" class="pagination">
        <button class="page"
        :disabled="page === 1"
        @click="page -= 1"        
        >
        &lt;
        </button>
        <button class="page"
        :class="{ active_page : page === n  }"
        v-for="n in countPages" 
        :key="n" 
        @click="page = n"
        > 
        {{ n }} 
        </button>
        <button class="page"
        :disabled="page === countPages"
        @click="page += 1"
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
        countPages: {
            type: Number,
            default: 1, 
        }           
    },
    data() {
        return {
            page: 1,
        }
    },
    watch: {
        page: function(page) {
            this.$emit('select-page', page - 1)
        } 
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