# React-Native-Prepare
## 👋 ini dibuat sebagai dokumentasi pribadi belajar react :smile:



1. Masuk directory project
```
cd D:\android-react
react-native init <nama-project>

cd <nama-project>
```

2. Cek dulu HP dah connet belum
```
cd C:\Users\indomi-rebus\AppData\Local\Android\android-sdk\platform-tools
adb devices
```

3. Compile Project nya
```
cd D:\android-react\<nama-project>
react-native run-android


note : *kalo ada error yang minta port 8081
cd C:\Users\indomi-rebus\AppData\Local\Android\android-sdk\platform-tools
adb reverse tcp:8081 tcp:8081

note : *digunakan jika project sudah dicompile dan ingin menjalankan project
cd D:\android-react\<nama-project>
npm start

```

## React-Native-Bulid-Release-APK
Masuk ke directory JDK terinstall

```
cd C:\Program Files\Java\jdk1.8.0_291\bin
keytool -genkeypair -v -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000

```

Edit file `android/gradle.properties`, dan tambahkan script

```
MYAPP_UPLOAD_STORE_FILE=my-upload-key.keystore  //text my-upload-key berdasarkan file dari keystore
MYAPP_UPLOAD_KEY_ALIAS=my-key-alias
MYAPP_UPLOAD_STORE_PASSWORD=***** // Ganti Password Yang dibuat
MYAPP_UPLOAD_KEY_PASSWORD=***** // Ganti Password Yang dibuat 
```

Edit file `android/app/build.gradle` di folder project
```
...
android {
    ...
    defaultConfig { ... }
    signingConfigs {
    ...
        release { //Tambahkan Ini
            if (project.hasProperty('MYAPP_UPLOAD_STORE_FILE')) { //Tambahkan Ini
                storeFile file(MYAPP_UPLOAD_STORE_FILE) //Tambahkan Ini
                storePassword MYAPP_UPLOAD_STORE_PASSWORD //Tambahkan Ini
                keyAlias MYAPP_UPLOAD_KEY_ALIAS //Tambahkan Ini
                keyPassword MYAPP_UPLOAD_KEY_PASSWORD //Tambahkan Ini
            } //Tambahkan Ini
        } //Tambahkan Ini
    } 
    buildTypes {
        release {
            ...
            //komen ini  // signingConfig signingConfigs.debug
            signingConfig signingConfigs.release //Tambahkan Ini
        }
    }
}
...
```

```
cd android
gradlew assembleRelease
```
