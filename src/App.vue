<template>


    <v-layout>
        <v-system-bar color="grey-darken-3"></v-system-bar>

        <v-navigation-drawer color="grey-darken-2"></v-navigation-drawer>

        <v-app-bar color="grey" flat></v-app-bar>
        <v-main class="d-flex align-center text-h5">
            <div v-for="name in names" :key="name">
                <div>
                    <h3>{{ name }}</h3>
                    <input type="radio" :name="name" :id="`${name}Yes`" value="yes" v-model="checkedStatus[name]">
                    <label :for="`${name}Yes`">Yes</label>
                    <input type="radio" :name="name" :id="`${name}No`" value="no" v-model="checkedStatus[name]">
                    <label :for="`${name}No`">No</label>
                </div>

            </div>
            <div>
            <h1>Hello World</h1>
            <textarea>{{ checkedNames }}</textarea>

            <textarea>{{ uncheckedNames }}</textarea>
            </div>
        </v-main>
    </v-layout>
</template>

<script>
export default {
    data() {
        return {
            names: ["Frage 1", "Frage 2", "Frage 3", "Frage 4", "Frage 5"],
            checkedStatus: {},
            checkedNames: [],
            uncheckedNames: []
        };
    },
    watch: {
        checkedStatus: {
            deep: true,
            handler(newVal) {
                this.checkedNames = Object.keys(newVal).filter(
                    name => newVal[name] === "yes"
                );
                this.uncheckedNames = Object.keys(newVal).filter(
                    name => newVal[name] === "no"
                );
            }
        }
    },
    mounted() {
        this.names.forEach(name => {
            this.$set(this.checkedStatus, name, null);
        });
    }
};
</script>
