<template >
    <div class="container">
        <h3>{{ this.health }} / 100</h3>
        <div class="healthBar">
            <div class="green" :style="{'width' : this.health + '%'}"></div>
            <div class="red" :style="{'width' : 100 - this.health + '%'}"></div>
        </div>
        <div class="user"></div>
        <button @click="this.handleClick()">take damage</button>
    </div>
    
</template>
<script>
export default {
    name: 'Player',
    data () { 
        return {
            health: 100
        }
    },
    methods: {
        handleClick() { 
            let rand = Math.round(Math.random() *10)
            if (this.health - rand > 0) {
                this.health -= rand
            }else{ 
                this.health = 0 
            }
           
        }
    }
}
</script>
<style lang="css" scoped>
    .user{ 
        width: 200px;
        height: 300px;
        background-color: aqua;
    }
    .green {
        background-color: greenyellow;
        height: 30px;
    }

    .red {
        background-color: red;
        height: 30px;
    }
    .container{ 
        width: 400px;
        height: 800px;
        padding: 15px;
        display: flex;
        flex-direction: column;
        gap: 15px;
        align-items: center;
    }
    .healthBar { 
        display: flex;
        width: 100%;
        height: 30px;
        background-color: white;
        border: 2px solid black;
    }
</style>