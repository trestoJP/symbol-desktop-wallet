<template>
    <div class="dashboard-container">
        <div class="dashboard-left-container">
            <div class="dashboard-top-left-container">
                <HarvestStatisticsPanel />
            </div>
            <div class="dashboard-bottom-left-container">
                <div class="header-container">
                    <NavigationTabs direction="horizontal" :parent-route-name="'harvesting'" />
                </div>
                <div class="harvesting-container">
                    <router-view />
                </div>
            </div>
        </div>
        <div class="dashboard-right-container">
            <!--TODO: Harvesting dashboard following standard style.-->
            <div class="header-container-placeholder">
                <h1 class="section-title">
                    {{ $t('harvested_blocks') }}
                </h1>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
// external dependencies
import { Component, Vue } from 'vue-property-decorator';

// child components
import NavigationTabs from '@/components/NavigationTabs/NavigationTabs.vue';
import HarvestStatisticsPanel from '@/components/HarvestStatisticsPanel/HarvestStatisticsPanel.vue';

@Component({
    components: { NavigationTabs, HarvestStatisticsPanel },
    data() {
        return {};
    },
})
export default class HarvestingDashboardPage extends Vue {}
</script>
<style lang="less" scoped>
@import './HarvestingDashboardPage.less';

.header-container-placeholder {
    padding: 0 0.4rem;
    margin: 0.2rem 0;
    .section-title {
        font-weight: 600;
        color: @purpleDark;
        font-family: @symbolFont;
    }
}
</style>
