<script>
export default {
    props: ['onTagsChange'],
    data() {
        return {
            currentValue: '',
            tags: []
        }
    },
    methods: {
        handleKeyDown(e) {
            if (e.key === 'Backspace' && this.currentValue === '') {
                this.tags.pop()
                this.onTagsChange(this.tags)
            }
        },
        handleSubmit() {
            if (this.currentValue !== '') {
                const exist = this.tags.some(item => item === this.currentValue)
                if (!exist) {
                    this.tags.push(this.currentValue)
                    this.currentValue = ''
                    this.onTagsChange(this.tags)

                }
            }
        },
        deleteTag(tag) {
            this.tags = this.tags.filter(item => item !== tag)
            this.onTagsChange(this.tags)

        }
    }
}

</script>
<template>
    <div class="input-tag">
        <div class="tags">
            <div v-for="(tag, idx) in tags" :key="idx" class="tag">{{ tag }} <button @click="deleteTag(tag)">X</button>
            </div>
        </div>
        <form action="#" @submit.prevent="handleSubmit">
            <input type="text" v-model="currentValue" @keydown="handleKeyDown">
        </form>
    </div>
</template>
<style scoped>
.input-tag {
    display: inline-flex;
    border: 1px solid #ffff;
    border-radius: 5px;
    min-height: 50px;
}

.tags {
    display: flex;
    gap: 3px;
    padding: 5px;
}

.tags .tag {
    display: flex;
    padding: 5px;
    border: solid 1px #ccc;
    align-items: center;
    gap: 5px;
    border-radius: 5px;
}

.input-tag form {
    display: inline-flex;
}

.input-tag input {
    outline: none;
    border: none;
}
</style>