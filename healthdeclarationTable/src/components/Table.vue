<template>
    <div class="table">
        <b-table-simple>
            <tr>
                <th>Name / שם</th>
                <th>Temperature / חום</th>
                <th>Cough / שיעול</th>
                <th>Breathing / נשימה</th>
                <th>Date / תאריך</th>
            </tr>
            <tr v-for="(item,index) in pepole" :key="item" v-bind:index="index">
                <td>{{item.name}}</td>
                <td>{{item.temperature}}</td>
                <td>{{item.cough}}</td>
                <td>{{item.breathing}}</td>
                <td>{{item.date}}</td>
            </tr>
        </b-table-simple>
    </div>
</template>

<script>
import axios from 'axios'
export default {
        data(){
    return{
        pepole:[]
    }
    },
    created(){
        axios.get('https://healthdeclaration-6e331.firebaseio.com/users.json')
        .then(res =>{
            //console.log(res.data);
            let info = res.data;
            console.log(info);
            this.pepole = Object.keys(info).map(key => {
            return info[key];
            });
            console.log(this.pepole);

            })
        .catch(error => console.log(error))
    }
    
}
</script>


<style scoped>
th, td{
    border: 1px solid grey;
    text-align: center;
}

.table{
    margin-top: 20px;
}

</style>