<template>
  <div class="mt-3">
    <loading :active.sync="isLoading"></loading>
    <invoices-filter :invoices-filter="invoicesList.listConfig.filters"
                     :available-invoices-statuses="availableInvoicesStatuses"
                     @filtersChanged="filtersChanged"></invoices-filter>
    <div v-if="!isLoading" class="mt-3">
      <p>{{ $t("account.invoices.grid.text-above") }}</p>
      <b-table
        id="invoices-table"
        stacked="md"
        striped
        hover
        tbody-tr-class="text-break"
        :show-empty="true"
        :empty-text="$t('account.invoices.no-invoices')"
        :items="invoicesList.invoices"
        :fields="invoicesList.listConfig.columns"
        no-local-sorting
        @sort-changed="sortChanged">
        <template v-slot:cell(createdDate)="data">
          <span>{{ data.value | moment("LL") }}</span>
        </template>
        <template v-slot:cell(actions)="row">
          <font-awesome-layers v-b-tooltip.hover
                               :title="$t('account.invoices.download-invoice')"
                               class="btn"
                               @click="getInvoicePdf(row.item.orderId)">
            <font-awesome-icon :icon="downloadIcon" size="lg"></font-awesome-icon>
          </font-awesome-layers>
        </template>
      </b-table>

      <div class="d-flex justify-content-between">
        <b-pagination
          :value="invoicesList.listConfig.pageNumber"
          aria-controls="invoices-table"
          :total-rows="invoicesList.totalCount"
          :per-page="invoicesList.listConfig.pageSize"
          @change="pageChanged($event)"></b-pagination>
        <div>
          <select
            :value="invoicesList.listConfig.pageSize"
            class="form-control"
            @change="pageSizeChanged($event.target.value)">
            <option v-for="pageSize in pageSizes"
                    :key="pageSize"
                    :value="pageSize">
              {{ pageSize }}
            </option>
          </select>
        </div>
      </div>
      <p>{{ $t("account.invoices.grid.text-below") }}</p>
    </div>
  </div>
</template>

<script lang="ts" src="./account-invoices.ts"></script>
