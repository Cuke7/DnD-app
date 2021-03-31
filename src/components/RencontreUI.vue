<template>
    <v-row class="ma-6" justify="space-around" align="center">
        <v-col cols="3">
            <v-range-slider color="primary" track-color="secondary" thumb-label="always" persistent-hint hint="Niveau de FP" v-model="FP_range" max="33" min="0" step="1">
                <template v-slot:thumb-label="{ value }">
                    {{ values[value] }}
                </template>
            </v-range-slider>
        </v-col>
        <v-col cols="3">
            <v-select v-model="al1" :items="align1" label="Morale"></v-select>
            <v-select v-model="al2" :items="align2" label="Éthique"></v-select>
        </v-col>
        <v-col cols="2">
            <v-text-field v-model="number" label="Nombre de monstres"></v-text-field>
        </v-col>
        <v-col cols="2">
            <v-switch v-model="ident" :label="`Monstres identiques`"></v-switch>
        </v-col>

        <v-col cols="2">
            <v-btn :loading="loading" color="primary" @click="generate_rencontre()">Generate</v-btn>
        </v-col>
    </v-row>
</template>
<script>
export default {
    name: "Monster",
    data: () => ({
        loading: false,
        ident: true,
        FP_range: [3, 11],
        al1: "Tout",
        al2: "Tout",
        align2: ["Bon", "Neutre", "Mauvais", "Tout"],
        align1: ["Loyal", "Neutre", "Chaotique", "Tout"],
        number: "3",
        values: ["0", "1/8", "1/4", "1/2", 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30],
        values2: [0, 0.125, 0.25, 0.5, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30],
    }),
    methods: {
        generate_rencontre: function() {
            this.loading = true;
            let key = 0;
            get_data_from_server(this.url).then((data) => {
                this.loading = false;
                if (data[0] == null) {
                    this.monsters = [];
                    console.log("Nothing found");
                    this.$emit("newMonsters", this.monsters);
                } else {
                    for (const monster of data) {
                        monster.show = false;
                        monster.key = key;
                        key++;
                        this.nothing = false;
                    }
                    this.monsters = data;
                    this.$emit("newMonsters", this.monsters);
                }
            });
        },
    },

    computed: {
        url: function() {
            let FPmin = this.values2[this.FP_range[0]];
            let FPmax = this.values2[this.FP_range[1]];
            let number = this.number;
            let ident = this.ident;

            let align = "";

            switch (this.al1) {
                case "Loyal":
                    align = "L";
                    break;
                case "Neutre":
                    align = "N";
                    break;
                case "Chaotique":
                    align = "C";
                    break;
                case "Tout":
                    align = "A";
                    break;
            }

            switch (this.al2) {
                case "Bon":
                    align = align + "B";
                    break;
                case "Neutre":
                    align = align + "N";
                    break;
                case "Mauvais":
                    align = align + "M";
                    break;
                case "Tout":
                    align = align + "A";
                    break;
            }

            return "https://my-servo.herokuapp.com/monsterAPI/get_rencontre?FPmin=" + FPmin + "&FPmax=" + FPmax + "&alignement=" + align + "&number=" + number + "&ident=" + ident;
        },
    },
};

function get_data_from_server(url) {
    console.log(url);
    return fetch(url)
        .then((response) => {
            return response.json();
        })
        .catch(() => {
            return null;
        });
}
</script>
