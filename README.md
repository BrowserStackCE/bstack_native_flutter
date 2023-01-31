# bs_native_flutter


## Note
This sample application has been modified according to the changes mentioned in [this documentation](https://www.browserstack.com/docs/app-automate/flutter/getting-started) by BrowserStack.

### requirements
- Java 11 
- Flutter 3.4.0

### build
- rm android/settings.gradle
- flutter create .

### Android
- #### generate debug apk
  `cd android && ./gradlew app:assembleDebug -Ptarget="./integration_test/app_test.dart" && cd ..`
- #### generate test apk
  `cd android && ./gradlew app:assembleAndroidTest && cd ..`
- #### running tests on BrowserStack
  upload apk
  `curl -u "BROWSERSTACK_USERNAME:BROWSERSTACK_ACCESS_KEY" \
   -X POST "https://api-cloud.browserstack.com/app-automate/flutter-integration-tests/v2/android/app" \
   -F "file=@./build/app/outputs/flutter-apk/app-debug.apk"`
   
   Note down the app_url from the response
   
   upload test apk
   `curl -u "BROWSERSTACK_USERNAME:BROWSERSTACK_ACCESS_KEY" \
   -X POST "https://api-cloud.browserstack.com/app-automate/flutter-integration-tests/v2/android/test-suite" \
   -F "file=@./build/app/outputs/apk/androidTest/debug/app-debug-androidTest.apk"`
   
   Note down the test_suite_url from the response
   
   run the tests
   `curl -u "BROWSERSTACK_USERNAME:BROWSERSTACK_ACCESS_KEY" \
   -X POST "https://api-cloud.browserstack.com/app-automate/flutter-integration-tests/v2/android/build" \
   -d '{"app": "<APP_URL>", "testSuite": "<TEST_SUITE_URL>", "devices": ["Samsung Galaxy S9 Plus-9.0"]}' \
   -H "Content-Type: application/json"`
   
  
### iOS
TO-DO




  
  
   


