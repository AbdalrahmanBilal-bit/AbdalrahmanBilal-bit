# What is MFA?

Multi-Factor Authentication (MFA), the process of authenticating a user to a service or organization using multiple methods instead of one. Traditionally, a username and a password only were used to implement the authentication module, the username identifies you and password ensures that you are the person who is signing in. The main problems with the Tradition method:

Password Forgetting

Password stealing or sniffing

Phishing

Brute-Force Attack

Keyloggers

There might be other issues from the traditional method perspective;

MFA comes to solve those issues using multiple method to overcome the previous issues by using the following factors:

What you know

Password

Pin

What you have

Phone

Security Key

Smart Card

What you are

Biometrics

## Microsoft Authenticator

Microsoft Software used for Authenticating users when signing into the organization account or service, it provides multiple authenticating method such as:

### Push Notification

Upon Singing in the user will receive a pop notification where is asks the user “whether you were trying to sign in” if yes then click the confirmation button else just reject the prompt.

It works by :

Enter the username and password

The user will receive a notification on his phone via the application to approve or reject the event of signing in.

After tapping approve the user will be signed in.

### TOTP

When the event of signing in the user will be prompted to enter a digits (of 6) numbers that will be provided by the authenticator and if the digits entered right the user will be signed in.

Mechanism:

Trial to sign in using the username and password

Current time is registered and the OTP is created

Both sides compute the code simultaneously

If the code is not entered until a specific time the whole process will fail and it has to be done again

### Password-less Phone Sign-In

No Password required in this option where the user is not prompted to enter a password only the username is enough in addition to the phone for authentication and that’s it. Mechanism:

Provide the username and login

The server or the application requiring authentication will send a notification via the authenticator application.

A number will be displayed

That number must be chosen in the authenticator application

## Passkeys

A secure procedure used for authenticating a user trying to sign in to a specific service without entering the digital credentials but using the native approaches for signing (PIN, Fingerprint, Face recognition etc.)  A pair of private and public key are created, and the mechanism goes as the following, the public key will be shared with the server, while the private key remains protected locally in the host. During login process, the server sends a random cryptographic challenge the host signing in will solve the challenge and sign it with the private key, and then sent to the server which in its position will decrypt the data using the public key stored earlier.

Pros : Phishing resistance, no server theft, and simplicity

### Device-Bound Passkey

No password and traditional codes by using public-key cryptography tied straight to your physical hardware, mechanism:

Configure a public key and private key

When logging in use the passkey option

The website sends a request for the device to solve a digital challenge

A native authentication method is used in order to authenticate

The device will use the hidden private key to sign the challenge (Authentication Question) and send the signature back.

### Synced Passkey

The private key is created by the HSM/TPM and encrypted in the local device, A synced passkey can be securely synchronized between a user's devices by the credential provider, such as iCloud Keychain or Google Password Manager. The relying party stores the public key and does not receive the private key.

Pros : Faster than the traditional MFA method, more successful sign-in, scalability

### FIDO2

This Approach is built in hybrid mode for working with asymmetric cryptography and origin-bound authentication, which provides strong phishing resistance and other kind of attacks, this kind of security is to be implemented to high authorities and privileged users, the core component are WebAuthn, and CTAP (Client-To-Authenticator Protocol)

Mechanism:

For example, a face biometric (Face recognition) is used

A website asks for an authentication, and a message sent for the authenticator device either camera of the laptop/PC or even a if used

After the face recognition is done the authenticator create a public key and a private key just for that website

The biometric or the authentication of the native approach used will never leave the device

## Windows Hello for Business

The user authenticates to the service with fingerprint, Face, Hello PIN, which will be working later as TPM + (PIN or Biometric)  Cryptographic authentication

### Certificate Authentication

Using a digital certificate for signing in, the digital cert will be stored safely in the device for later use, this certificate is to be signed by a Certificate Authority (CA).

## Phone Authentication method

Similarly, when mobile authentication for the enterprise, can be used via biometrics as well but this is not the only option. There are several methods;

Device PIN

The user opens the company URL

WebAuthn Requested

Phone asks for PIN

Phone signs in to the website using the passkeys solving the cryptographic challenge

Passkeys (FIDO2)

When a user register a cryptographic keys are stored and used for signing in

Challenge sent for the user

Phone verififes user

Private keys signs the challenge

Authenticator verifies using the public key

Authentication TOTP

The WebAuthn display a QR code to be scanned by the Authenticator app

The authenticator will keep displaying a code every 30 second to be entered in the web

If the code is right then acess

Security Key

The user uses a physical key for authentication

User connect the key (USB-C / NFC card)

Security Keys signs that challenge

Web verifies signature using public key

Push approval

User logs into a website

Tries to log in

Push notification (“Are you trying to sing in?”)

Approve / Deny

The Push approval can be implemented in other way as well by displaying a 2 digits for example “23” then the authenticator app or notification will display 3 numbers which asks the user to choose from them for example  “41 23 24” if the user selected any number other than 23 then reject. Or another way is the app asks the user to enter the number manually.

# Implementation (OTP)

![Image 1](documentation_images/image_001.png)
Figure : Download the .zip file from the official website for “https://KeyCloak.org/downloads”

![Image 2](documentation_images/image_002.png)
Figure : Send the zip into the desired folder and extract it

![Image 3](documentation_images/image_003.png)
Figure : The Directory of the keycloak configurations

![Image 4](documentation_images/image_004.png)
Figure : This issue means that java jdk (java development kit) is not installed, this is an programming language which this application is built on.

![Image 5](documentation_images/image_005.png)
Figure : This is the resolution for Figure 4 issue of the jdk, downloading jdk and then running the script again in sudo mode for getting more privilege

![Image 6](documentation_images/image_006.png)
Figure : The script started and configuration of the keycloak started the flag (--http-port=22222) used to make the application run that specific port.

![Image 7](documentation_images/image_007.png)
Figure : The web application is ready to be accessible

![Image 8](documentation_images/image_008.png)
Figure : Registration page (This is for the admin)

![Image 9](documentation_images/image_009.png)
Figure : The main Dashboard

![Image 10](documentation_images/image_010.png)
Figure : the first thing is to create a realm (not a real realm but a domain in this perspective)  for customizing an authentication method from scratch.

![Image 11](documentation_images/image_011.png)
Figure : Created

![Image 12](documentation_images/image_012.png)
Figure : Duplicate the “browser” flow for making a backup whenever an issue occurs we can come back from here and start the configuration from this point.

![Image 13](documentation_images/image_013.png)
Figure : The browser flow were duplicated and named fido-testing for the demo purpose

![Image 14](documentation_images/image_014.png)
Figure : Search for the “WebAuthn Passwordless Authenticator” to ensure that it is present and we can continue the configuration the passwordless doesn’t mean that the authentication is not secured but it means that the authentication is going to be without a password but with more secured method that can mitigate phising and other counter measures of identity theft, passwordless means the sign in process is going to be using the private and public keys created with the users biometrics or another native local authentication method without leaving the device and not being sniffed or intercepted

![Image 15](documentation_images/image_015.png)
Figure : Add a sub-flow and name it, in my case I named it “FIDO Authentication”

![Image 16](documentation_images/image_016.png)
Figure : This is the created Authentication sub flow

![Image 17](documentation_images/image_017.png)
Figure : Search for the “WebAuthn Passwordless Authenticator” and click its radio button and click Add, do the same option for the “Username Form” and drag it above it

![Image 18](documentation_images/image_018.png)
Figure : Set the option list into “Required” so that it will be applied later the signing in or the registration part

![Image 19](documentation_images/image_019.png)
Figure : Go to Authentication > select the created flow and bind it into the browser so it can be the used one currently

![Image 20](documentation_images/image_020.png)
Figure : Clients > Create a client that will be using the FIDO authentication method

![Image 21](documentation_images/image_021.png)
Figure 21: Create a client and provide the name

![Image 22](documentation_images/image_022.png)
Figure 22: Turn on the options that makes the registration available without a password and default option

![Image 23](documentation_images/image_023.png)
Figure : provide the root url () this is an testing webpage for testing the configuration applied for the specific client in order to be authenticated

![Image 24](documentation_images/image_024.png)
Figure : Visit the testing application, and provide the local host ip or keep it as local host and use the port configured earlier with the setup command, provide the realm name created, and the client ID

![Image 25](documentation_images/image_025.png)
Figure : Go to Realm setting then to login, and turn on “User Registration” for allowing the user registration in the website.

![Image 26](documentation_images/image_026.png)
Figure : Head to the sign page and then click Register

![Image 27](documentation_images/image_027.png)
Figure : Fill the required information.

![Image 28](documentation_images/image_028.png)
Figure : click the sign out from other devices and click register

![Image 29](documentation_images/image_029.png)
Figure : Prompted to use my finger-print but since I am using a laptop without that option I can’t use this (this is operating system verification) so I am going to skip this step manually

![Image 30](documentation_images/image_030.png)
Figure : the user ‘test’ is not verified click on the username and verify manually

![Image 31](documentation_images/image_031.png)
Figure : Turn on the Email verified and the email will be verified.

![Image 32](documentation_images/image_032.png)
Figure : Head back to sign in page and use the user we registered just now

![Image 33](documentation_images/image_033.png)
Figure : This QR code is to be read or scanned by on of the apps mentioned above “Microsoft Authenticator, FreeOTP, Google Authenticator” in my case I am using “Microsoft Authenticator” free.

![Image 34](documentation_images/image_034.jpeg)
Figure : Click the QR sign and camera will turn on for QR scanning, and scan the provided QR in the website.

![Image 35](documentation_images/image_035.jpeg)
Figure : FIDO-testing will be added automatically and this code will be used to sing in safely.

![Image 36](documentation_images/image_036.png)
Figure : The code is prompted to be entered in order to sign in without a password

![Image 37](documentation_images/image_037.png)
Figure : the user is now verified and can sing in using the authenticator

# Implementation (FIDO2) – PIN number

![Image 38](documentation_images/image_038.png)
Figure :Creating a Common name for the certificate to act as a normal trusted website in the browser

![Image 39](documentation_images/image_039.png)
Figure : Browser detecting some security issue due to the certificate created and the domain name is not used here

![Image 40](documentation_images/image_040.png)
Figure

![Image 41](documentation_images/image_041.png)
Figure : Running the website with the created certificate to check the SSL cert with http to get https with the domain name.

![Image 42](documentation_images/image_042.png)
Figure : Modified the Common Name so it matches the LAB name the “addext” command tells the webpage that this certificate is signed by a certificate authority

![Image 43](documentation_images/image_043.png)
Figure

![Image 44](documentation_images/image_044.png)
Figure

![Image 45](documentation_images/image_045.png)
Figure : finally adding the common name to the cert so it can be accessible using the resolved name from the IP address

![Image 46](documentation_images/image_046.png)
Figure

![Image 47](documentation_images/image_047.png)
Figure : Changing the ‘hosts’ file so the domain name is binded with the IP address.

![Image 48](documentation_images/image_048.png)
Figure 46: Certificates ready and the lab-ca.crt will be shared in windows machine so the cert can act like a CA.

![Image 49](documentation_images/image_049.png)
Figure : Settings > Manage Certificate > Installed by you > import. Then import the shared certificate and webpage is ready

![Image 50](documentation_images/image_050.png)
Figure

![Image 51](documentation_images/image_051.png)
Figure : Testing the FIDO Authentication by providing the information we configured earlier

![Image 52](documentation_images/image_052.png)
Figure : Click Sign-in

![Image 53](documentation_images/image_053.png)
Figure : Now we have to register a new account to start the thing from scratch for a new user

![Image 54](documentation_images/image_054.png)
Figure : Fill the required form

![Image 55](documentation_images/image_055.png)
Figure : Sign in with the credentials created and click Sign-In

![Image 56](documentation_images/image_056.png)
Figure : Fill the check box and click the register button

![Image 57](documentation_images/image_057.png)
Figure : Choose another method to make the passkeys

![Image 58](documentation_images/image_058.png)
Figure : Choose the desired method the first one is choosed for simplicity

![Image 59](documentation_images/image_059.png)
Figure : Provide the PIN number or use the fingerprint, or face recognition method if used

![Image 60](documentation_images/image_060.png)
Figure : Passkeys are created

# Conclusion

In my conclusion, the suggested Multi-Factor Authentication is to be used is the “Windows Hello for Business” because it integrates FIDO2 in the cloud which will secure each website the user registers in. This might be considered as a hybrid method of synced passkeys applying the FIDO2 approach where only the keys are passed and not the authentication factors (PIN, Biometrics, etc.) which stay on the local device and only the encrypted keys are shared with the website keeping the user identity safe.

In addition to, this is to be integrated with Microsoft Entra ID where can be managed using the ‘Intune’ user management in the Azure cloud platform which can be easily managed.

On the other hand, for mobile authentication, FIDO2/WebAuthn Passkeys can be applied through the mobile device’s built-in platform authenticator. Users can authenticate using their phone PIN, fingerprint, or facial recognition, while these factors remain locally on the device. Only cryptographic keys are used to authenticate with the registered website. This can be integrated with Microsoft Entra ID for centralized authentication and Microsoft Intune for managing and enforcing security policies on enterprise mobile devices.

# Reference

Nist :

Microsoft Ignite :

KeyCloak :

Youtube video :
