
<template>
  <div id="footer">
        <span>Power by {{author}}，欢迎访问</span>
        <br/>
        <span>Welcome hello</span>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                author: "熊文轩"
            }
        }
    }
</script>

<style lang="less" scoped>
    #footer {
    margin: 40px;
    text-align: center;
    color: #eee;
    font-size: 15px;
    text-shadow: 0 3px 0 2px #eee;
    }
</style>

