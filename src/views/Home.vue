<template>
	<div class="bg">
        <span class="home-icon" >
            <svg v-if="isTableShow" @click="isTableShow = false" xmlns="http://www.w3.org/2000/svg" width="25" height="25" fill="#FFF" class="bi bi-house-door-fill" viewBox="0 0 16 16">
                <path d="M6.5 14.5v-3.505c0-.245.25-.495.5-.495h2c.25 0 .5.25.5.5v3.5a.5.5 0 0 0 .5.5h4a.5.5 0 0 0 .5-.5v-7a.5.5 0 0 0-.146-.354L13 5.793V2.5a.5.5 0 0 0-.5-.5h-1a.5.5 0 0 0-.5.5v1.293L8.354 1.146a.5.5 0 0 0-.708 0l-6 6A.5.5 0 0 0 1.5 7.5v7a.5.5 0 0 0 .5.5h4a.5.5 0 0 0 .5-.5Z"/>
            </svg>
            <span v-else @click="isTableShow = true">Customer List</span>
        </span>
        <div class="container-fluid">
            <div  v-show="!isTableShow" class="row vh-100 justify-content-center align-items-center">
                <form class="registration-form" @submit.prevent="submitForm">
                    <div class="text-center">
                        <img class="company-logo mb-4" src="../assets/logo.png">
                    </div>
                    <!-- <h3>registration form</h3> -->
                    <div class="form-group">
                        <label for="exampleInputEmail1">Full Name</label>
                        <input autocomplete="off" required type="text" id="name" class="form-control" placeholder="Full Name" v-model="form.name" >
                    </div>
                    <div class="form-group d-flex">
                        <div class="form-check ">
                            <input class="form-check-input" type="radio" name="flexRadioDefault" id="male" value="male" v-model="form.gender">
                            <small class="form-check-label bold-l" for="flexRadioDefault1">Male</small>
                        </div>
                        <div class="form-check ml-4">
                            <input class="form-check-input" type="radio" name="flexRadioDefault" id="female" value="female" v-model="form.gender">
                            <small class="form-check-label bold-l" for="flexRadioDefault2">Female</small>
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="exampleInputEmail1">Email address</label>
                        <input autocomplete="off" required type="email" id="email" class="form-control" aria-describedby="emailHelp" placeholder="Email" v-model="form.email" >
                    </div>
                    <div class="form-group">
                        <label for="exampleInputPassword1">Phone Number</label>
                        <input autocomplete="off" required type="number" id="phone" class="form-control" placeholder="Phone Number" v-model="form.phone">
                    </div>
                    <div class="form-group">
                        <label for="exampleInputPassword1">Birth Date</label>
                        <div>
                            <date-picker v-model="form.birthdate" placeholder="Birth Date" format="DD MMM YYYY" valueType="YYYY-MM-DD" ></date-picker>
                        </div>
                    </div>
                    <div class="form-group mb-1">
                        <label for="exampleInputPassword1">Address</label>
                        <textarea autocomplete="off" required type="text" id="address" class="form-control" placeholder="Address" rows="2" v-model="form.address"> </textarea>
                    </div>
                    <div class="form-check">
                        <input class="form-check-input" type="checkbox" v-model="form.news">
                        <small class="form-check-label bold-l" for="flexCheckDefault">
                            Sign Up for Newsletter
                        </small>
                    </div>
                    <button type="submit" class="bold-l mt-4 btn btn-primary submit py-2" >Create User Account</button>
                </form>
                <!-- <div class="" >
                    <button class="bold-l mt-4 btn btn-primary submit py-2" >Customer List</button>
                </div> -->
            </div>
            <div v-show="isTableShow" class="mx-5 vh-100"> 
                <h3 class="pt-5 text-center mb-3">Customer Information</h3>
                <table class="table">
                    <thead class="thead-dark">
                        <tr>
                            <th scope="col">#</th>
                            <th scope="col">Full Name</th>
                            <th scope="col">Email</th>
                            <th scope="col">Gender</th>
                            <th scope="col">Birth Date</th>
                            <th scope="col">Address</th>
                            <th scope="col">Phone Number</th>
                            <th class="text-center" scope="col">Newsletter Status</th>
                            <th scope="col"></th>
                        </tr>
                    </thead>
                    <tbody class="bg-white" :key="rerender">
                        <template v-if="items.length > 0">
                            <tr v-for="(v,k) in items" :key="k">
                                <td>{{k+1}}</td>
                                <td>{{v.name}}</td>
                                <td>{{v.email}}</td>
                                <td>{{v.gender}}</td>
                                <td>{{v.birthdate}}</td>
                                <td>{{v.address}}</td>
                                <td>{{v.phone}}</td>
                                <td class="text-center">
                                    <svg v-if="v.news" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="#30D5C8" class="bi bi-check-circle-fill" viewBox="0 0 16 16">
                                        <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zm-3.97-3.03a.75.75 0 0 0-1.08.022L7.477 9.417 5.384 7.323a.75.75 0 0 0-1.06 1.06L6.97 11.03a.75.75 0 0 0 1.079-.02l3.992-4.99a.75.75 0 0 0-.01-1.05z"/>
                                    </svg>
                                    <svg v-else xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="#de0000" class="bi bi-x-circle-fill" viewBox="0 0 16 16">
                                        <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM5.354 4.646a.5.5 0 1 0-.708.708L7.293 8l-2.647 2.646a.5.5 0 0 0 .708.708L8 8.707l2.646 2.647a.5.5 0 0 0 .708-.708L8.707 8l2.647-2.646a.5.5 0 0 0-.708-.708L8 7.293 5.354 4.646z"/>
                                    </svg>
                                </td>
                                <td class="text-nowrap">
                                    <svg @click="customerModalHandler(k)" xmlns="http://www.w3.org/2000/svg" style="cursor: pointer !important" width="16" height="16" fill="currentColor" class="cursor-pointer bi bi-info-circle-fill" viewBox="0 0 16 16">
                                        <path d="M8 16A8 8 0 1 0 8 0a8 8 0 0 0 0 16zm.93-9.412-1 4.705c-.07.34.029.533.304.533.194 0 .487-.07.686-.246l-.088.416c-.287.346-.92.598-1.465.598-.703 0-1.002-.422-.808-1.319l.738-3.468c.064-.293.006-.399-.287-.47l-.451-.081.082-.381 2.29-.287zM8 5.5a1 1 0 1 1 0-2 1 1 0 0 1 0 2z"/>
                                    </svg>
                                    <svg @click="delCustomerHandler(k)" xmlns="http://www.w3.org/2000/svg" style="cursor: pointer !important" width="16" height="16" fill="#de0000" class="ml-2 bi bi-trash-fill cursor-pointer" viewBox="0 0 16 16">
                                        <path d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0z"/>
                                    </svg>
                                </td>
                            </tr>
                        </template>
                        <template v-else >
                            <tr>
                                <td class="text-center" colspan="11">There is no data</td>
                            </tr>
                        </template>
                    </tbody>
                </table>
            </div>
        </div>
        <Modal
            :showModal="isCustomerDetail"
            :isborderHeader="true"
            :modalClass="'modal-internal primary'"
            :modalSize="'modal-md'"
            @closeModal="isCustomerDetail = false"
        >
            <template v-slot:title>
                <div class="title">Customer Details</div>
            </template>
            <template v-slot:body>
                <form
                    class="customer-details-form"
                    @submit.prevent="editFormHandler"
                >
                    <div class="">
                        <div class="form-group">
                            <label for="exampleInputEmail1">Full Name</label>
                            <div class="form-desc">{{ editForm.name }}</div>
                        </div>
                        <div class="form-group">
                            <label for="exampleInputEmail1">Gender</label>
                            <div class="form-desc">{{ editForm.gender }}</div>
                        </div>
                        <div class="form-group">
                            <label for="exampleInputEmail1">Birth Date</label>
                            <div class="form-desc">{{ editForm.birthdate }}</div>
                        </div>
                        <div class="form-group">
                            <label for="exampleInputEmail1">Email Address</label>
                            <input autocomplete="off" required type="email" id="email" class="form-control" aria-describedby="emailHelp" placeholder="Email" v-model="editForm.email" >
                        </div>
                        <div class="form-group">
                            <label for="exampleInputEmail1">Phone Number</label>
                            <input autocomplete="off" required type="number" id="phone" class="form-control" placeholder="Phone Number" v-model="editForm.phone">
                        </div>
                      
                        <div class="form-group mb-1">
                            <label for="exampleInputPassword1">Address</label>
                            <textarea autocomplete="off" required type="text" id="address" class="form-control" placeholder="Address" rows="2" v-model="editForm.address"> </textarea>
                        </div>
                        <div class="form-check ">
                            <input class="form-check-input" type="checkbox" v-model="editForm.news">
                            <small class="form-check-label bold-l" for="flexCheckDefault">
                                Sign Up for Newsletter
                            </small>
                        </div>
                    </div>

                    <div class="d-sm-flex w-100 mt-4 justify-content-center">
                        <div class="col-12 d-flex flex-wrap flex-md-nowrap">
                            <button
                                type="reset"
                                class="btn btn-secondary mr-3"
                            >Close</button>
                            <button
                                type="submit"
                                class="btn btn-primary"
                            >Save Changes</button>
                        </div>
                    </div>
                </form>

            </template>
        </Modal>
        <Loading :showLoader="loader" />
	</div>
</template>

<script>
import Modal from '../components/Modal.vue'
import Loading from '../components/Loading.vue'
import DatePicker from 'vue2-datepicker';
import 'vue2-datepicker/index.css';

export default {
	name: "HelloWorld",
    components: { Loading, DatePicker, Modal },
	props: {
	},
    head() {
        return {

        }
    },
    data() {
        return {
            loader: false,
            form: {
                name: "",
                email: "",
                phone: "",
                address: "",
                news: 0,
                birthdate: "",
                gender: "male",
            },
            items: [],
            isTableShow: false,
            isCustomerDetail: false,
            editForm: {},
            currIndex: "",
            rerender: false,
        }
    },
    methods: {
        submitForm() {
            this.loader = true

            this.items.push(this.form)
            this.form = {
                news: 0,
                gender: "male"
            }

            setTimeout(() => {
                this.loader = false
                this.$swal({
                    position: 'center',
                    icon: 'success',
                    text: 'Customer information has been added!',
                    showConfirmButton: false,
                    timer: 1500
                })
            }, 1000);
        },
        customerModalHandler(x) {
            this.isCustomerDetail = true
            this.currIndex = x

            this.editForm = {
                name: this.items[x].name,
                email: this.items[x].email,
                phone: this.items[x].phone,
                address: this.items[x].address,
                news: this.items[x].news,
                birthdate: this.items[x].birthdate,
                gender: this.items[x].gender,
            }
        },
        editFormHandler() {
            this.isCustomerDetail = false
            this.loader = true
            this.rerender = false

            this.items[this.currIndex].email = this.editForm.email
            this.items[this.currIndex].phone = this.editForm.phone
            this.items[this.currIndex].address = this.editForm.address
            this.items[this.currIndex].news = this.editForm.news

            setTimeout(() => {
                this.loader = false
                this.rerender = true
                this.$swal({
                    position: 'center',
                    icon: 'success',
                    text: 'Customer information has been updated!',
                    showConfirmButton: false,
                    timer: 1500
                })
            }, 1000);
        },
        delCustomerHandler(x) {
            this.$swal({
                title: "Delete this customer?",
                text: "Are you sure? You won't be able to revert this!",
                type: "warning",
                showCancelButton: true,
                confirmButtonColor: "#3085d6",
                confirmButtonText: "Yes, Delete it!"
            }).then((result) => { 
                if (result.value) { 
                     this.items.splice(x, 1)
                }
            });
           
        }

    },
    computed: {
        
    },
    mounted() {
        this.rerender = true
        this.$swal({
            title: 'Hello there! ',
            html: '<div>Welcome to Hangry Customer Information Management. </div> <div> <small>Hope there is no error while you testing >< hehe </small></div>',
        })
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

.home-icon {
    float: right;
    position: absolute;
    top: 0;
    right: 0;
    padding: 1rem;
    padding-left: 1.5rem;
    cursor: pointer;
    border-bottom-left-radius: 1.5rem;
    background-color: #000;
    color: #FFF;
    font-weight: bold;
    transition: all 0.3s ease;

    &:hover {
        background-color: rgba(0, 0, 0, 0.55);
    }
}
.customer-details-form {
    .form-group {
        display: flex;
        label {
            min-width: 150px;
        }
    }
}
.registration-form, .customer-details-form {
    background-color: #FFF;
    border-radius: 1rem;
    padding: 1rem;
    width: 400px;

    .company-logo {
        height: 100px;
        align-self: center;

    }

    .form-group {
        margin-bottom: 0.5rem;

        label {
            margin-bottom: 0.3rem;
            margin-left: 3px;
            font-size: 0.875rem;
            font-weight: bold;
        }
    }

    .form-control {
        background-color: #e8f0fe !important;
        color: #000;
        border-radius: 1rem;
        font-size: 0.875rem;
        // font-weight: bold;

        &::placeholder {
            color: #C8C8C8;
        }
        // &:valid {
        //     background-color:  #6597d2!important;
        // }
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

.form-check-input {
    margin-top: 0.4rem;
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
