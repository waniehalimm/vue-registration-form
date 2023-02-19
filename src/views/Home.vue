<template>
	<div class="bg">
        <div class="container-fluid">
            <div class="row vh-100 justify-content-center align-items-center">
                <form class="registration-form" @submit.prevent="submitForm">
                    <div class="text-center">
                        <img class="company-logo mb-4" src="../assets/logo.png">
                    </div>
                    <!-- <h3>registration form</h3> -->
                    <div class="form-group">
                        <!-- <label for="exampleInputEmail1">Email address</label> -->
                        <input required type="text" id="name" class="form-control" placeholder="Full Name" v-model="form.name" >
                        <!-- <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small> -->
                    </div>
                    <div class="form-group col-12 row">
                        <div class="form-check col-6">
                            <input class="form-check-input" type="radio" name="flexRadioDefault" id="male" value="male" v-model="form.gender">
                            <label class="form-check-label" for="flexRadioDefault1">Male</label>
                        </div>
                        <div class="form-check col-6">
                            <input class="form-check-input" type="radio" name="flexRadioDefault" id="female" value="female" v-model="form.gender">
                            <label class="form-check-label" for="flexRadioDefault2">Female</label>
                        </div>
                    </div>
                    <div class="form-group">
                        <!-- <label for="exampleInputEmail1">Email address</label> -->
                        <input required type="email" id="email" class="form-control" aria-describedby="emailHelp" placeholder="Email" v-model="form.email" >
                        <!-- <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small> -->
                    </div>
                    <div class="form-group">
                        <!-- <label for="exampleInputPassword1">Password</label> -->
                        <input required type="number" id="phone" class="form-control" placeholder="Phone Number" v-model="form.phone">
                    </div>
                    <div class="form-group">
                        <date-picker v-model="form.birthdate" placeholder="Birth Date" format="DD MMM YYYY" valueType="YYYY-MM-DD" ></date-picker>
                    </div>
                    <div class="form-group mb-1">
                        <!-- <label for="exampleInputPassword1">Password</label> -->
                        <textarea required type="text" id="address" class="form-control" placeholder="Address" rows="3" v-model="form.address"> </textarea>
                    </div>
                    <div class="form-check">
                        <input class="form-check-input" type="checkbox" v-model="form.news">
                        <small class="form-check-label bold-l" for="flexCheckDefault">
                            Sign Up for Newsletter
                        </small>
                    </div>
                    <button type="submit" class="bold-l mt-4 btn btn-primary submit" >Create User Account</button>
                </form>
            </div>
        </div>
	</div>
</template>

<script>
import DatePicker from 'vue2-datepicker';
import 'vue2-datepicker/index.css';

export default {
	name: "HelloWorld",
    components: { DatePicker },
	props: {
	},
    head() {
        return {

        }
    },
    data() {
        return {
            form: {
                name: "",
                email: "",
                phone: "",
                address: "",
                news: 0,
                birthdate: "",
                gender: "male",
            }
        }
    },
    methods: {

    },
    computed: {
        
    },
    mounted() {

    }
};
</script>

<style scoped lang="scss">

.bg {
    background-image: url(../assets/bg-image.jpg);
	background-size: cover;
	background-position: center;
	background-repeat: no-repeat;
}

.registration-form {
    background-color: #FFF;
    border-radius: 1rem;
    padding: 1rem;
    width: 400px;

    .company-logo {
        height: 100px;
        align-self: center;

    }

    .form-control {
        background-color: #96d3ec;
        color: #FFF;
        border-radius: 1rem;
        &::placeholder {
            color: #FFF;
        }
        &:valid {
            background-color:  #6597d2!important;
        }
    }
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}
input[type=number] {
    -moz-appearance: textfield;
}

.btn {
    &.submit {
        width: 100%;
        border-radius: 1rem;
    }
}





// h3 {
// 	margin: 40px 0 0;
// }
// ul {
// 	list-style-type: none;
// 	padding: 0;
// }
// li {
// 	display: inline-block;
// 	margin: 0 10px;
// }
// a {
// 	color: #42b983;
// }
</style>
