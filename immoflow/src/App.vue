<script setup lang="ts">
  import { ref } from 'vue';
  import Avatar from 'primevue/avatar';
  import Button from 'primevue/button';
  import OverlayBadge from 'primevue/overlaybadge';
  import DataTable from 'primevue/datatable';
  import Column from 'primevue/column';
  import ColumnGroup from 'primevue/columngroup';   // optional
  import Row from 'primevue/row';                   // optional


  const files = ref([
    { code: 'P001', name: 'Product 1', category: 'Category 1', quantity: 10 },
    { code: 'P002', name: 'Product 2', category: 'Category 2', quantity: 20 },
    { code: 'P003', name: 'Product 3', category: 'Category 3', quantity: 30 },
    { code: 'P004', name: 'Product 4', category: 'Category 4', quantity: 40 },
  ])

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
      <DataTable :value="files" tableStyle="min-width: 50rem">
        <Column field="code" header="Code"></Column>
        <Column field="name" header="Name"></Column>
        <Column field="category" header="Category"></Column>
        <Column field="quantity" header="Quantity"></Column>
      </DataTable>
    </div>

  </main>
</template>

<style scoped>

</style>
^