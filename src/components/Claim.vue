<template>
    <div class="claim-wrapper">
        <h1 class="claim">SPACER</h1>
        <p class="sub-claim"> Begin you journey through our amazing galazy, and discover places you never even heard of.</p>
        <p class="sub-claim">Type anything space-related to start</p>
    </div>
</template>

<script>
    export default {
        name: 'Claim',
    }
    
</script>

<style lang="scss" scoped>
    .claim-wrapper {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
        color: #fff;
    }

    .claim {
        font-size: 4rem;
        margin: 0;

        @media (min-width: 768px) {
            font-size: 5rem;
        }

        @media (min-width: 1024px) {
            font-size: 6rem;
        }
    }

    .sub-claim {
        font-size: 1rem;
        margin: 30px 0 0 0;
        font-weight: 400;
        @media (min-width: 768px){
            font-size: 1.2rem;
            width: 600px;
            line-height: 1;
            letter-spacing: 1px;
        }
    }


</style>
