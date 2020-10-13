<template>
    <div class="star-rating-bar" :id="`star-rating-bar-${ id }`">
        <div class="stars" @click.stop="RegisterRating">
            <input type="radio" name="starrating[]" :id="`star-rating-bar-${ this.id }-star5`" data-rating="5">
            <label :for="`star-rating-bar-${ this.id }-star5`" class="star fas fa-star"></label>
            <input type="radio" name="starrating[]" :id="`star-rating-bar-${ this.id }-star4`" data-rating="4">
            <label :for="`star-rating-bar-${ this.id }-star4`" class="star fas fa-star"></label>
            <input type="radio" name="starrating[]" :id="`star-rating-bar-${ this.id }-star3`" data-rating="3">
            <label :for="`star-rating-bar-${ this.id }-star3`" class="star fas fa-star"></label>
            <input type="radio" name="starrating[]" :id="`star-rating-bar-${ this.id }-star2`" data-rating="2">
            <label :for="`star-rating-bar-${ this.id }-star2`" class="star fas fa-star"></label>
            <input type="radio" name="starrating[]" :id="`star-rating-bar-${ this.id }-star1`" data-rating="1">
            <label :for="`star-rating-bar-${ this.id }-star1`" class="star fas fa-star"></label>
        </div>
    </div>
</template>

<script>
export default {
    name: 'StarRatingBar',
    props: ["id"],
    methods: {
        RegisterRating(e)
        {
            if(e.target instanceof Object && e.target.nodeName == "INPUT")
            {
                // Get the selected star
                let selectedStar = this.GetSelectedStar();
                if(selectedStar != null)
                {
                    if(!selectedStar.hasAttribute('data-rating'))
                    {
                        selectedStar.checked = false;
                        return;
                    }

                    let starAmount = selectedStar.getAttribute('data-rating');

                    // Emit the rated event
                    this.$emit('rated', starAmount);
                }
            }
        },
        // This method can be called outside of the component
        ResetRating()
        {
            let selectedStar = this.GetSelectedStar();
            if(selectedStar != null)
                selectedStar.checked = false;
        },
        GetSelectedStar()
        {
            let activeStar = null;

            // Get the amount of stars
            let starContainer = document.querySelector(`#star-rating-bar-${ this.id } .stars`);

            // Get the current selected star
            let selectedStar = starContainer.querySelector('input:checked');
            if(selectedStar instanceof Object)
                activeStar = selectedStar;

            return activeStar;
        }
    }
}
</script>

<style lang="scss">
.star-rating-bar{
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;

    .stars{
        .star{
            padding: 0px 0.35rem;
            font-size: 2rem;
            float: right;
        }

        & > input{
            display: none;
        }

        & > input:checked + .star{
            color: #A751CC;
        }

        & > input:checked ~ .star{
            color: #A751CC;
        }

        & > input:not(:checked) ~ .star:hover,
        & > input:not(:checked) ~ .star:hover ~ .star{
            color: #A751CC;
        }
    }
}
</style>