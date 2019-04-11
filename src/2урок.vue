<template>
    <div class="container">
        <form v-if="show">
            <p>Email</p>
            <input type="text" v-model="email">
            <p>First Name</p>
            <input type="text" v-model="firstName">
            <p>Last Name</p>
            <input type="text" v-model="lastName">
            <p>Phone</p>
            <input type="text" v-model="phone">
            <span>Guests</span> <button class="addGuest btn-primary" @click.prevent="addGuest"> + </button><br>
            <div class="guests" v-for="(item,index) in guestList">
                <p v-on:dblclick="delGuest(index)">{{ index + 1}} Guest Name</p>
                <input type="text" v-model="item.name">
            </div>
            <button class="btn-success mt-4" @click.prevent="Done">Send Form</button>

        </form>
        <div class="result" v-if="!show">
            <table border="bordered">
                <tr>
                    <td>Email</td>
                    <td>{{ email }}</td>
                </tr>
                <tr>
                    <td>Name</td>
                    <td>{{ firstName }}</td>
                </tr>
                <tr>
                    <td>Lastname</td>
                    <td>{{ lastName }}</td>
                </tr>
                <tr>
                    <td>Phone</td>
                    <td>{{ phone }}</td>
                </tr>

                <tr>
                    <td>Guests</td>
                    <td>
                        <ol>
                            <li v-for="item in guestList"> {{item.name}} </li>
                        </ol>
                    </td>
                </tr>
            </table>
            <button class="btn-primary mt-3" v-on:click="show=!show">Назад</button>

        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            email: "",
            firstName: "",
            lastName: "",
            phone: "",
            guestList: [],
            ready: "",
            show: true
        }
    },
    methods: {
        addGuest() {
            if (this.guestList.length < 5) {
                this.guestList.push({});
            } else alert("max guests is 5")
        },
        Done() {
            this.show = !this.show;
        },
        delGuest(index) {
            this.guestList.splice(index, 1);
        }
    },
    computed: {},
    components: {
        appProgress: progress
    }
};

</script>

<style scoped>
.container {}

form,
.result {
    display: block;
    width: 40%;
    margin: 0 auto;

}

table {
    width: 100%;
}

td {
    width: 50%;
}

input {
    width: 100%;
    margin-bottom: 10px;
}

p {
    margin: 0 auto;
    font-weight: 700;
}

</style>
