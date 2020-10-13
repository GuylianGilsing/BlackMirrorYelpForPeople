<template>
    <div class="account-post">
        <div class="account-info">
            <div>
                <ProfileIcon href="/" src="./img/profile/placeholder.png" alt="Profile card icon" size="2" />
            </div>
            <div class="name-and-rating">
                <p class="username">{{ username }}</p>
                <p class="rating">{{ rating }}</p>
            </div>
        </div>
        <div class="content">
            <p>{{ content['top-text'] }}</p>
            <img :src="content['images'][0]" alt="">  
        </div>
        <div class="rating">
            <p><i class="fas fa-star"></i> {{ content['rating-5-star-amount'] }} people rated this 5 stars</p>
        </div>
        <div class="comments">
            <p>Comments</p>
            <div class="divider"></div>
            <div class="comment">
                <i class="like-icon fas fa-heart liked"></i>
                <p class="name">Harry Sunweb</p>
                <p class="content">What do you get when you cross a mentally...</p>
            </div>
            <a href="/" class="read-more">Read more</a>
        </div>
    </div>
</template>

<script>
import ProfileIcon from '@/components/ProfileIcon.vue';

export default {
    name: 'AccountPost',
    components: {
        ProfileIcon
    },
    data()
    {
        return {
            username: 'Johny James',
            rating: 3.8,
            content: {
                'top-text': "Hello World!",
                'images': ['./img/posts/placeholder.png'],
                'rating-5-star-amount': 17
            }
        }
    }
}
</script>

<style lang="scss">
.account-post{
    .account-info{
        margin-bottom: 1.2rem;
        display: grid;
        grid-template-columns: 1fr 2fr;
        grid-template-rows: 1fr;

        .profile-icon{
            margin-right: 1.5rem;
        }

        .username{
            margin-top: 0.8rem;
            font-size: 1.5rem;
        }

        .rating{
            margin-top: 0.2rem;
            font-size: 1.8rem;
        }
    }

    .content{
        font-size: 1.125rem;

        img{
            width: 100%;
            height: auto;
            margin: 0.5rem 0px;
            display: block;
            object-fit: cover;
        }
    }

    & > .rating{
        margin-bottom: 1.5rem;
    }

    .comments{
        .comment{
            position: relative;
            font-size: 0.9rem;

            .like-icon{
                top: 0.35em;
                right: 0.5em;
                position: absolute;
                font-size: 1em;

                &.liked{
                    color: #FF3434;
                }
            }

            .name{
                font-weight: 600;
            }

            .content{
                margin-top: 0.2em;
                padding-right: 0.8em;
                font-size: 1em;
            }
        }

        .read-more{
            font-weight: 600;
            text-decoration: none;
        }
    }
}
</style>