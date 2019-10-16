<template>
  <resource-layout>
    <div slot="left">
      <slot name="info-card">
        <info-card :resource="resource" :loading="loading" />
      </slot>
    </div>
    <div slot="right">
      <a-card
        :bordered="true"
        style="width:100%">
        <a-skeleton active v-if="loading" />
        <a-tabs
          v-else
          :defaultActiveKey="tabs[0].name"
          style="width: 100%"
          @change="onTabChange" >
          <a-tab-pane
            v-for="tab in tabs"
            :tab="$t(tab.name)"
            :key="tab.name">
            <component :is="tab.component" :resource="resource" :loading="loading" />
          </a-tab-pane>
        </a-tabs>
      </a-card>
    </div>
  </resource-layout>
</template>

<script>

import DetailsTab from '@/components/view/DetailsTab'
import InfoCard from '@/components/view/InfoCard'
import ResourceLayout from '@/layouts/ResourceLayout'

export default {
  name: 'ResourceView',
  components: {
    InfoCard,
    ResourceLayout
  },
  props: {
    resource: {
      type: Object,
      required: true
    },
    loading: {
      type: Boolean,
      default: false
    },
    tabs: {
      type: Array,
      default: function () {
        return [{
          name: 'details',
          component: DetailsTab
        }]
      }
    }
  },
  methods: {
    onTabChange (key) {
      this.activeTab = key
    }
  }
}
</script>

<style lang="less" scoped>
</style>