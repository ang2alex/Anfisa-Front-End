<template>
    <div class="custom-table">
        <div
          v-b-toggle="'table_'+id"
          :class="['custom-table_header', 'js-table_header',
            secondary ? 'custom-table_header-secondary' : '']"
        >
            {{title.toUpperCase()}}
            <div class="custom-table_header_icon" />
        </div>
        <b-collapse :id="'table_'+id" class="custom-table_collapse">
            <div class="custom-table_table-wrapper">
                <CustomHScroll :id="id">
                    <div v-if="content" v-html="content" class="custom-table_html"/>
                    <table class="custom-table_table">
                        <tr v-for="(row, index) in data" v-bind:key="index">
                            <td v-for="(cell, index) in row" v-html="cell" v-bind:key="index"/>
                        </tr>
                    </table>
                </CustomHScroll>
            </div>
        </b-collapse>
    </div>
</template>

<script>
import CustomHScroll from './CustomHScroll.vue';

export default {
    props: {
        title: String,
        id: String,
        data: Array,
        secondary: Boolean,
        content: String,
    },
    components: {
        CustomHScroll,
    },
};
</script>

<style lang="scss" scoped>
    .custom-table {
            border-radius: 5px;
            box-shadow: 0px 12px 24px rgba(24,64,104,0.09);
            background-color: #ffffff;
            margin: 0 10px 20px 10px;

        &_header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            overflow: hidden;
            border-radius: 5px 5px 0 0;
            font-size: 16px;
            letter-spacing: 0px;
            color: #2bb3ed;
            font-weight: 800;
            line-height: 47px;
            box-shadow: 0px 2px 24px rgba(24,64,104,0.06);
            background-color: #ffffff;
            padding: 0 20px;
            &:hover {
                cursor: pointer;
                background-color: #12aaeb;
                box-shadow: 0px 12px 24px rgba(24,64,104,0.09);
                color: #fff;
                .custom-table_header_icon {
                    border-bottom-color: #fff;
                }
            }
            &-secondary:hover {
                background-color: #52002957;
                &[aria-expanded=false] {
                    &:hover {
                        background-color: #52002957;
                    }
                }
            }
            &_icon {
                width: 0;
                height: 0;
                border-top: 0;
                border-right: 5px solid transparent;
                border-bottom: 7px solid #b8cedd;
                border-left: 5px solid transparent;
            }
            &[aria-expanded=false] {
                background-color: #a4b6c5;
                color: #ffffff;
                border-bottom: 0;
                .custom-table_header_icon {
                    border-top: 7px solid #ffffff;
                    border-bottom: 0;
                }
                .custom-table_header_title {
                    border-bottom: none;
                    color: #ffffff;
                }
                &:hover {
                    cursor: pointer;
                    background-color: #12aaeb;
                    box-shadow: 0px 12px 24px rgba(24,64,104,0.09);
                    color: #fff;
                    .custom-table_header_icon {
                        border-bottom-color: #fff;
                    }
                }
            }
        }
        &_html {
            white-space: pre-line;
        }
        &_table {
            width: 100%;
            tr {
                height: 30px;
                border-bottom: 1px solid #e8edf1;
                &:last-child {
                    border-bottom: none;
                }
            }
            td {
                font-size: 14px;
                letter-spacing: 0px;
                color: #586978;
                padding: 0 10px;
                &:nth-child(1) {
                    color: #1a3e6c;
                    font-weight: bold;
                }
            }
            &-wrapper {
                width: 100%;
                position: relative;
            }
        }
    }

</style>
