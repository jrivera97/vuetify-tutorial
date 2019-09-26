<template>
    <div class="Team">
        <h1 class="subtitle-1 grey--text">
            Team
        </h1>
        <v-container class="my-5">
            <v-layout row>
                <v-flex xs12 sm6 md4 lg3 v-for="(person, index) in team" :key="index">
                    <v-card  class="ma-3">

                            <v-responsive class="text-sm-center">
                                <v-avatar size="100" class="pt-3">
                                    <img class="pt-3" :src="person.avatar">
                                </v-avatar>
                            </v-responsive>
                        <v-card-text class="text-sm-center">
                            <div class="subtitle-1" style="color: black">{{person.name}}</div>
                            <div class="grey--text">{{person.role}}</div>
                        </v-card-text>
                        <v-card-actions>
                            <v-btn text color="grey">
                                <v-icon small left>message</v-icon>
                                <span>message</span>
                            </v-btn>
                        </v-card-actions>
                    </v-card>
                </v-flex>
            </v-layout>



        </v-container>


    </div>
</template>

<script>
    export default {
     data() {
         return {
             team: [
                 { name: 'The Net Ninja', role: 'Web developer' , avatar: '/avatar-1.png'},
                 { name: 'Ryu', role: 'Graphic designer' , avatar: '/avatar-2.png'},
                 { name: 'Chun Li', role: 'Web developer' , avatar: '/avatar-3.png'},
                 { name: 'Gouken', role: 'Social media maverick' , avatar: '/avatar-4.png'},
                 { name: 'Yoshi', role: 'Sales guru', avatar: '/avatar-5.png'}
             ]
         }
     }
    }
</script>