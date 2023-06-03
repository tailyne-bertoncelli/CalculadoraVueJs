<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <div class="d-flex justify-content-center">
            <table class="table table-bordered  w-75 mt-3">
                <thead class="table-dark">
                    <tr class="text-center">
                        <td colspan="4">{{ output || 0 }}</td>
                    </tr>
                </thead>
                <tbody>
                    <tr class="table-active">
                        <td v-on:click="cleanField">C</td>
                        <td v-on:click="setNegativeOrPositive">+ / -</td>
                        <td v-on:click="calculatePercentage">%</td>
                        <td v-on:click="processOutput('divide')" class="right-column">/</td>
                    </tr>
                    <tr>
                        <td v-on:click="getNumber('7')">7</td>
                        <td v-on:click="getNumber('8')">8</td>
                        <td v-on:click="getNumber('9')">9</td>
                        <td v-on:click="processOutput('multiply')" class="right-column table-active">X</td>
                    </tr>
                    <tr>
                        <td v-on:click="getNumber('4')">4</td>
                        <td v-on:click="getNumber('5')">5</td>
                        <td v-on:click="getNumber('6')">6</td>
                        <td v-on:click="processOutput('substract')" class="table-active">-</td>
                    </tr>
                    <tr>
                        <td v-on:click="getNumber('1')">1</td>
                        <td v-on:click="getNumber('2')">2</td>
                        <td v-on:click="getNumber('3')">3</td>
                        <td v-on:click="processOutput('add')" class="table-active">+</td>
                    </tr>
                    <tr>
                        <td v-on:click="getNumber('0')" colspan="2">0</td>
                        <td v-on:click="getDot()">.</td>
                        <td v-on:click="updateOutput" class="right-column">=</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>


export default {
    name: 'CalculadoraComponente',
    props: {
        msg: String
    },
    data() {
        return {
            output: ''
        }
    },
    methods: {
        cleanField() {
            this.output = 0
        },
        setNegativeOrPositive(){
            this.output = this.output[0] === '-'? this.output.slice(1): `-${this.output}`;
        },
        calculatePercentage(){
            this.output = parseFloat(this.output)/100;
        },
        getNumber(number){
            if(this.operationFired){
                this.output = '';
                this.operationFired = false;
            }
            this.output=`${this.output}${number}`;
        },
        getDot(){
            if(this.output.indexOf('.') === -1){
                this.output = this.output+'.';
            }
        },
        processOutput(operation){

            if(operation === 'add'){
                this.operation=(a,b)=>{
                    return parseFloat(a)+parseFloat(b);
                }
            }else if(operation === 'substract'){
                this.operation=(a,b)=>{
                    return parseFloat(a)-parseFloat(b);
                }
            } else if(operation === 'multiply'){
                this.operation=(a,b)=>{
                    return parseFloat(a)*parseFloat(b);
                }
            } else if(operation === 'divide'){
                this.operation=(a,b)=>{
                    return parseFloat(a)/parseFloat(b);
                }
            }
            this.previousValue = this.output;
            this.operationFired = true;
        },
        updateOutput(){
            this.output = `${this.operation(this.previousValue, this.output)}`;
            this.previousValue = null;
        }

    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
    margin: 40px 0 0;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}

td{
    cursor: pointer;
}

</style>
