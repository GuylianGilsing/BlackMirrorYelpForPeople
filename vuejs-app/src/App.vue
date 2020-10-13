<template>
    <div id="app">
        <NavbarMain />
        <router-view/>
    </div>
</template>

<script>
import NavbarMain from '@/components/NavbarMain.vue';

export default {
    name: 'App',
    components: {
        'NavbarMain': NavbarMain
    }
}
</script>

<style lang="scss">
html, body{
    width: 100vw;
    min-height: 100vh;
    margin: 0px;
    padding: 0px;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    overflow-y: auto;
    color: #fff;
    background-color: #121212;
}

*{
    box-sizing: border-box;
}

:root{
    font-size: 16px;
}

p{
    margin-top: 0.5rem;
    margin-bottom: 0.2rem;
}

a, p, span, div, label, button, input, select, textarea, h1, h2, h3, h4, h5, h6{
    color: inherit;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

main{
    flex-grow: 1;
    margin: 2.5rem 0px;
}

#app{
    height: 100vh;
    display: flex;
    flex-direction: column;
}

.container{
    width: 80%;
    margin-left: auto;
    margin-right: auto;
}

.divider{
    widows: 100%;
    height: 2px;
    display: block;
    background-color: #fff;
}

p ~ .divider{
    margin-bottom: 0.2rem;
}
</style>
