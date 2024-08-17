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


  const filters = ref({
    global: { value: null, matchMode: 'contains' },
    filename: { value: null, matchMode: 'contains' },
  });

  const files = ref(listOfFiles)


  const visible = ref(false);
  const fileName = ref('');

  const showPopup = () => {
      visible.value = true;
  };

  const hidePopup = () => {
      visible.value = false;
  };

  const addFile = () => {
      console.log('Adding file:', fileName.value);
      hidePopup();
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
      <DataTable v-model:filters="filters" :globalFilterFields="['filename', 'category']" :value="files" tableStyle="min-width: 50rem" removableSort>
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
                    <Dialog v-model="visible" title="Datei hochladen" :modal="true" :closable="false">
                      <InputText v-model="fileName" placeholder="Enter file name" />
                      <Button label="Add" icon="pi pi-check" @click="addFile" />
                      <Button label="Cancel" icon="pi pi-times" @click="hidePopup" />
                    </Dialog>
                </div>

          </div>
          </section>
        </template>
        <template #empty>Keine Dateien Gefunden</template>
        <Column field="filename" header="Dateiname" sortable style="min-width: 12rem">
          <template #body="{ data }">
            {{ data.filename }}
          </template>
          <template #filter="{ filterModel, filterCallback}">
            <InputText v-model="filterModel.value" type="text" @input="filterCallback()" placeholder="Suche nach Dateinamen" />
          </template>
        </Column>
        <Column field="category" header="Kategorie" sortable></Column>
        <Column field="size_bytes" header="Größe" sortable></Column>
        <Column field="filetype" header="Dateityp" sortable></Column>
        <Column field="created_date" sortable header="Erstellt"></Column>
      </DataTable>
    </div>

  </main>
</template>

<style scoped>

</style>
^