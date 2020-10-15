<template>
    <tr>
        <td>
            <div class="form-group p-0">
                <div class="row">
                    <div class="col-5">
                        <input type="text" class="form-control border-0 shadow-none bg-transparent " v-bind:name="nameCol" v-bind:value="valueCol"/>
                    </div>
                    <div class="col-6">
                        <input type="text" class="form-control border-0 shadow-none bg-transparent text-muted " v-bind:name="nameCommentCol" v-bind:value="valueCommentCol"/>
                    </div>
                </div>
            </div>
        </td>
    </tr>
</template>

<script>
    export default {
        props: {
            nameCol: String,
            valueCol: String,
            nameCommentCol: String,
            valueCommentCol: String
        }
    }
</script>

<style>

</style>