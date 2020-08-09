<template>
    <div class='file'>
        <b-container class="bv-example-row">
        <b-card class="text-center">
            <h3>HEALTH DECLARATION / הצהרת בריאות</h3>

        <br>   
            <b-form-input class="inputForm" v-model="person.name" placeholder="Enter your name / הכנס שם"></b-form-input>

        <br>


        <table>
            <tr>
                <td>
                 אני מצהיר שחום גוף  מתחת ל38 מעלות צלזיוס
                <br>
                I declare that my body temperature is below 38 degrees Celsius
                </td>

                <td>
                    <b-form-checkbox 
                    v-model="person.temperature">
                    </b-form-checkbox>
                </td>
            </tr>

            <br>

            <tr>
                <td>
                 אני מצהיר על העדר שיעול
                <br>
                I declare no cough
                </td>

                <td>
                    <b-form-checkbox class="inline"
                    v-model="person.cough">
                    </b-form-checkbox>
                </td>
            </tr>

            <br>

            <tr>
                <td>
                 אני מצהיר על העדר קושי בנשימה
                <br>
                I declare the absence of difficulty in breathing
                </td>

                <td>
                    <b-form-checkbox
                    v-model="person.breathing">
                    </b-form-checkbox>
                </td>
            </tr>


        </table>


            <br>

            <b-button variant="primary" @click="submit">Submit</b-button>

        </b-card>
        </b-container>
    </div>  
</template>


<script>
 import axios from 'axios'
export default {
    data(){
        return{
            person:{
                name:'',
                temperature:false,
                cough:false,
                breathing:false,
                date: ''
            }

        }
    },
    methods:{
        submit(){

            this.person.date = new Date();
            var datestring = this.person.date.getDate()  + "-" + (this.person.date.getMonth()+1) + "-" + this.person.date.getFullYear() + " " +
            this.person.date.getHours() + ":" + this.person.date.getMinutes();
            this.person.date = datestring

            axios.post('https://healthdeclaration-6e331.firebaseio.com/users.json',this.person)
            .then(res => {console.log(res);
                    alert('Thank you!')} )
            .catch(error => console.log(error))
            }
        }
    }
</script>

<style scoped>

td{
    margin-left:10px;
    text-align: center;
    vertical-align: middle;
}

table{
    margin-left:auto;
    margin-right:auto;
}

.file{
    margin-top:10px;
}

.inputForm{
    margin-left:auto;
    margin-right:auto;
    width:350px;
}


</style>