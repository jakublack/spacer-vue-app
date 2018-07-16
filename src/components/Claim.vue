<template>

    <div class="claim-wrapper">
        <h1 class="claim">Spacer</h1>
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
    }

    .sub-claim {
        font-size: 1rem;
        margin: 30px 0 0 0;
    }


</style>
