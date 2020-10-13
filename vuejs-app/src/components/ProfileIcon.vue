<template>
    <a :href="href" class="profile-icon" :class="imgSize">
        <img :src="src" :alt="alt">
    </a>
</template>

<script>
export default {
    name: 'ProfileIcon',
    props: ["href", "src", "alt", "size"],
    data()
    {
        return {
            imgSize: (this.size.length > 0) ? `size-${ this.size }` : 'size-1'
        }
    }
}
</script>

<style lang="scss">
.profile-icon{
    width: 100%;
    padding-bottom: 100%;
    position: relative;
    display: block;
    border-radius: 50%;
    overflow: hidden;

    img{
        widows: 100%;
        height: 100%;
        top: 0px;
        left: 0px;
        position: absolute;
        display: block;
        object-fit: cover;
    }

    &.size-1{
        width: 48px;
        padding-bottom: 48px;
    }

    &.size-2{
        width: 96px;
        padding-bottom: 96px;
    }

    &.size-3{
        width: 160px;
        padding-bottom: 160px;
    }
}
</style>