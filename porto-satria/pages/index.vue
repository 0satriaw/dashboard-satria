<template>
    <div class="grid gap-4 w-full">
        <header class="flex items-start justify-between">
            <div class="grow">
                <p>Hi, Welcome Back Satria</p>
                <h1>Dashoard</h1>
            </div>
            <div class=" w-[120px] bg-neutral-400 h-[32px]"></div>
        </header>
        <main class="grid gap-4">

            <Tabs default-value="Today" @click="setCategory">
                <TabsList class="max-w-[400px]">
                    <TabsTrigger v-for="item, index in tabs" :key="index" :value="item.title">
                        {{ item.title }}
                    </TabsTrigger>
                </TabsList>
                <TabsContent v-for="item, index in tabs" :key="index" :value="item.title">
                    <highchart :options="options" />
                </TabsContent>
            </Tabs>
            <!-- <div class="flex items-center gap-3">
                <div v-for='(item, index) in 3' :key='index' class="w-[120px] h-[36px] 
                bg-neutral-400">

                </div>
            </div>
            <section>
                <div class="w-full h-[300px] bg-neutral-400">

                </div>
            </section> -->
        </main>
        <footer>
            <div class="flex gap-4 items-start justify-between">
                <div v-for='(item, index) in 3' :key='index' class=" w-full h-[200px] bg-neutral-400">

                </div>
            </div>

        </footer>
    </div>
</template>
<script setup>
const loading = ref(false)
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs'


const tabs = [
    {
        title: 'Today',
        content: resolveComponent('Today')
    },
    {
        title: 'Week',
        content: 'Week'
    },
    {
        title: 'Month',
        content: 'Month'
    },
    {
        title: 'Year',
        content: 'Year'
    }
];

let data = ref([
    7.0, 6.9, 9.5, 14.5, 18.2, 21.5,
    25.2, 26.5, 23.3, 18.3, 13.9, 9.6
]);
let categories = ref({
    'today': [
        '0:00', '1:00', '2:00', '3:00', '4:00', '5:00', '6:00', '7:00', '8:00', '9:00', '10:00', '11:00',
        '12:00', '13:00', '14:00', '15:00', '16:00', '17:00', '18:00', '19:00', '20:00', '21:00', '22:00', '23:00'
    ],
    'week': [
        'Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'
    ],
    'month': [],
    'year': [
        'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'
    ]
});

let currentCategories = ref('today');
const options = computed(() => (
    {
        chart: {
            type: 'line',
            animation: {
                enabled: false
            }
        },
        title: {
            text: 'Monthly Average Temperature'
        },
        xAxis: {
            gridLineColor: 'transparent',
            categories: categories.value[currentCategories.value],

        },
        yAxis: {
            gridLineColor: 'transparent',
            title: {
                text: ''
            },
        },
        tooltip: {
            crosshairs: true,
            shared: true
        },
        plotOptions: {
            line: {
                dataLabels: {
                    enabled: false
                },
                marker: {
                    enabled: false,
                },
                enableMouseTracking: true
            }
        },
        series: [{
            name: 'Line',
            lineWidth: '2px',
            marker: {
                symbol: 'square'
            },
            color: {
                linearGradient: { x1: 0, x2: 0, y1: 0, y2: 1 },
                stops: [
                    [0, 'rgb(255, 0, 0)'],
                    [1, 'rgb(0, 0, 255)']
                ]
            },
            data: data.value
        }]
    }
))

function generateRandomData(number) {
    let values = []
    for (let i = 0; i < number; i++) {
        values.push(Math.floor(Math.random() * 100))
    }
    data.value = values;

    return values;

}

const setCategory = (e) => {
    let v = e.target.innerText.toLowerCase();

    currentCategories.value = v;

    switch (v) {
        case 'today':
            generateRandomData(24);
            break;
        case 'week':
            generateRandomData(7);
            break;
        case 'month':
            generateRandomData(31);
            break;
        case 'year':
            generateRandomData(12);
            break;
        default:
            generateRandomData(24);
            break;
    }

}


function generateMonthDates() {
    const dates = [];
    const now = new Date();
    const year = now.getFullYear();
    const month = now.getMonth();
    const daysInMonth = new Date(year, month + 1, 0).getDate();

    for (let i = 1; i <= daysInMonth; i++) {
        dates.push(`${month + 1}/${i}`);
    }

    categories.value.month = dates;
}

onMounted(() => {
    generateRandomData(24);
    generateMonthDates();
})

</script>
<style></style>