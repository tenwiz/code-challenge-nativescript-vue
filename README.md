# NativeScript-Vue Code Challenge

> A native application built with NativeScript-Vue for code challenge

## Assessment
Sign-Up Screen (screen 1)
- The first screen is a sign-up screen.
- It should have fields to enter First Name, Last Name, and Date of Birth.
o Date of birth should be a date selector, not an open text field
- It should let the user take a photo.
- Since this is just a code challenge app, we won’t be posting the data to any server. However,
the photo should post to the user’s photo library, requesting any needed permissions from
the user.
- It should have a Submit button
- Your name should appear somewhere on the sign-up screen

Results Screen (screen 2)
- This 2nd screen should have a dark blue background – extra points for gradient
- It should display a “thank you” message that tells the user that their information has been
submitted.
- The thank you message must address the user by name – either first name or first + last.
- The user’s profile photo must appear on the 2nd screen.

## Dependencies

* "nativescript-camera": "^4.0.3",
* "nativescript-modal-datetimepicker": "^1.1.10"

`nativescript-camera` was used to take controll user's camera and also caputure a photo of user to be used in 2nd screen.

`nativescript-modal-datetimepicker` was used to select user's birthday in a fancy date picker modal.


## Run on Android

``` bash
# Install dependencies
npm install

# Build for production
tns build android --bundle

# Build, watch for changes and debug the application
tns debug android --bundle

# Build, watch for changes and run the application
tns run android --bundle
```


## Run on iOS

``` bash
# Install dependencies
npm install

# Build for production
tns build ios --bundle

# Build, watch for changes and debug the application
tns debug ios --bundle

# Build, watch for changes and run the application
tns run ios --bundle
```

> Submitted by Hycaro