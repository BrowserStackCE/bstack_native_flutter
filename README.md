# bstack_native_flutter

This repository will help you run your flutter integration tests on BrowserStack.


### Prepare Android Flutter app and test suite for testing
The following files of the sample application has been modified according to the changes mentioned in [this documentation](https://www.browserstack.com/docs/app-automate/flutter/getting-started) by BrowserStack.
- #### Android
  - [MainActivityTest.java](https://github.com/BrowserStackCE/bstack_native_flutter/blob/develop/android/app/src/androidTest/java/dev/flutter/testing_app/MainActivityTest.java)
  - [app/build.gradle](https://github.com/BrowserStackCE/bstack_native_flutter/blob/develop/android/app/build.gradle)

- #### iOS
  - TO-DO

### Requirements
- Java 11 
- Flutter 3.4.0

### Build
- rm android/settings.gradle
- flutter create .

### Generate APK for Android
- #### Generate debug apk
  `cd android && ./gradlew app:assembleDebug -Ptarget="./integration_test/app_test.dart" && cd ..`
- #### Generate test apk
  `cd android && ./gradlew app:assembleAndroidTest && cd ..`
- #### Running tests on BrowserStack
  - ##### upload apk
  ```
  curl -u "BROWSERSTACK_USERNAME:BROWSERSTACK_ACCESS_KEY" \
   -X POST "https://api-cloud.browserstack.com/app-automate/flutter-integration-tests/v2/android/app" \
   -F "file=@./build/app/outputs/flutter-apk/app-debug.apk"
   ```
   <sub>Note down the app_url from the response</sub>
   
   - ##### upload test apk
   ```
   curl -u "BROWSERSTACK_USERNAME:BROWSERSTACK_ACCESS_KEY" \
   -X POST "https://api-cloud.browserstack.com/app-automate/flutter-integration-tests/v2/android/test-suite" \
   -F "file=@./build/app/outputs/apk/androidTest/debug/app-debug-androidTest.apk"
   ```
  <sub>Note down the test_suite_url from the response</sub>
   
   - #### run the tests
   ```
   curl -u "BROWSERSTACK_USERNAME:BROWSERSTACK_ACCESS_KEY" \
   -X POST "https://api-cloud.browserstack.com/app-automate/flutter-integration-tests/v2/android/build" \
   -d '{"app": "<APP_URL>", "testSuite": "<TEST_SUITE_URL>", "devices": ["Samsung Galaxy S9 Plus-9.0"]}' \
   -H "Content-Type: application/json"
   ```
  
### iOS
TO-DO




  
  
   


