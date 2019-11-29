<template>
    <div class="btn-group" :disabled="disabled">
        <button  v-if="enableFirstPage" type="button"
                 class="btn btn-default mb-2" @click="onClickFirstPage" :disabled="isInFirstPage">
            {{firstLabel}}
        </button>
        <button type="button" class="btn btn-default mb-2"
                @click="onClickPreviousPage" :disabled="isInFirstPage">
            {{previousLabel}}
        </button>

        <template v-if="enablePageListing" v-for="page in pages">
            <button class="btn btn-default mb-2" type="button"
                    :key="page.name" @click="onClickPage(page.name)"
                    :disabled="page.isDisabled" :class="{ active: isPageActive(page.name) }">
                {{ page.name }}
            </button>
        </template>

        <button  type="button" class="btn btn-default mb-2"
                @click="onClickNextPage" :disabled="isInLastPage">
            {{nextLabel}}
        </button>
        <button  v-if="enableLastPage"  type="button"  class="btn btn-default mb-2"
                 @click="onClickLastPage" :disabled="isInLastPage">
            {{lastLabel}}
        </button>
    </div>
</template>
<script>
    export default {

        name: 'VuePaginater',
        data: function () {
            return {
                currentPage:1,
                //offset:0
            }
        },
        props: {
            maxVisibleButtons: {
                type: Number,
                required: false,
                default: 3
            },

            max: {
                type: Number,
                required: false,
                default:0
            },
            total: {
                type: Number,
                required: true
            },

            enablePageListing:{
                type: Boolean,
                required:false,
                default:true
            },
            enableFirstPage:{
                type: Boolean,
                required:false,
                default:true
            },
            enableLastPage:{
                type: Boolean,
                required:false,
                default:true
            },
            firstLabel:{
                type:String,
                required:false,
                default:'First'
            },
            lastLabel:{
                type:String,
                required:false,
                default:'Last'
            },
            nextLabel:{
                type:String,
                required:false,
                default:'Next'
            },
            previousLabel:{
                type:String,
                required:false,
                default:'Previous'
            },
            disabled:{
                type:Boolean,
                required:false,
                default:false
            },

        },
        computed: {
            startPage() {
                if (this.currentPage == 1) {
                    return 1;
                }

                if (this.currentPage == this.totalPages) {
                    return this.amountOfPages - this.maxVisibleButtons;
                }

                return this.currentPage - 1;
            },
            amountOfPages() {
                return Math.round((this.total/this.max))
            },
            pages() {
                const range = [];
                for (let i = this.startPage;
                     i <= Math.min(this.startPage + this.maxVisibleButtons - 1, this.amountOfPages);
                     i+= 1 ) {
                    if (i>0) {
                        range.push({
                            name: i,
                            isDisabled: i == this.currentPage
                        });
                    }
                }
                return range;
            },
            isInFirstPage() {
                return this.currentPage == 1;
            },
            isInLastPage() {
                return this.currentPage == this.amountOfPages;
            },
        },
        methods: {
            pageChanged:function(page) {
                this.currentPage = page;
               // this.offset=(page*this.max)-this.max
                //this.$emit('offset',this.offset);
                this.$emit('offset',(page*this.max)-this.max);
            },
            onClickFirstPage() {
                this.$emit('pagechanged', 1);
                this.pageChanged(1)
            },
            onClickPreviousPage() {
                this.currentPage=this.currentPage - 1
                this.$emit('pagechanged', this.currentPage);
                this.pageChanged(this.currentPage)
            },
            onClickPage(page) {
                this.$emit('pagechanged', page);
                this.pageChanged( page)
            },
            onClickNextPage() {
                this.currentPage=this.currentPage + 1
                this.$emit('pagechanged', this.currentPage);
                this.pageChanged(this.currentPage)
            },
            onClickLastPage() {
                this.$emit('pagechanged', this.amountOfPages);
                this.pageChanged(this.amountOfPages)
            },
            isPageActive(page) {
                return this.currentPage == page;
            }
        }
    };
</script>
<style>
    .pagination {
        list-style-type: none;
    }

    .pagination-item {
        display: inline-block;
    }

    .active {
        background-color: #4AAE9B;
        color: #ffffff;
    }
</style>