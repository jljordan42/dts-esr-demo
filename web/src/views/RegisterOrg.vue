<template>
  <v-container class="mb-4">
    <v-row>
      <v-col>
        <h2 class="my-4 display-1">
          Add Organization
        </h2>
        <v-btn to="/manage" text
          ><v-icon>mdi-chevron-left</v-icon> Back to organizations</v-btn
        >
        <v-skeleton-loader
          boilerplate
          type="paragraph"
          class="mt-2"
        ></v-skeleton-loader>
        <br />

        <v-toolbar dense flat class="mb-3">
          <v-toolbar-title>Find your Organization</v-toolbar-title>
        </v-toolbar>
        <v-alert text border="left" color="secondary darken-1" icon="mdi-flag">
          This search mechanism will use an OrgBook API to support owners/directors in finding the legal name of their organization.
          Fully implemented, this section will integrate with BC Registries to verify a connection between the user and their
          essential service organization.
        </v-alert>
        <v-card outlined class="mb-4 pa-3">
          <v-autocomplete
            label="Orgbook Search"
            placeholder="Start typing to Search"
            prepend-icon="mdi-office-building"
            return-object
            outlined
            hide-details
          ></v-autocomplete>
        </v-card>

        <v-toolbar dense flat class="mb-3">
          <v-toolbar-title>Services Offered</v-toolbar-title>
        </v-toolbar>

        <v-card outlined>
          <v-card-text class="py-1">
            <v-row align="center" justify="start">
              <v-col v-if="!services.length">
                <v-alert
                  color="primary"
                  class="mb-0"
                  text
                  icon="mdi-information"
                  >No services added</v-alert
                >
              </v-col>
              <v-col
                v-for="(service, i) in services"
                :key="service.id"
                class="shrink"
              >
                <v-chip close @click:close="services.splice(i, 1)">
                  <v-icon left v-text="service.icon"></v-icon>
                  {{ service.name }}
                </v-chip>
              </v-col>
            </v-row>
          </v-card-text>
          <v-divider v-if="!allSelected"></v-divider>
          <v-list v-if="!allSelected">
            <template v-for="(item, i) in serviceOptions">
              <v-list-item
                v-if="!services.includes(item)"
                :key="i"
                @click="services.push(item)"
              >
                <v-list-item-avatar>
                  <v-icon v-text="item.icon"></v-icon>
                </v-list-item-avatar>
                <v-list-item-title v-text="item.name"></v-list-item-title>
                <v-list-item-action
                  ><v-icon>mdi-plus</v-icon></v-list-item-action
                >
              </v-list-item>
            </template>
          </v-list>
        </v-card>

        <div style="text-align: right" class="mt-4">
          <v-btn to="/update" color="primary">Save and Continue</v-btn>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped lang="scss"></style>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { Service } from "@/models/organization";

@Component({})
export default class RegisterOrg extends Vue {
  private serviceOptions: Service[] = [
    {
      id: "1",
      name: "Medical Facility Services",
      icon: "mdi-medical-bag"
    },
    {
      id: "2",
      name: "Doctor",
      icon: "mdi-doctor"
    },
    {
      id: "3",
      name: "Nurse",
      icon: "mdi-doctor"
    },
    {
      id: "4",
      name: "Cleaning",
      icon: "mdi-broom"
    },
    {
      id: "5",
      name: "Sanitation",
      icon: "mdi-trash-can-outline"
    },
    {
      id: "6",
      name: "HVAC Repair",
      icon: "mdi-water-boiler"
    },
    {
      id: "7",
      name: "IT",
      icon: "mdi-laptop"
    }
  ];
  private services: Service[] = [];

  private serviceIds() {
    const ids = [];
    for (const svc of this.services) {
      ids.push(svc.id);
    }
    return ids;
  }

  private allSelected = false;

  created() {
    //
  }
}
</script>
