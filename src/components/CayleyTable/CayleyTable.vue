<template>
    <table class="cayley-table">
        <caption>Таблица Кэли для &lt;<b>&#x2124;</b><sup v-if="coprime">*</sup><sub>{{m}}</sub>, {{operator}}&gt;</caption>
        <thead>
        <tr>
            <th>{{operator}}</th>
            <th :key="col" v-for="col in cols">{{col}}</th>
        </tr>
        </thead>
        <tbody>
        <tr :key="row" v-for="row in cols">
            <td>{{row}}</td>
            <td :key="col" v-for="col in cols">{{calculate(row, col)}}</td>
        </tr>
        </tbody>
    </table>
</template>

<script>
    function* range(length, from = 0) {
        for (let i = from; i < length + from; i++) {
            yield i;
        }
    }

    export default {
        name: "CayleyTable",
        props: {
            m: {
                type: Number,
                required: true
            },
            operator: {
                type: String,
                required: true
            },
            coprime: {
                type: Boolean,
            }
        },
        data: function () {
            return {decoratedName: `"${this.name}"`};
        },
        methods: {
            calculate(i, j) {
                if (this.operator === '+') {
                    return `${(i + j) % this.m}`;
                } else if (this.operator === '*') {
                    return `${(i * j) % this.m}`;
                }
            }
        },
        computed: {
            cols() {
                const cols = [...range(this.m)];
                if (this.coprime) {
                    return cols.filter((n) => {
                        const d = this.m / 2 | 0;
                        for (let i = 2; i <= d; i++) {
                            if (this.m % i === 0 && n % i === 0) {
                                return false
                            }
                        }
                        return true;
                    })
                } else {
                    return cols;
                }
            }
        }
    }
</script>

<style scoped lang="sass">
    .cayley-table
        color: #191919
        border: 1px solid currentColor
        border-collapse: collapse
        font-family: monospace
        font-size: 24px

        tr, td, th
            width: 37px
            height: 37px
            font-weight: normal
            border: 1px solid currentColor
            padding: 4px

        th:not(:first-child), td
            position: relative

            &:before
                content: ''
                position: absolute
                top: 6px
                left: 25%
                height: 1px
                width: 50%
                background-color: currentColor
</style>
