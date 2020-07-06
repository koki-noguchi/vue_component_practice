<template>
    <div>
        <p>
            <button @click="start">start</button>
        </p>
        <div v-if="answer > 0">
            <input
                type="number"
                v-model.number="num"
                @keyup.enter="guess"
            />
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            answer: 0,
            num: 0,
            tryCountLeft: 10
        }
    },
    methods: {
        start () {
            this.answer = Math.floor(Math.random() * (100 - 1) + 1)
            this.num = 0
            this.tryCountLeft = 10
            this.$emit('start', this.tryCountLeft)
        },
        guess () {
            this.tryCountLeft -= 1

            if (this.answer === this.num) {
                this.$emit('collect', this.tryCountLeft)
                return
            }

            if (this.tryCountLeft === 0) {
                this.$emit('lose', this.tryCountLeft)
            } else if (this.answer < this.num) {
                this.$emit('lower', this.tryCountLeft)
            } else {
                this.$emit('higher', this.tryCountLeft)
            }
        }
    }
}
</script>