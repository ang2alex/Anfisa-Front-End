<template>
    <div class="load-view">
        <div class="load-view_header">
            <div class="load-view_header_sort">
                Sort By:
                <div class="load-view_header_sort_btn">Data saved</div>
                <div class="load-view_header_sort_btn">A-Z</div>
            </div>
            <div class="load-view_header_cancel" @click="onCancel">
                CANCEL
            </div>
        </div>
        <div class="load-view_cards">
            <FilterCard
                v-for="(filterData, index) in filterDetails"
                v-bind:key="index + '-' + filterData.name"
                :name="filterData.name"
                :conditions="filterData.conditions"
                :date="filterData.date"
                :onLoad="() => onLoad(filterData.name, filterData.conditions)"
                :onRemove="() => onRemove(filterData.name)"
            />
        </div>
    </div>
</template>

<script>
import FilterCard from './FilterCard.vue';

export default {
    props: ['onCancel', 'onLoad', 'onRemove'],
    components: {
        FilterCard,
    },
    computed: {
        filterDetails() {
            return this.$store.state.filterDetails;
        },
    },
    mounted() {
        this.$store.dispatch('getFilterDetails');
    },
};
</script>

<style lang="scss" scoped>
    .load-view {
        &_header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
            border-bottom: 1px solid #dfe4ea;
            &_sort {
                display: flex;
                align-items: center;
                font-size: 12px;
                letter-spacing: 0px;
                color: #627490;
                &_btn {
                    margin-left: 10px;
                    padding: 0 6px;
                    width: fit-content;
                    height: 21px;
                    line-height: 21px;
                    border-radius: 2px;
                    background-color: #d6dade;
                    font-size: 11px;
                    letter-spacing: 0px;
                    color: #ffffff;
                    &:hover {
                        background-color: #a5b7c6;
                        cursor: pointer;
                    }
                }
            }
            &_cancel {
                display: flex;
                justify-content: center;
                align-items: center;
                font-size: 11px;
                letter-spacing: 0px;
                color: #0a1c34;
                font-weight: 800;
                text-align: center;
                width: 77px;
                height: 25px;
                border-radius: 13px;
                background-color: #e7e7e7;
                &:hover {
                    background-color: #ededed;
                    cursor: pointer;
                }
            }
        }
        &_cards {
            margin: 0 12px;
        }
    }
</style>

