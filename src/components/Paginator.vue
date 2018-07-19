<template>
    <div class="pagination-container">
        <nav aria-label="Paginator" v-if="this.lastPage > 1">
            <ul class="pagination"  :class="{'pagination-sm' : small || extraSmall}">
                <li class="page-item" :class="{'disabled' : isAtFirstPage }" :disabled="isAtFirstPage">
                        <a :disabled="isAtFirstPage" @click.prevent.stop="prevPage" class="page-link" href="#">
                            <span v-if="small || extraSmall"><i class="fa fa-arrow-left"></i></span> <span v-else>Previous</span>
                        </a>
                    </li>
                <li 
                    v-for="(pageNumber, index) in pages" 
                    class="page-item"
                    :class="{'active' : page == pageNumber}" :key="pageNumber+'-page-'+id+index"
                >
                    <a class="page-link" href="#" @click.prevent.stop="setPageNumber(pageNumber)" v-if=" ! pageNumber.isSpacer">
                        {{pageNumber}}
                    </a>
                    <span v-else>
                        <a @click.prevent.stop href="#" disabled class="page-link">...</a>
                    </span>
                </li>
                <li class="page-item" :class="{'disabled' : isAtLastPage}" :disabled="isAtLastPage">
                    <a :disabled="isAtLastPage" @click.prevent.stop="nextPage" class="page-link" href="#">
                        <span v-if="small || extraSmall"><i class="fa fa-arrow-right"></i></span> <span v-else>Next</span>
                    </a>
                </li>
            </ul>
        </nav>
    </div>
</template>

<script>

import uuid from 'uuid'
import Vue from 'vue'

export default {
    props : ['items', 'setPage', 'size', 'small', 'name', 'extraSmall', 'stayOnFirstPage'],
    data(){
        return {
            page : 1,
            pageSize : this.size ? this.size : 8,
            previousItems : []
        }
    },
    watch : {
        items(incoming, outgoing){
        
            let newestItems = (incoming.filter(i => outgoing.indexOf(i) == -1));
            if (newestItems.length){
                let itemIndex = incoming.indexOf(newestItems[0]) + 1
                let itemPage = Math.ceil(itemIndex / this.pageSize);
                this.setPageNumber(itemPage);
            }
            Vue.nextTick( () => {
                this.$emit('update', this.pagedItems);
            })

            if (this.pagedItems.length == 0 && this.page > 1){
                this.goToLastPage()
            }

            if (  this.stayOnFirstPage ) this.setPageNumber(1);
              
        },
    },
    computed : {
        isAtFirstPage(){
            return this.page == 1;
        },
        isAtLastPage(){
            return this.page == this.lastPage
        },
        id(){
            return uuid.v4()
        },
        lastPage(){
            return Math.ceil(this.items.length / this.pageSize);
        },
        pagedItems(){
            let page = this.page - 1;
            var items = [...this.items];
            
            return items.splice(page * this.pageSize, this.pageSize);
        },
        pages(){
            let pageArray = [...Array(this.lastPage).keys()].map(function($i){ return $i+1; });
            let maxLength = 3
            if (this.small){
                maxLength = 1
            }

            if (pageArray.length > maxLength){
                let rangeToKeep = [1];

                let lowEnd = this.page - 2;

                if (lowEnd > 2){
                    rangeToKeep.push({ isSpacer: true });
                }
                for(var i = 0; i < 5; i++){
                    var page = lowEnd + i;
                    if (page > 1 && page < this.lastPage){
                        rangeToKeep.push(page);
                    }
                }

                if (this.page < this.lastPage - 3){
                    rangeToKeep.push({ isSpacer: true });
                }

                rangeToKeep.push(this.lastPage);
                pageArray = rangeToKeep;
            }

            return pageArray
        }
    },
    mounted(){
        this.previousItems = this.items;
        this.$emit('update', this.pagedItems)

        if (this.name){
            window.Events.$on('PageWasUpdatedForPaginator', ({name, page}) => {
                if (name == this.name && this.page != page)
                this.setPageNumber(page)
            })
        }
    },
    methods : {
        prevPage(){
            if (this.page > 1){
                this.page -= 1;
            }
            this.update()
        },
        nextPage(){
            if (this.page < this.lastPage){
                this.page += 1;
            }
            this.update()
        },
        update(){
            this.$emit('update', this.pagedItems)
        },
        setPageNumber(page){
            this.page = page;
            this.$emit('update', this.pagedItems)
            if (this.name)
                window.Events.$emit('PageWasUpdatedForPaginator', ({name : this.name, page}));
        },
        goToLastPage() {
            this.page = this.lastPage
        }
    }
}
</script>

<style>
.pagination-container {
    max-width: 100%;
    overflow-x: auto;
}
</style>