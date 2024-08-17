<script setup lang="ts">
  import { ref } from 'vue';
  import Avatar from 'primevue/avatar';
  import Button from 'primevue/button';
  import OverlayBadge from 'primevue/overlaybadge';
  import DataTable from 'primevue/datatable';
  import Column from 'primevue/column';
  import ColumnGroup from 'primevue/columngroup';   // optional
  import Row from 'primevue/row';                   // optional
  import { listOfFiles } from './assets/fake-data';
  import InputIcon from 'primevue/inputicon';
  import InputText from 'primevue/inputtext';
  import IconField from 'primevue/iconfield';
  import MultiSelect from 'primevue/multiselect';
  import Dialog from 'primevue/dialog';
  import FileUpload from 'primevue/fileupload';

  const filters = ref({
    global: { value: null, matchMode: 'contains' },
    filename: { value: null, matchMode: 'contains' },
  });

  const files = ref(listOfFiles)


  const visible = ref(false);
  const fileComment = ref('');
  const currentFile = ref<File | null>(null);

  const showPopup = () => {
      visible.value = true;
  };

  const hidePopup = () => {
      visible.value = false;
  };

  const addFile = () => {
      let file = currentFile.value as File;

      const newFile = {
          filename: file.name,
          category: 'Uncategorized',
          size_bytes: file.size,
          filetype: file.name.split('.').pop(),  
          created_date: new Date().toISOString().split('T')[0],

          description: fileComment.value,
      };

      files.value.push(newFile);

      hidePopup();
  };

  const inputChange = (e: any) => {
    currentFile.value = e.target.files[0]
  }

  const expandedRows = ref([]);

  const onRowExpand = (event) => {
    // console.log('Row expanded:', event.data);
  };

  const onRowCollapse = (event) => {
    // console.log('Row collapsed:', event.data);
  };

</script>

<template>
  <header id="header-desktop" class="flex m-4 border-round p-3 align-items-center justify-content-between shadow-1">
    <section class="flex align-items-center gap-4">
      <div id="logo-container">
        <img width="240" height="35" src="@/assets/immoflow-logo.png" alt="Logo" />
      </div>
      <nav>
        <ul class="flex gap-4">
          <li>
            <Button v-slot="slotProps" label="Dashboard" severity="contrast" asChild>
              <button
                lable="Home"
                v-bind="slotProps.a11yAttrs"
                class=" p-button p-component p-button-text text-white font-bold text-xl"
              >
                <span class="pi pi-home"></span>
                <span>
                  Dashboard
                </span>
              </button>
            </Button>
          </li>
          <li>
            <Button v-slot="slotProps" label="Objekte" severity="contrast" asChild>
              <button
                lable="Objekte"
                v-bind="slotProps.a11yAttrs"
                class=" p-button p-component p-button-text text-white font-bold text-xl"
              >
                <span class="pi pi-building"></span>
                <span>
                  Objekte
                </span>
              </button>
            </Button>
          </li>
          <li>
            <Button v-slot="slotProps" label="Mietverhältnisse" severity="contrast" asChild>
              <button
                lable="Mietverhältnisse"
                v-bind="slotProps.a11yAttrs"
                class=" p-button p-component p-button-text text-white font-bold text-xl"
              >
                <span class="pi pi-th-large"></span>
                <span>
                  Mietverhältnisse
                </span>
              </button>
            </Button>
          </li>
          <li>
            <Button v-slot="slotProps" severity="contrast" asChild>
              <button
                v-bind="slotProps.a11yAttrs"
                class=" p-button p-component p-button-text text-white font-bold text-xl"
              >
                <span class="pi pi-money-bill"></span>
                <span>
                  Nebenkosten
                </span>
              </button>
            </Button>
          </li>
          <li>
            <Button v-slot="slotProps" severity="contrast" asChild>
              <button
                v-bind="slotProps.a11yAttrs"
                class=" p-button p-component p-button-text text-white font-bold text-xl"
              >
                <span class="pi pi-users"></span>
                <span>
                  Kontaktmanager
                </span>
              </button>
            </Button>
          </li>
          <li>
            <Button v-slot="slotProps" severity="contrast" asChild>
              <button
                v-bind="slotProps.a11yAttrs"
                class=" p-button p-component p-button-text text-white font-bold text-xl"
              >
                <span class="pi pi-comments"></span>
                <span>
                  Nachrichten
                </span>
              </button>
            </Button>
          </li>
          <li>
            <Button v-slot="slotProps" severity="contrast" asChild>
              <button
                v-bind="slotProps.a11yAttrs"
                class=" p-button p-component p-button-text text-white font-bold text-xl"
              >
                <span class="pi pi-paperclip"></span>
                <span>
                  Dokumente
                </span>
              </button>
            </Button>
          </li>
        </ul>
      </nav>
    </section>
    <section id="profile">
    <OverlayBadge value="4" severity="danger" class="inline-flex">
        <Avatar label="U" size="xlarge" class="bg-gray-200" />
    </OverlayBadge>    </section>
  </header>
  <main class="p-4">
    <div class="border-round overflow-hidden">
      <DataTable :expandedRows="expandedRows" @row-expand="onRowExpand" @row-collapse="onRowCollapse" dataKey="filename" v-model:filters="filters" :globalFilterFields="['filename', 'category']" :value="files" tableStyle="min-width: 50rem" removableSort>
        <template #header>
          <section class="flex align-items-center justify-content-between">
            <div class="flex justify-end">
                <IconField>
                    <InputIcon>
                        <i class="pi pi-search" />
                    </InputIcon>
                    <InputText v-model="filters['global'].value" placeholder="Globale Suche" />
                </IconField>
            </div>
            <div>
              <div>
                  <Button label="Datei Hochladen" icon="pi pi-plus" @click="showPopup" />
                  <Dialog v-model:visible="visible" title="Datei hochladen" :modal="true" :closable="false">
                    <div class="flex gap-2 flex-column">
                      <div class="flex justify-content-start align-items-start flex-column gap-2">
                        <input @change="inputChange" type="file"/>
                        <!-- <FileUpload v-model="currentFile" mode="basic" accept="image/*" maxFileSize="1000000" @upload="addFile" /> -->
                        <InputText v-model="fileComment" placeholder="Kommentar" />
                      </div>
                      <div class="flex gap-2">
                        <Button class="flex-grow-1" label="Add" icon="pi pi-check" @click="addFile" />
                        <Button class="flex-grow-3" label="Cancel" icon="pi pi-times" @click="hidePopup" severity="danger"/>
                      </div>
                    </div>
                  </Dialog>
              </div>
          </div>
          </section>
        </template>
        <template #empty>Keine Dateien Gefunden</template>
        
        <Column expander style="width: 3em"/>
        
        <Column field="filename" header="Dateiname" sortable style="min-width: 12rem">
          <template #body="{ data }">
            {{ data.filename }}
          </template>
          <template #filter="{ filterModel, filterCallback}">
            <InputText v-model="filterModel.value" type="text" @input="filterCallback()" placeholder="Suche nach Dateinamen" />
          </template>
        </Column>
        <Column field="description" header="Beschreibung"></Column>
        <Column field="category" header="Kategorie" sortable></Column>
        <Column field="size_bytes" header="Größe" sortable></Column>
        <Column field="filetype" header="Dateityp" sortable></Column>
        <Column field="created_date" sortable header="Erstellt"></Column>

        <!-- <template #expandedRow="{ data }">
          <div class="p-3">
            <h5>Details for {{ data.filename }}</h5>
            <p><strong>Category:</strong> {{ data.category }}</p>
            <p><strong>Size:</strong> {{ data.size_bytes }} bytes</p>
            <p><strong>File Type:</strong> {{ data.filetype }}</p>
            <p><strong>Created Date:</strong> {{ data.created_date }}</p>
            <p><strong>Description:</strong> {{ data.description }}</p>
          </div>
        </template> -->
      </DataTable>
    </div>

  </main>
</template>

<style scoped>

</style>
^