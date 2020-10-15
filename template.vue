<template>
    <div class="row">
    <table class="form-group table table-hover w-100">
        <transition-group name="item" tag="tbody">
            <item
                    v-for="template in templates"
                    v-bind:key="template.id"
                    v-bind:id="template.id"
                    v-bind:name-col="template.nameCol"
                    v-bind:value-col="template.valueCol"
                    v-bind:name-comment-col="template.nameCommentCol"
                    v-bind:value-comment-col="template.valueCommentCol">
            </item>
        </transition-group>
    </table>
    <p>Добавить новый пункт...</p>
    <div class="input-group">
        <input v-model="colName" type="text" class="form-control" placeholder="Заголовок">
        <input v-model="colMemo" type="text" class="form-control" placeholder="Комментарий" >
        <div class="input-group-append">
            <button v-on:click="addItem" class="btn btn-success" type="button">+</button>
        </div>
    </div>
    </div>
</template>

<script>
    let $ = require('jquery');
    import {URL} from '../contants.js';
    import item from './template/item.vue';

    export default {
        components: {
            item
        },
        data () {
            return {
                idItem: Number,
                colName: '',
                colMemo: '',
                templates: []
                //templates:  [{id: 1, nameCol:'1', valueCol: 'sdsdsdf', nameCommentCol: 'sdfdf', valueCommentCol: 'sdfsdf'}]
            }
        },
        mounted(){
            this.getItems();
        },
        methods: {
            addItem() {
                if (this.colName.length > 0) {
                    this.idItem = this.templates.length+1;
                    this.templates.push(
                        {
                            id: this.idItem,
                            nameCol:'col-'+this.idItem,
                            valueCol: this.colName,
                            nameCommentCol: 'com-'+this.idItem,
                            valueCommentCol: this.colMemo
                        }
                    );
                    this.colName = '';
                    this.colMemo = '';
                }

            },
            getItems(){
                let template_id = document.getElementById('template-id').value;
                if (template_id == null) return null;
                let items = this.templates;
                $.ajax({
                    url: URL + 'templates/getcols?template_id=' + template_id,
                    success: function (data) {
                        data.forEach(function(item){
                            items.push({
                                id: item.id,
                                nameCol:'col-'+item.id,
                                valueCol: item.name,
                                nameCommentCol: 'com-'+item.id,
                                valueCommentCol: item.memo
                            })
                        });
                    }
                });
            }
        }
    }
</script>

<style>

    .item-enter-active {
        transition: all .5s ease;
    }
    .item-leave-active {
        transition: all .5s cubic-bezier(1.0, 0.5, 0.8, 1.0);
    }
    .item-enter, .slide-fade-leave-to
        /* .slide-fade-leave-active до версии 2.1.8 */ {
        transform: translateY(20px);
        opacity: 0;
    }
</style>