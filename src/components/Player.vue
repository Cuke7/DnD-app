<template>
    <v-card class="my-6 mx-auto" max-width="1500" dense>
        <v-row align="center" justify="space-around">
            <v-col cols="2" class="text-center">
                <v-avatar size="150">
                    <img alt="Avatar" :src="player.avatar_url" />
                </v-avatar>
            </v-col>
            <v-col cols="5" class="text-center">
                <v-row>
                    <strong>{{ player.nom }}</strong>
                </v-row>
                <v-row>
                    <v-simple-table dense>
                        <thead>
                            <tr>
                                <th>FOR</th>
                                <th>DEX</th>
                                <th>CON</th>
                                <th>INT</th>
                                <th>SAG</th>
                                <th>CHA</th>
                            </tr>
                        </thead>
                        <tbody>
                            <td v-for="(value, index) in player.caracs" v-bind:key="index">
                                <v-chip color="grey" class="ma-2 black--text" label small>{{ value }}</v-chip>
                            </td>
                        </tbody>
                    </v-simple-table>
                </v-row>
            </v-col>

            <v-col cols="2">
                <v-chip-group column>
                    <v-chip color="red lighten-4" class="ml-0 mr-2 black--text" label small>{{ player.type }}</v-chip>
                    <v-chip color="blue lighten-4" class="ml-0 mr-2 black--text" label small>{{ player.alignement }}</v-chip>
                    <v-chip color="green lighten-4" class="ml-0 mr-2 black--text" label small>{{ player.vitesse_details }}</v-chip>
                    <v-chip color="green lighten-4" class="ml-0 mr-2 black--text" label small>{{ player.taille }}</v-chip>
                </v-chip-group>
            </v-col>

            <v-col cols="2">
                <v-row>
                    <v-text-field class="ma-2" hide-details color="red" label="PV" prepend-inner-icon="mdi-heart" v-model="player.PV"></v-text-field>
                </v-row>
                <v-row>
                    <v-text-field class="ma-2" hide-details color="blue" label="CA" prepend-inner-icon="mdi-shield" v-model="player.CA"></v-text-field>
                </v-row>
                <v-row>
                    <v-text-field class="ma-2" hide-details color="green" label="Init" prepend-inner-icon="mdi-fast-forward" v-model="player.init"></v-text-field>
                </v-row>
            </v-col>

            <v-col cols="1">
                <v-btn icon @click="show = !show">
                    <v-icon>{{ show ? "mdi-chevron-up" : "mdi-chevron-down" }}</v-icon>
                </v-btn>
            </v-col>
        </v-row>

        <v-expand-transition>
            <div v-show="show">
                <v-divider></v-divider>

                <v-card-text>
                    I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for sleeping, soldier, not with all the bed making you'll be doing. Then we'll
                    go with that data file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to escape.
                </v-card-text>
            </div>
        </v-expand-transition>
    </v-card>
</template>
<script>
export default {
    name: "Player",
    props: ["player"],
    data: () => ({
        show: false,
    }),
};
</script>
