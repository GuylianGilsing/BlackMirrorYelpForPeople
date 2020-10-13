<template>
    <header id="navbar-main">
        <nav class="container">
            <ProfileIcon v-if="!profileIsOpen" href="/profile" src="./img/profile/placeholder.png" alt="test" size="1" />
            <div v-else class="close-icon"></div>
            
            <a v-if="!newPostIsOpen" href="/post/new" class="new-post-icon">
                <i class="fas fa-camera"></i>
            </a>
            <div v-else class="close-icon"></div>
        </nav>
    </header>
</template>

<script>
import ProfileIcon from '@/components/ProfileIcon.vue'

export default {
    name: 'NavbarMain',
    components: {
        'ProfileIcon': ProfileIcon
    },
    data()
    {
        return {
            profileIsOpen: false,
            newPostIsOpen: false
        }
    }
}
</script>

<style lang="scss" scoped>
header{
    margin: 1.5rem 0px;

    nav{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
    }

    .new-post-icon{
        display: block;
        color: #fff;
        font-size: 2rem;
    }

    .close-icon{
        width: 2rem;
        height: 2rem;
        position: relative;
        display: block;

        &::before, &::after{
            content: '';
            width: 15%;
            height: 100%;
            top: 0px;
            left: 41%;
            position: absolute;
            display: block;
            background-color: #fff;
        }

        &::before{
            transform: rotate(45deg);
        }

        &::after{
            transform: rotate(-45deg);
        }
    }
}
</style>