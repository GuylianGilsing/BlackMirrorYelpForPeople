<template>
  <main id="view-home" class="home container" @dragstart="RegisterMouseDownClick" @dragend="RegisterMouseUpClick" @drag="MouseDrag" @mousedown="RegisterMouseDownClick" @mouseup="RegisterMouseUpClick" @mousemove="MouseDrag">
    <div class="posts">
        <AccountPost />
    </div>
    <StarRatingBar id="main" ref="StarRatingBar" v-on:rated="RatingGiven" />
    <transition name="fade" v-if="uploading">
        <div id="uploading-post">
            <div v-if="!uploadComplete" class="uploading">
                <i class="fas fa-spinner"></i>
            </div>
            <div v-else class="rated">
                <ProfileIcon src="./img/profile/placeholder.png" size="3" />
                <p>Rated</p>
                <p><i>James {{ starsRated }}</i> stars</p>
            </div>
        </div>
    </transition>
  </main>
</template>

<script>
import AccountPost from '@/components/AccountPost.vue';
import StarRatingBar from '@/components/StarRatingBar.vue';
import ProfileIcon from '@/components/ProfileIcon.vue';

export default {
    name: 'Home',
    components: {
        AccountPost,
        StarRatingBar,
        ProfileIcon
    },
    data()
    {
        return {
            canUpload: false,
            uploading: false,
            uploadComplete: false,

            dragStart: false,
            curDragY: 0,
            lastDragY: 0,
            dragUpTicks: 0,

            starsRated: 0,
        }
    },
    methods: {
        RegisterMouseDownClick()
        {
            this.dragStart = true;
        },
        RegisterMouseUpClick()
        {
            this.dragStart = false;
        },
        MouseDrag(e)
        {
            if(this.dragStart && this.canUpload)
            {
                this.curDragY = e.screenY;

                if(this.curDragY <= this.lastDragY)
                    this.dragUpTicks += 1;

                if(this.dragUpTicks > 60)
                {
                    this.dragUpTicks = 0;
                    this.dragStart = false;
                    this.uploading = true;
                    
                    let postsContainer = document.querySelector(`#view-home .posts`);
                    
                    // Make sure that the postContainer is not in the uploading state
                    if(postsContainer.classList.contains('uploading'))
                        postsContainer.classList.remove('uploading');
                    
                    postsContainer.classList.add('uploading');
                }

                this.lastDragY = this.curDragY;
            }
        },
        RatingGiven(starAmount)
        {
            if(!Number.isSafeInteger(Number(starAmount)))
            {
                this.canUpload = false;
                this.$refs.StarRatingBar.ResetRating();
                return;
            }

            this.canUpload = true;
        }
    }
}
</script>

<style lang="scss">
.home{
    display: flex;
    flex-direction: column;

    & > .posts{
        position: relative;
        flex-grow: 1;

        // Select the first post that has a class that ends with '-post'
        & > div[class$="-post"]:nth-child(1){
            top: 0px;
            position: absolute;
            transition: top 0.5s ease;
        }

        &.uploading > div[class$="-post"]:nth-child(1){
            top: -100vh;
        }

        // Make sure that no text is highlightable
        & *:not([href]){
            pointer-events: none;
            -webkit-touch-callout: none; /* iOS Safari */
            -webkit-user-select: none; /* Safari */
            -khtml-user-select: none; /* Konqueror HTML */
            -moz-user-select: none; /* Old versions of Firefox */
                -ms-user-select: none; /* Internet Explorer/Edge */
                    user-select: none; /* Non-prefixed version, currently
                                        supported by Chrome, Edge, Opera and Firefox */
        }
    }

    & > .star-rating-bar{
        margin: 7vh 0px;
    }
}

#uploading-post{
    top: 50vh;
    left: 50vw;
    position: absolute;
    display: inline-block;
    text-align: center;
    transform: translateX(-50%) translateY(-50%);

    p{
        font-size: 1.35rem;
        font-weight: 300;
    }

    .profile-icon{
        margin: 0 auto;
    }

    .uploading{
        font-size: 3rem;
        animation-name: RotateSpinner;
        animation-duration: 1.2s;
        animation-play-state: running;
        animation-iteration-count: infinite;
        animation-fill-mode: forwards;
        animation-timing-function: linear;
    }
}

@keyframes RotateSpinner
{
    from{transform: rotate(0deg);}
    to{transform: rotate(360deg);}
}
</style>
