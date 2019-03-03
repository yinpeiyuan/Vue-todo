<template>
    <div>
        <footer id="footer" >written by {{author}}</footer>
    </div>
</template>

<script>
export default {
    data() {
        return {
            author: '阿原'
        }
    },

}
</script>


<style lang="stylus" scoped>
#footer{
    margin-top 40px
    text-align center
    color red
    font-size 20px
    text-shadow 0 1px   #ffffff


}
    
</style>