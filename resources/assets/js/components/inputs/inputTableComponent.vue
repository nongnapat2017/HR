<template>
    <table class="table table-bordered table-hover" style="width:100%">
        <thead>
            <tr style="background: azure;">
                <th 
                    class="word-wrap"
                    v-for = "head in headRows"
                    :key = "head"
                    scope = "col"
                    v-text = "head"
                ></th>  
                <th class="word-wrap" v-if = "hasActions !== undefined">จัดการข้อมูล</th>
            </tr>
        </thead>
        <tbody>
            <tr class="word-wrap" 
                v-for = "(row,index) in rows"
                :key = "index"
                scope = "col">
                <td 
                    class="word-wrap"
                    v-for = "(field,fieldIndex) in row " 
                    :key = "fieldIndex"
                    v-if = "fieldIndex !== 'id'"
                    v-text = "field"
                ></td>   
                <td class="word-wrap" v-if = "hasActions !== undefined">
                    <button
                        style="margin-left:5px;"
                        v-for ="action in hasActions"
                        :key = "action"
                        :class = "actions[action].class"
                        v-html= "actions[action].icon"
                        :name = "actions[action].name"
                        :value="row.id"
                        @click="ClickButton"
                    ></button>
                </td>
            </tr>
        </tbody>
    </table>
</template>
<style>
    .word-wrap{
        text-align: center;
        max-width: 15px;
        word-wrap:break-word;
    }
    button {
        box-shadow:0 0 5px #D2D0D0;
    }
</style>

<script>
export default {
    props : {
        name  : { required : true },
        headRows : 
            {
                required : true,
                type : Array
            },
        rows : 
            { 
                required : true,
                type : Array
            },
        hasActions : 
            {
                required: false
            }
    },
    data() {
        return {
            actions : {
                edit : {
                    name : 'edit',
                    class : 'btn btn-sm btn-info',
                    icon : '<i class = "fa fa-pencil"></i>'
                },
                delete : {
                    name : 'delete',
                    class : 'btn btn-sm btn-danger',
                    icon : '<i class = "fa fa-trash"></i>'
                }
            }
        }
    },
    methods:{
        ClickButton: function (event) {
            console.log ( 'table name : ' + this.name + ' id : ' + event.target.value + ' type : ' + event.target.name)
        }
    }
}
</script>

