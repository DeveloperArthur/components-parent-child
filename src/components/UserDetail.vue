<template>
    <div class="component">
        <h3>You may view the User Details here</h3>
        <p>Many Details</p>
        <p>User name: {{ switchName() }}</p>
        <p>User age: {{ userAge }}</p>
        <button @click="resetName">Reset Name</button>
        <button @click="resetFn()">Reset Name</button>
    </div>
</template>
    
<script>
    import { eventBus } from '../main';

    export default{
        props: {
            MyName: {
                type: String
            },
            resetFn: Function,
            userAge: Number
        },
        created(){
            console.log('Passei pelo UserDetail');
            eventBus.$on('ageWasEdited', (age) => {
                this.userAge = age;
            });
        },
        methods: {
            switchName(){
                return this.MyName.split("").reverse("").join("");
            },
            resetName(){
                this.MyName = 'Arthur';
                this.$emit('nameWasReset', this.MyName);
            }
        }
    }
</script>

<style scoped>
    div {
        background-color: lightcoral;
    }
</style>
