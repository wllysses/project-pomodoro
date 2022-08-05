<template>
    <div class="main">
        <div class="container">
            <h1>{{ num }}</h1>
            <div class="buttons">
                <button @click="startPomodoroTimer">{{ btnStart }}</button>
                <button @click="clearPomodoroTimer">ZERAR</button>
            </div>
        </div>

        <div class="results" v-show="listPauses.length > 0">
            <ul>
                <li v-for="pause in listPauses" :key="pause">Você fez uma pausa em: {{ pause }}</li>
            </ul>
            <button @click="listPauses = []">ZERAR HISTÓRICO</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'myPomodoro',
    data() {
        return {
            num: '25:00',
            timer: null,
            btnStart: 'INICIAR',
            ss: 60,
            mm: 24,
            listPauses: []
        }
    },
    methods: {
        startPomodoroTimer() {
            if(this.timer !== null) {
                clearInterval(this.timer)
                this.timer = null
                this.btnStart = 'INICIAR'
                if(this.ss != 59) {
                    this.listPauses.push(this.num)
                }
            } else {
                this.btnStart = 'PAUSAR'
                this.timer = setInterval(() => {
                    this.runPomodoroTimer()
                }, 1000)
            }
        },
        clearPomodoroTimer() {
            if(this.timer !== null) {
                clearInterval(this.timer)
                this.timer = null
            }
            this.ss = 59
            this.mm = 24
            this.num = '25:00'
            this.btnStart = 'INICIAR'
            this.listPauses = []
        },
        runPomodoroTimer() {
            this.ss--

            if(this.ss == 0) {
                this.ss = 59
                this.mm--
            }

            if(this.mm == 0) {
                clearInterval(this.timer)
                this.timer = null
                this.btnStart = 'INICIAR'
                this.mm = 24
                this.ss = 59
                return this.numero = '25:00'
            }

            let formatPomodoroTimer =   `
                                            ${this.mm < 10 ? '0' + this.mm : this.mm} :
                                            ${this.ss < 10 ? '0' + this.ss : this.ss}
                                        `
            this.num = formatPomodoroTimer
            return this.num
        }
    }
}
</script>

<style scoped>

.main {
    width: 100%;
    height: 100%;
    margin: auto;
    
}
.container {
    margin: 50px auto 0;
    max-width: 400px;
    width: 100%;
    height: 400px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 5px solid white;
    border-radius: 50%;
    margin-bottom: 30px;
}

.container h1 {
    font-size: 100px;
    margin-bottom: 10px;
    color: white;
    font-weight: 300;
}

.container .buttons {
    display: flex;
}

.container .buttons button {
    width: 100px;
    padding: 10px;
    margin: 10px;
    color: white;
    font-weight: 700;
    background-color: #D8534E;
    border: 2px solid white;
    border-radius: 10px;
    cursor: pointer;
    transition: 0.2s;
}

.container .buttons button:hover {
    background-color: white;
    color: #D8534E;
}

.results {
    width: 300px;
    margin: auto;
}

.results ul {
    max-height: 200px;
    overflow: auto;
    list-style: none;
}

.results ul li {
    margin-bottom: 5px;
    background-color: white;
    padding: 10px;
    color: #D8534E;
    font-weight: 700;
}

.results button {
    margin-top: 10px;
    width: 100px;
    padding: 10px;
    color: white;
    font-weight: 700;
    background-color: #D8534E;
    border: 2px solid white;
    border-radius: 10px;
    cursor: pointer;
    transition: 0.2s;
}
</style>