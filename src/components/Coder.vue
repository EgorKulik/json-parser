<template>
    <div>
        <div class="text-danger" ></div>
        <div class="text-success" >Valid JSON</div>
        <div class="edit_window">
            <textarea class="editor form-control" type="text" 
                placeholder="скопируйте или начните вводить ваш JSON код...">
            </textarea>
        </div>
    </div>
</template>

<script>
export default {

}
</script>

<style>
    .edit_window{
        display: flex;
        padding: 5px;
    }
    .editor{
        width: 100%;
        height: 300px;
        resize: none;
    }
</style>