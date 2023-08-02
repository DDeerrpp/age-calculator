<script>
export default {
    name: 'Calculations',
    data() {
        return {
            years: '- -',
            months: '- -',
            days: '- -',
        }
    },
    methods: {
        calculateAge(d, m, y) {
            var date = new Date();
            var birth = new Date(`${y}-${m}-${d}`);
            var year = date.getFullYear() - birth.getFullYear();
            var month = date.getMonth() - birth.getMonth();
            var day = date.getDate() - birth.getDate();
            if (month < 0 || (month === 0 && date.getDate() < birth.getDate())) {
                year--;
            }
            this.years = `${Math.abs(year)}`;
            this.months = `${Math.abs(month)}`;
            this.days = `${Math.abs(day)}`;

        }
    }
}
</script>

<template>
    <main class="dates">
        <p class="years"><span>{{ years }}</span> years</p>
        <p class="months"><span>{{ months }}</span> months</p>
        <p class="days"><span>{{ days }}</span> days</p>
    </main>
    
</template>



<style scoped>
@import '../style.css';
.dates {
    height: 100px;
    display: flex;
    flex-direction: column;
    transform: translateY(-25px);
}
span {
    color: var(--purple);
}
p {
    font-size: 85px;
    font-weight: 800 !important;
    font-style: italic;
}

@media only screen and (max-width: 500px) {
    .dates {
        transform: translate(10px, 20px);
    }
    p {
        font-size: 40px;
    }
}
</style>