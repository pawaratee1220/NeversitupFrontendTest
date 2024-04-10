<template>
  <div class="d-flex align-center justify-center">
    <v-sheet width="500" class="mx-auto my-5">
      <v-card style="padding: 20px">
        <v-row>
          <v-col>
            <v-card
              v-for="(item, index) in items"
              :key="index"
              style="
                background-color: #ffebee;
                padding: 5px;
                margin-bottom: 15px;
              "
            >
              <v-row>
                <v-col>
                  <h5>TODO TITLE</h5>
                </v-col>
                <v-col class="text-right">
                  <v-btn
                    variant="text"
                    density="compact"
                    icon="mdi-close"
                    @click="onDelete(index)"
                  >
                  </v-btn>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  {{ item.title }}
                  <v-btn
                    variant="text"
                    density="compact"
                    icon="mdi-pencil"
                    color="info"
                    @click="onEdit(item, index)"
                    ></v-btn
                  >
                </v-col>
              </v-row>
              <v-row>
                <v-col class="text-right">
                  {{ formatDate(item.createDate) }}
                </v-col>
              </v-row>
            </v-card>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-btn
              density="compact"
              class="bg-info text-none"
              @click="onCreate()"
              >Create</v-btn
            >
          </v-col>
        </v-row>
      </v-card>
    </v-sheet>
    <!-- <pre>{{ items }}</pre> -->
  </div>

  <v-dialog v-model="isShow" max-width="600">
    <v-card style="padding: 10px">
      <v-card-text>
        <v-row>
          <v-col>
            <v-textarea label="Title" v-model="formData.title"></v-textarea>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-textarea
              label="Description"
              v-model="formData.desc"
            ></v-textarea>
          </v-col>
        </v-row>
      </v-card-text>
      <v-divider></v-divider>
      <v-card-actions>
        <v-spacer></v-spacer>

        <v-btn text="Cancel" variant="plain" @click="isShow = false"></v-btn>

        <v-btn
          color="primary"
          text="Create"
          variant="tonal"
          @click="onSave"
        ></v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script setup>
const isShow = ref(false);
const formData = ref({
  title: "",
  desc: "",
  createDate: null,
  index: null,
});
const items = ref([]);

const onCreate = () => {
  isShow.value = true;
  formData.value.title = "";
  formData.value.desc = "";
  formData.value.createDate = null;
  formData.value.index = null
};
const onSave = () => {
  console.log("hh", formData.value.index);
  if (formData.value.index != null) {
    items.value.forEach((x, i) => {
      if (i == formData.value.index) {
        x.title = formData.value.title;
        x.desc = formData.value.desc;
        x.createDate = formData.value.createDate;
      }
    });
  } else {
    formData.value.createDate = new Date();

    const newValue = {
      title: formData.value.title,
      desc: formData.value.desc,
      createDate: formData.value.createDate,
    };
    items.value.push(newValue);
  }

  isShow.value = false;
};
const formatDate = (date) => {
  if (date) {
    let day = date.getDate();
    let month = date.getMonth();
    let newMonth = month < 10 ? "0" + (month + 1) : month + 1;
    let year = date.getFullYear();

    return `${day}-${newMonth}-${year}`;
  }
};

const onEdit = (item, index) => {
  isShow.value = true;
  formData.value.title = item.title;
  formData.value.desc = item.desc;
  formData.value.createDate = item.createDate;
  formData.value.index = index;
};
const onDelete = (index) => {
  items.value.splice(index, 1);
};
</script>
