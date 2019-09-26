<template>
    <v-dialog max-width="600px" v-model="modal">
        <template v-slot:activator="{ on }">
            <v-btn text dark style="background: #3cd1c2" v-on="on">Add a new project</v-btn>
        </template>
        <v-card>
            <v-card-title>
                <h2>Add a New Project</h2>
                <v-card-text>
                    <v-form class="px-3" ref="form">
                        <v-text-field label="Title" v-model="title" prepend-icon="folder" :rules="inputRules"></v-text-field>
                        <v-textarea label="Information" v-model="content" prepend-icon="edit" :rules="inputRules"></v-textarea>

                        <v-menu>
                            <template v-slot:activator="{ on }">
                                <v-text-field v-on="on" :value="due" label="Due Date" prepend-icon="date_range" :rules="inputRules"></v-text-field>
                            </template>
                            <v-date-picker v-model="due"></v-date-picker>
                        </v-menu>

                        <v-spacer></v-spacer>
                        <v-btn :loading="loading"
                               :disabled="loading" text dark style="background: #3cd1c2" @click="submit" class="mx-0 mt-3" >
                            Add Project
                        </v-btn>

                    </v-form>
                </v-card-text>
            </v-card-title>
        </v-card>


    </v-dialog>
</template>

<script>
import db from'@/fb'
    export default {
        data() {
            return {
                title: '',
                content: '',
                due: '',
                inputRules: [
                    v => v.length >= 3 || 'Minimum length is 3 characters'
                ],
                loading: false,
                modal: false
            }
        },
        methods: {
            submit() {
                if(this.$refs.form.validate()) { //use refs to get input from form, need refs= hmtl tag
                    this.loading = true;
                    const project = {
                        title: this.title,
                        content: this.content,
                        due: this.due,
                        person: "The Net Ninja",
                        status: 'ongoing'
                    };

                    db.collection('projects').add(project).then(() => {
                        // eslint-disable-next-line no-console
                        this.loading = false;
                        this.modal=false;
                        this.$emit('projectAdded')
                    });
                }

            }
        }
    }
</script>