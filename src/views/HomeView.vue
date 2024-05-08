<template>
  <v-data-table
    :headers="headers"
    :items="desserts"
    item-value="name"
  >
    <template v-slot:headers="{ columns, isSorted, getSortIcon, toggleSort }">
      <tr>
        <template v-for="column in columns" :key="column.key">
          <td>
            <span class="mr-2 cursor-pointer" @click="() => toggleSort(column)">{{ column.title }}</span>
            <template v-if="isSorted(column)">
              <v-icon :icon="getSortIcon(column)"></v-icon>
            </template>
            <v-btn color="red" @click="() => remove(column.key)">Supprimer</v-btn>
          </td>
        </template>
        <td>
          <v-btn
            class="mb-2"
            color="primary"
            dark
            @click="openDialog"
          >
            Ajouter une catégorie
          </v-btn>
        </td>
      </tr>
    </template>
  </v-data-table>

  <v-dialog v-model="dialog" max-width="500px">
    <v-card>
      <v-card-title>
        <span class="text-h5">{{ formTitle }}</span>
      </v-card-title>

      <v-card-text>
        <v-container>
          <v-row>
            <v-col
              cols="12"
              md="4"
              sm="6"
            >
              <v-text-field
                v-model="editedItem.name"
                label="Nom de catégorie"
              ></v-text-field>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
          color="blue-darken-1"
          variant="text"
          @click="close"
        >
          Cancel
        </v-btn>
        <v-btn
          color="blue-darken-1"
          variant="text"
          @click="save"
        >
          Save
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data() {
    return {
      dialog: false,
      formTitle: 'New Item',
      editedItem: {
        name: ''
      },
      headers: [
        {
          title: 'Nom',
          align: 'start',
          key: 'name',
          sortable: false,
          removable: false,
        },
        { title: 'Calories', key: 'calories', removable: true },
        { title: 'Fat (g)', key: 'fat', removable: true },
        { title: 'Carbs (g)', key: 'carbs', removable: true },
        { title: 'Protein (g)', key: 'protein', removable: true },
        { title: 'Iron (%)', key: 'iron', removable: true },
      ],
      desserts: [
        {
          name: 'Frozen Yogurt',
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: 1,
        },
        {
          name: 'Ice cream sandwich',
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: 1,
        },
        {
          name: 'Eclair',
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: 7,
        },
        {
          name: 'Cupcake',
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: 8,
        },
        {
          name: 'Gingerbread',
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          iron: 16,
        },
        {
          name: 'Jelly bean',
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: 0,
        },
        {
          name: 'Lollipop',
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: 2,
        },
        {
          name: 'Honeycomb',
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: 45,
        },
        {
          name: 'Donut',
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          iron: 22,
        },
        {
          name: 'KitKat',
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: 6,
        },
      ]}},
  methods: {
    remove(key) {
      this.headers = this.headers.filter(header => header.key !== key);
      this.desserts.forEach(item => delete item[key]);
    },
    add(key) {
      this.headers.push({ title: key, key: key, removable: true });
      this.desserts.forEach(item => { item[key] = "No data yet"; });
    },
    openDialog() {
      this.dialog = true;
    },
    close() {
      this.dialog = false;
    },
    save() {
      this.add(this.editedItem.name);
      this.dialog = false;
    }
  }
}
</script>
