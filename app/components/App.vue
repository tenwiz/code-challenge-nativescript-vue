<template>
	<Page>
		<FlexboxLayout class="page">
			<StackLayout class="form">
				<Label class="header" :text="getAppTitle" />

				<StackLayout class="input-field" marginBottom="25">
					<TextField ref="lastname" class="input" hint="Type Firstname" v-model="user.firstname" returnKeyType="next" @returnPress="focusLastName" fontSize="18" />
					<StackLayout class="hr-light" />
				</StackLayout>

				<StackLayout class="input-field" marginBottom="25">
					<TextField ref="lastname" class="input" hint="Type Lastname" v-model="user.lastname" returnKeyType="next" @returnPress="focusBirthday" fontSize="18" />
					<StackLayout class="hr-light" />
				</StackLayout>

				<StackLayout class="input-field">
					<TextField ref="birthday" class="input" hint="Select Birthday" v-model="user.birthday" @focus="togglePicker" fontSize="18" />
					<StackLayout class="hr-light" />
				</StackLayout>
                <StackLayout>
                    <Image class="cam-image" :src="cameraData" />
                </StackLayout>

                <Button text="Take a Picture" class="btn btn-primary" marginTop="20" @tap="takePicture"></Button>
				<Button v-if="cameraData !== null" @tap="submit" class="btn btn-primary m-t-20">Submit</Button>
			</StackLayout>
		</FlexboxLayout>
	</Page>
</template>

<script>
import * as camera from 'nativescript-camera';
import { ModalDatetimepicker } from 'nativescript-modal-datetimepicker';
import WelcomePage from './Welcome';

const picker = new ModalDatetimepicker();

const userService = {
    register(user) {
        return Promise.resolve(user);
    },
};

export default {
    data() {
        return {
            cameraData: null,
            user: {
                firstname: '',
                lastname: '',
                birthday: ''
            }
        };
    },
    computed: {
        getAppTitle() {
            return 'Hi! ' + this.user.firstname + ' ' + this.user.lastname;
        }
    },
    methods: {
        submit() {
            if (this.user.firstname === '' || this.user.lastname === '') {
                this.alert(
                    'Please provide both an First Name and Last Name.'
                );
                return;
            }
            this.register();
        },

        takePicture() {
            camera.requestPermissions();
            camera
                .takePicture({ width: 300, height: 300, keepAspectRatio: true })
                .then(imageAsset => {
                    this.cameraData = imageAsset;
                })
                .catch(err => {
                    console.log("Error -> " + err.message);
                });
        },

        register() {
            userService
                .register(this.user)
                .then(() => {
                    this.$navigateTo(WelcomePage, {props: {user: this.user, img: this.cameraData}});
                })
                .catch(() => {
                    this.alert(
                        'Unfortunately we were unable to create your account.'
                    );
                });
        },

        togglePicker() {
            picker.pickDate({
                    title: 'Select Your Birthday',
                    theme: 'light',
                    maxDate: new Date()
                })
                .then(result => {
                    this.user.birthday = result.day + "-" + result.month + "-" + result.year;                   
                })
                .catch(error => {
                    this.alert(
                        'Error on birthday!'
                    );
                });
        },

        focusBirthday() {
            this.$refs.birthday.nativeView.focus();
        },

        focusLastName() {
            this.$refs.lastname.nativeView.focus();
        },

        alert(message) {
            return alert({
                title: 'Alert',
                okButtonText: "OK",
                message: message
            });
        }
    }
};
</script>

<style scoped>
	.page {
		align-items: center;
		flex-direction: column;
	}

	.form {
		margin-left: 30;
		margin-right: 30;
		flex-grow: 2;
		vertical-align: middle;
	}

	.logo {
		margin-bottom: 12;
		height: 90;
		font-weight: bold;
	}

	.header {
		horizontal-align: center;
		font-size: 25;
		font-weight: 600;
		margin-bottom: 70;
		text-align: center;
		color: #D51A1A;
	}
    
    .cam-image {
        height: 100;
    }

	.input-field {
		margin-bottom: 25;
	}

	.input {
		font-size: 18;
		placeholder-color: #A8A8A8;
	}

	.input-field .input {
		font-size: 54;
	}

	.btn-primary {
		height: 50;
		margin: 30 5 15 5;
		background-color: #D51A1A;
		border-radius: 5;
		font-size: 20;
		font-weight: 600;
	}

	.login-label {
		horizontal-align: center;
		color: #A8A8A8;
		font-size: 16;
	}

	.sign-up-label {
		margin-bottom: 20;
	}

	.bold {
		color: #000000;
	}
</style>
