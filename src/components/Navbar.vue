<template>
    <nav>
        <v-toolbar flat flameapp>
            <v-toolbar-side-icon class="grey-text" @click="drawer = !drawer"></v-toolbar-side-icon>

            <v-toolbar-title class="text-uppercase grey--text">
                <span class="font-weight-light">Todo</span>
                <span>Ninja</span>

            </v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn flat color="grey">
                <span>Sign Out</span>
                <v-icon right>exit_to_app</v-icon>
            </v-btn>
        </v-toolbar>

        <v-navigation-drawer v-model="drawer" flameapp class="indigo">
            <p>test</p>
        </v-navigation-drawer>
    </nav>
</template>

<script>
export default {
    data(){
        return{
            drawer: false
        }
    }
}
</script>

<style>


</style>