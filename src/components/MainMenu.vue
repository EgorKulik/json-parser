<template>
    <div class="menu">
        <div class="checkbox_item item">
            <input type="checkbox" class="checkbox" @change="buttons.autoformation = !buttons.autoformation">
            <label class="text item">автоматическое форматирование кода</label> 
        </div>
        <a type="submit" class="button item">Шаг назад</a>
        <a type="submit" class="button item">Шаг вперед</a>
        <a type="submit" class="button item">Сохранить</a>
    </div>
</template>

<script>
export default {
    props: ['buttons']
}
</script>

<style>
    .item{
        margin: auto;
        margin: 5px auto 5px auto;
    }
    .button{
        padding: 10px;
        border: 3px;
        border-color: gray;
        border-radius: 5px;
        background-color: #2c3e50;
        color: white;
        cursor: pointer;
    }
    .button:hover{
        background-color: #586c81;
    }
    .menu{
        display: flex;
        flex-wrap: wrap;
        padding: 5px 20px;
        align-content: space-between;
    }
    .checkbox_item{
        display: flex;
        align-items: center;
    }
    .checkbox{
        margin: 0;
        margin-right: 15px;
        height: 20px;
        transform: scale(1.5);
    }
</style>