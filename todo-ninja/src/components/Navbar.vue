<template>
    <nav>

        <v-snackbar v-model="thnacks" :timeout="4000" top color="#3cd1c2">
            <span>Your Project Has Been Added!</span>
            <v-btn text color="white" @click="thnacks=false">Close</v-btn>
        </v-snackbar>
        <v-app-bar flat app>
            <v-app-bar-nav-icon class="grey--text" v-on:click="drawer = !drawer"></v-app-bar-nav-icon>
            <v-toolbar-title class="grey--text text-uppercase">
                <span class="font-weight-light">Todo</span>
                <span>Ninja</span>
            </v-toolbar-title>


            <v-spacer></v-spacer>



            <!--- dropdown menu -->

            <div class="text-center">
                <v-menu offset-y>
                    <template v-slot:activator="{ on }">
                        <v-btn text v-on="on" color="grey">
                            <v-icon left>expand_more</v-icon>
                            <span>menu</span>
                        </v-btn>
                    </template>
                    <v-list>
                        <v-list-item v-for="(link,i) in links" :key="i" router :to="link.route">
                           <v-list-item-title>
                               {{ link.text }}
                           </v-list-item-title>
                        </v-list-item>
                    </v-list>
                </v-menu>
            </div>

            <v-btn text color="grey">
                <span>Sign Out</span>
                <v-icon right>exit_to_app</v-icon>
            </v-btn>
        </v-app-bar>

        <v-navigation-drawer class="purple" app v-model="drawer">
            <v-layout column align-center>
                <v-flex class="mt-5">
                    <v-avatar size="100">
                        <img src="/avatar-1.png" alt="">
                    </v-avatar>
                    <p class="white--text subtitle-1 mt-1 align-center">
                        The Net Ninja
                    </p>
                </v-flex>
                <v-flex class="mt-4 mb-3">
                    <Popup @projectAdded="thnacks=true"></Popup>
                </v-flex>
                <v-list>
                    <v-list-item v-for="(link,index) in links" :key="index" router :to="link.route">
                        <v-list-item-action>
                            <v-icon class="white--text">
                                {{ link.icon }}
                            </v-icon>
                        </v-list-item-action>
                        <v-list-item-content>
                            <v-list-item-title class="white--text">
                                {{ link.text }}
                            </v-list-item-title>
                        </v-list-item-content>
                    </v-list-item>
                </v-list>
            </v-layout>
        </v-navigation-drawer>
    </nav>
</template>

<script>
    import Popup from './Popup'
    export default {
        components: {
            Popup
        },
        data() {
            return {
                drawer: false,
                links: [
                    {icon: 'dashboard', text: 'Dashboard', route: '/'},
                    {icon: 'folder', text: 'My Projects', route: 'project'},
                    {icon: 'person', text: 'Team', route: '/team'},
                ],
                thnacks: false
            }
        }
    }
</script>