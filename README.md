
# Sony Dolby Atmos

## How to Include?

- Inherit the `sonydolby.mk` from your device in `device.mk` as shown
```makefile
# Inherit from Dolby Atmos
$(call inherit-product, vendor/sony/dolby/dolby.mk)
```
- Include the codecs in your media codecs config (should be in vendor partition) and make sure your device supports c2 codecs.
```xml
<Include href="media_codecs_dolby_audio.xml" />
```
- Add dolby the following audio effects in your device's `audio_effects.xml`

#### Libraries
```xml
        <!--DOLBY DAP-->
        <library name="dap" path="libswdap.so"/>
        <library name="dvl" path="libdlbvol.so"/>
        <!--DOLBY GAME-->
        <library name="gamedap" path="libswgamedap.so"/>
        <!--DOLBY VQE-->
        <library name="vqe" path="libswvqe.so"/>
```
#### Effects
```xml
        <!--DOLBY DAP-->
        <effect name="dap" library="dap" uuid="9d4921da-8225-4f29-aefa-39537a04bcaa"/>
        <effect name="dlb_music_listener" library="dvl" uuid="40f66c8b-5aa5-4345-8919-53ec431aaa98"/>
        <effect name="dlb_ring_listener" library="dvl" uuid="21d14087-558a-4f21-94a9-5002dce64bce"/>
        <effect name="dlb_alarm_listener" library="dvl" uuid="6aff229c-30c6-4cc8-9957-dbfe5c1bd7f6"/>
        <effect name="dlb_system_listener" library="dvl" uuid="874db4d8-051d-4b7b-bd95-a3bebc837e9e"/>
        <effect name="dlb_notification_listener" library="dvl" uuid="1f0091e3-6ad8-40fe-9b09-5948f9a26e7e"/>
        <effect name="dlb_voice_call_listener" library="dvl" uuid="58d13383-b41d-05df-d94e-bb23db293260"/>
        <!--DOLBY GAME-->
        <effect name="gamedap" library="gamedap" uuid="3783c334-d3a0-4d13-874f-0032e5fb80e2"/>
        <!--DOLBY VQE-->
        <effect name="vqe" library="vqe" uuid="64a0f614-7fa4-48b8-b081-d59dc954616f"/>
```
Now, moving hidl definitions in manifest to device trees is completely absurd so stop overriding manifest in your device trees an example for such would be :-

Changing these in BoardConfig makefile of your device tree:-

```makefile
DEVICE_FRAMEWORK_COMPATIBILITY_MATRIX_FILE :=
```

To:-

```makefile
DEVICE_FRAMEWORK_COMPATIBILITY_MATRIX_FILE +=
```

The only change done above is changing := symbol to += so that manifest can't be overriden from device tree in BoardConfig makefile.

---

- **Since we are using OSS LunarisDolbyUI, it is mandatory to clone [LunarisDolby](https://github.com/avalon-stuffs/android_packages_apps_LunarisDolby) Package repo in the path `packages/apps/LunarisDolby`**
---
**Example commit: [here](https://github.com/avalon-stuffs/android_device_oneplus_sm8650-common/commit/a7f995abd694a871556afc59744cdb402fd991cc) or [here](https://github.com/sweet-stuffs/device_xiaomi_sm6150-common/commit/98fabebfe367f9a82d3677084f2e9290536b2c97)**

