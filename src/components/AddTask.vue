<template>
    <form @submit="onSubmit" class="add-form">
        <div class="form-control">
            <label for=""><h1>Tarefa</h1></label>
            <input v-model="text" type="text" name="text" placeholder="Adicionar tarefa">
        </div>
        <div class="form-control">
            <label for=""><h1>Data / Horário</h1></label>
            <input v-model="day" type="text" name="day" placeholder="Adicionar horário">
        </div>
        <div class="form-control form-control-check">
            <label for=""><h1>Tarefa Urgente</h1></label>
            <input v-model="priority" type="checkbox" name="priority">
        </div>
        

        <input type="submit" value="Salvar Tarefa" class="btn btn-block">
        <div class="form-control">
            <label for=""><h2> {{ alert }} </h2></label>
        </div>
    </form>
</template>

<script>
    export default {
        name: 'AddTask',
        data() {
            return{
                text: '',
                day: '',
                priority: false,
                alert: ''
            }
        },
        methods:{
            onSubmit(e){
                e.preventDefault()

                if(!this.text) {
                    this.alert = 'Insira uma tarefa!'
                    return
                }

                const newTask = {
                    id: Math.floor(Math.random() * 100000),
                    text: this.text,
                    day: this.day,
                    priority: this.priority,
                }

                this.$emit('add-task', newTask)

                this.text = ''
                this.day = ''
                this.priority = false
                this.alert = ''
            
            }
        }
    }
</script>

<style scoped>
.add-form {
    margin-bottom: 40px;
    background-color: rgb(153, 128, 177);
    padding: 0 50px;
}
.form-control {
    margin: 20px 0;
}
.form-control label {
    display: flex;
}

h1 {
    margin: 0 auto;
    font-size: 18px;
    font-weight: 700;
    text-transform: uppercase;
    margin-top: 8px;
    margin-bottom: 5px;
    color: white;
}

h2 {
    color: rgb(255, 183, 89);
    margin: 0 auto;
    font-size: 16px;
    font-weight: 800;
    text-transform: uppercase;
    margin-bottom: 8px;
}

.form-control input {
    width: 100%;
    height: 34px;
    margin: 0px;
    padding: 3px 7px;
    font-size: 17px;
    text-align: center;
}

.form-control input::placeholder {
    text-align: center;
}

.form-control input::content{
    text-align: center;
}

.form-control-check input {
    height: 25px;
}
</style>