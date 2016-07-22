# iOS-Push-Notifications-SimulatorThis is a push notification simulator kit from a [Ray Wenderlich tutorial] (https://www.raywenderlich.com/123862/push-notifications-tutorial).1. Export your push certificate2. Save it as pushcert.p12 to a good place and remember the password you put in3. Open terminal and navigate to the folder that stores the certificate4. Run the following command to create a pem file: `openssl pkcs12 -in pushcert.p12 -out pushcert.pem -nodes -clcerts`5. Add the following two methods to AppDelegate in your project:```swiftfunc application(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {    let tokenChars = UnsafePointer<CChar>(deviceToken.bytes)    var tokenString = ""                                            for i in 0..<deviceToken.length {        tokenString += String(format: "%02.2hhx", arguments: [tokenChars[i]])    }    print("Device Token:", tokenString)}func application(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSError) {    print("Failed to register:", error)}```6. Run your app and copy the value of your tokenString7. Open newpush.php and update $deviceToken to the copied value of your tokenString8. Update $passphrase in the same file with the password you gave your push certificate9. Open terminal and nagivate to the folder containing newpush.php and type`php newspush.php 'Breaking News' 'https://raywenderlich.com'`If everything goes well, your terminal should display:Connected to APNSMessage successfully delivered