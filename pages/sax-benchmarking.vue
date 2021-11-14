<template>
  <section class="w-6/12 mx-auto">
    <section class="header-section">
      <div class="header">
        <h1 class="text-center text-3xl py-8 text-gray-600">
          Sax Benchmarking Tool
        </h1>
      </div>
    </section>
    <section class="sax-form m-auto">
      <p class="text-center mb-5">
        Select the SAX co-efficients of choice. For alphabet sizes less than 20
        the SAX words will be calculated as strings. For alphabets greater than
        20 a bit format will be used.
      </p>
      <div class="form-wrapper w-8/12 m-auto">
        <input
          type="number"
          class="
            mt-1
            mb-5
            block
            w-full
            rounded-md
            border-gray-300
            shadow-sm
            focus:border-indigo-300
            focus:ring
            focus:ring-indigo-200
            focus:ring-opacity-50
          "
          name="word-length"
          placeholder="Select word length"
          v-model="word_length"
        />
        <input
          type="number"
          class="
            mt-5
            block
            w-full
            rounded-md
            border-gray-300
            shadow-sm
            focus:border-indigo-300
            focus:ring
            focus:ring-indigo-200
            focus:ring-opacity-50
          "
          name="alphabet-size"
          placeholder="Select alphabet size"
          v-model="alphabet_size"
        />
        <label class="inline-flex items-center mt-5">
          <input
            type="checkbox"
            class="
              rounded
              border-gray-300
              text-indigo-600
              shadow-sm
              focus:ring
              focus:ring-offset-0
              focus:ring-indigo-200
              focus:ring-opacity-0
            "
            checked=""
            v-model="change_dataset"
          />
          <span class="ml-2">Change Dataset</span>
        </label>
        <button
          class="
            bg-indigo-500
            hover:bg-indigo-700
            text-white
            font-bold
            py-2
            mx-auto
            my-5
            px-4
            rounded
            w-6/12
          "
        >
          Submit
        </button>
      </div>
    </section>
    <transition name="bounce">
      <section class="results" v-if="alphabet_size && word_length">
        <div
          id="sax-results-wrapper"
          class="sax-results-wrapper border-t-2 border-indigo-600 pt-10 mt-20"
        >
          <h2 class="text-center text-3xl text-gray-600">Results</h2>
          <div class="results_first_section grid grid-cols-2">
            <div class="first_section_results_left">
              <div class="coefficients-section mt-5">
                <p>Selected Word Length: {{ word_length }}</p>
                <p>Selected Alphabet Size: {{ alphabet_size }}</p>
              </div>
              <div class="timeseries-names mt-5">
                <p>Timeseries 1 name: Lorem ipsum dolor sit</p>
                <p>Timeseries 1 name: Lorem ipsum dolor sit</p>
              </div>
            </div>
            <div class="first_section_results_right">
              <div class="coefficients-section mt-5">
                <p>Original Eucledian Distance: 22</p>
                <p>SAX Distance: 10</p>
                <p>Tighness of Lower Bound: 0.0222</p>
              </div>
              <div class="timeseries-names mt-5">
                <p>Original Timeseries 1 Size: 223123 Bytes</p>
                <p>Original Timeseries 2 Size: 223123 Bytes</p>
                <p>SAX Size: 1231 Bytes</p>
                <p>Compression Ratio: 60%</p>
              </div>
            </div>
          </div>
          <div id="chart" class="mt-20">
            <apexchart
              type="line"
              height="350"
              :options="chartOptions"
              :series="series"
            ></apexchart>
          </div>
          <div id="chart2" class="mt-20">
            <apexchart
              type="line"
              height="350"
              :options="chartOptions"
              :series="series"
            ></apexchart>
          </div>
        </div>
      </section>
    </transition>
  </section>
</template>

<script>
import VueApexCharts from 'vue-apexcharts'

export default {
  data() {
    return {
      alphabet_size: 10,
      word_length: 10,
      change_dataset: false,
      series: [
        {
          name: 'Timeseries 1',
          data: [28, 29, 33, 36, 32, 32, 33],
        },
        {
          name: 'Timeseries 2',
          data: [12, 11, 14, 18, 17, 13, 13],
        },
      ],
      chartOptions: {
        chart: {
          height: 350,
          type: 'line',
          dropShadow: {
            enabled: true,
            color: '#000',
            top: 18,
            left: 7,
            blur: 10,
            opacity: 0.2,
          },
          toolbar: {
            show: false,
          },
        },
        colors: ['#77B6EA', '#545454'],
        dataLabels: {
          enabled: false,
        },
        stroke: {
          curve: 'smooth',
        },
        title: {
          text: 'Original SAX Graphs',
          align: 'left',
        },
        grid: {
          borderColor: '#e7e7e7',
          row: {
            colors: ['#f3f3f3', 'transparent'], // takes an array which will be repeated on columns
            opacity: 0.5,
          },
        },
        markers: {
          size: 1,
        },
        xaxis: {
          // categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul'],
          title: {
            text: 'Time',
          },
          min: 1,
          max: 7,
        },
        yaxis: {
          title: {
            text: 'Timeseries',
          },
          min: 5,
          max: 40,
        },
        legend: {
          position: 'top',
          horizontalAlign: 'right',
          floating: true,
          offsetY: -25,
          offsetX: -5,
        },
      },
    }
  },
  components: {
    apexchart: VueApexCharts,
  },
}
</script>

<style lang="scss" scoped>
.sax-form {
  button {
    display: block;
  }
}

.bounce-enter-active {
  animation: bounce-in 0.5s;
}
.bounce-leave-active {
  animation: bounce-in 0.5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}
</style>
