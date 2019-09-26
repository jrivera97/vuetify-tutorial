<template>
    <div class="Dashboard">
        <h1 class="subtitle-1 grey--text">
            Dashboard
        </h1>
        <v-container class="my-5">

            <v-layout row class="mb-3">
                <v-tooltip top>
                    <template v-slot:activator="{ on }">
                        <v-btn small text color="grey" @click="sortBy('title')" v-on="on">
                            <v-icon left small>folder</v-icon>
                            <span class="caption text-lowercase">By Project Name</span>
                        </v-btn>
                    </template>
                    <span>Sort projects by project name</span>
                </v-tooltip>
                <v-tooltip top>
                    <template v-slot:activator="{ on }">
                        <v-btn small text color="grey" @click="sortBy('person')" v-on="on">
                            <v-icon left small>person</v-icon>
                            <span class="caption text-lowercase">By Person</span>
                        </v-btn>
                    </template>
                    <span>Sort projects by person</span>
                </v-tooltip>
            </v-layout>

            <v-card class="pl-2" v-for="project in projects" :key="project.title">
                <v-layout row :class="`pa-3 project ${project.status}`">
                    <v-flex xs12 md6 class="pa-3">
                        <div class="caption grey--text">Project Title</div>
                        <div>{{project.title}}</div>
                    </v-flex>
                    <v-flex xs6 sm4 md2 class="pa-3">
                        <div class="caption grey--text">Person</div>
                        <div>{{project.person}}</div>
                    </v-flex>
                    <v-flex xs6 sm4 md2 class="pa-3">
                        <div class="caption grey--text">Due by</div>
                        <div>{{project.due}}</div>
                    </v-flex>
                    <v-flex xs2 sm4 md2>
                        <div class="right">
                            <v-chip small class="white--text my-2 caption"
                                    :style="getChipColor(project.status)">{{
                                                                          project.status
                                                                          }}
                            </v-chip>
                        </div>
                    </v-flex>
                </v-layout>
            </v-card>
        </v-container>

    </div>
</template>

<script>
    import db from '@/fb'

    export default {
        data() {
            return {
                chipColor: null,
                projects: [
                //     {
                //         title: 'Design a new website',
                //         person: 'The Net Ninja',
                //         due: '1st Jan 2019',
                //         status: 'ongoing',
                //         content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'
                //     },
                //     {
                //         title: 'Code up the homepage',
                //         person: 'Chun Li',
                //         due: '10th Jan 2019',
                //         status: 'complete',
                //         content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'
                //     },
                //     {
                //         title: 'Design video thumbnails',
                //         person: 'Ryu',
                //         due: '20th Dec 2018',
                //         status: 'complete',
                //         content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'
                //     },
                //     {
                //         title: 'Create a community forum',
                //         person: 'Gouken',
                //         due: '20th Oct 2018',
                //         status: 'overdue',
                //         content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'
                //     },
                 ]
            }
        },
        methods: {
            getChipColor(status) {
                if (status === "ongoing") {
                    return "background: #ffaa2c"
                } else if (status === "complete") {
                    return "background: #3cd1c2"
                } else {
                    return "background: #f83e70"
                }
            },
            sortBy(preference) {
                //cool ternary sort method, not very efficient though
                this.projects.sort((a, b) => a[preference] < b[preference] ? -1 : 1)
            }
        },

        created() {
            db.collection('projects').onSnapshot(res => {
                const changes = res.docChanges();

                changes.forEach(change => {
                    if(change.type === 'added') {
                        this.projects.push({
                            ...change.doc.data(),
                            id: change.doc.id
                        })
                    }
                })
            })
        }

    }


</script>

<style>
    .project.complete {
        border-left: 4px solid #3cd1c2;
    }

    .project.ongoing {
        border-left: 4px solid orange;
    }

    .project.overdue {
        border-left: 4px solid tomato;
    }
</style>