<template>
  <div>
    <base-header
      class="header pb-8 pt-5 pt-lg-8 d-flex align-items-center"
      style="min-height: 600px; background-image: url(img/theme/profile-cover.jpg); background-size: cover; background-position: center top;"
    >
    <span class="mask bg-gradient-success opacity-4"></span>
      <div class="row">
        <div class="col-xl-3 col-lg-6">
          <stats-card
            title="TRÁFEGO TOTAL MÁQUINARIO"
            type="gradient-red"
            sub-title="350,897"
            icon="fa fa-truck"
            class="mb-4 mb-xl-0"
          >
            <template slot="footer">
              <span class="text-success mr-2">
                <i class="fa fa-arrow-up"></i> 73.48%
              </span>
              <span class="text-nowrap">Desde último Mês</span>
            </template>
          </stats-card>
        </div>
        <div class="col-xl-3 col-lg-6">
          <stats-card
            title="TRÁFEGO TOTAL MÁQUINARIO"
            type="gradient-orange"
            sub-title="2,356"
            icon="fa fa-truck"
            class="mb-4 mb-xl-0"
          >
            <template slot="footer">
              <span class="text-success mr-2">
                <i class="fa fa-arrow-up"></i> 12.18%
              </span>
              <span class="text-nowrap">Desde última Semana</span>
            </template>
          </stats-card>
        </div>
        <div class="col-xl-3 col-lg-6">
          <stats-card
            title="COMBUSTIVEL TOTAL GASTO"
            type="gradient-green"
            sub-title="924"
            icon="fa fa-tint"
            class="mb-4 mb-xl-0"
          >
            <template slot="footer">
              <span class="text-danger mr-2">
                <i class="fa fa-arrow-down"></i> 55.72%
              </span>
              <span class="text-nowrap">Desde último Més</span>
            </template>
          </stats-card>
        </div>
        <div class="col-xl-3 col-lg-6">
          <stats-card
            title="DESEMPENHO MÁQUINARIO"
            type="gradient-info"
            sub-title="49,65%"
            icon="fa fa-truck"
            class="mb-4 mb-xl-0"
          >
            <template slot="footer">
              <span class="text-success mr-2">
                <i class="fa fa-arrow-up"></i> 54.8%
              </span>
              <span class="text-nowrap">Desde último Més</span>
            </template>
          </stats-card>
        </div>
      </div>
    </base-header>

    <!--Charts-->
    <div class="container-fluid mt--7">
      <div class="row">
        <div class="col-xl-8 mb-5 mb-xl-0">
          <card type="default" header-classes="bg-transparent">
            <div slot="header" class="row align-items-center">
              <div class="col">
                <h6 class="text-light text-uppercase ls-1 mb-1">Visão geral</h6>
                <h5 class="h3 text-white mb-0">Consumo Máquinario</h5>
              </div>
              <div class="col">
                <ul class="nav nav-pills justify-content-end">
                  <li class="nav-item mr-2 mr-md-0">
                    <a
                      class="nav-link py-2 px-3"
                      href="#"
                      :class="{active: bigLineChart.activeIndex === 0}"
                      @click.prevent="initBigChart(0)"
                    >
                      <span class="d-none d-md-block">Mês</span>
                      <span class="d-md-none">M</span>
                    </a>
                  </li>
                  <li class="nav-item">
                    <a
                      class="nav-link py-2 px-3"
                      href="#"
                      :class="{active: bigLineChart.activeIndex === 1}"
                      @click.prevent="initBigChart(1)"
                    >
                      <span class="d-none d-md-block">Semana</span>
                      <span class="d-md-none">W</span>
                    </a>
                  </li>
                </ul>
              </div>
            </div>
            <line-chart
              :height="350"
              ref="bigChart"
              :chart-data="bigLineChart.chartData"
              :extra-options="bigLineChart.extraOptions"
            ></line-chart>
          </card>
        </div>

        <div class="col-xl-4">
          <card header-classes="bg-transparent">
            <div slot="header" class="row align-items-center">
              <div class="col">
                <h6 class="text-uppercase text-muted ls-1 mb-1">Atuação</h6>
                <h5 class="h3 mb-0">Solitação do Máquinario</h5>
              </div>
            </div>

            <bar-chart :height="350" ref="barChart" :chart-data="redBarChart.chartData"></bar-chart>
          </card>
        </div>
      </div>
      <!-- End charts-->

      <!--Tables-->
      <div class="row mt-5">
        <div class="col-xl-8 mb-5 mb-xl-0">
          <page-visits-table></page-visits-table>
        </div>
        <div class="col-xl-4">
          <social-traffic-table></social-traffic-table>
        </div>
      </div>
      <!--End tables-->
    </div>
    <br/><br/><br/><br/><br/><br/>
  </div>
</template>
<script>
// Charts
import * as chartConfigs from "@/components/Charts/config";
import LineChart from "@/components/Charts/LineChart";
import BarChart from "@/components/Charts/BarChart";

// Tables
import SocialTrafficTable from "./Dashboard/SocialTrafficTable";
import PageVisitsTable from "./Dashboard/PageVisitsTable";

export default {
  components: {
    LineChart,
    BarChart,
    PageVisitsTable,
    SocialTrafficTable
  },
  data() {
    return {
      bigLineChart: {
        allData: [
          [0, 20, 10, 30, 15, 40, 20, 60, 60],
          [0, 20, 5, 25, 10, 30, 15, 40, 40]
        ],
        activeIndex: 0,
        chartData: {
          datasets: [],
          labels: []
        },
        extraOptions: chartConfigs.blueChartOptions
      },
      redBarChart: {
        chartData: {
          labels: ["Jul", "Aug", "Set", "Out", "Nov", "Dez"],
          datasets: [
            {
              label: "Sales",
              data: [25, 20, 30, 22, 17, 29]
            }
          ]
        }
      }
    };
  },
  methods: {
    initBigChart(index) {
      let chartData = {
        datasets: [
          {
            label: "Performance",
            data: this.bigLineChart.allData[index]
          }
        ],
        labels: ["Mai", "Jun", "Jul", "Aug", "Sey", "Out", "Nov", "Dez"]
      };
      this.bigLineChart.chartData = chartData;
      this.bigLineChart.activeIndex = index;
    }
  },
  mounted() {
    this.initBigChart(0);
  }
};
</script>
<style></style>
