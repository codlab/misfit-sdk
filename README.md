Shine SDK for Android
=====================


# Overview

The current document based on the version 1.7.1.3 found on Internet - a new version is incoming with the whole "hidden" api

The Shine SDK (here for Android) provides an API to help building native applications (native as Java) to communicate directly with Misfit Shine and Misfit Flash.

# Key, Terms, Concepts

  * Serial Number
        Represents an unique identifier associates with a Shine/Flash device.
        It is set during the manufacturing process.

  * Activity
        Represent the user movement during one minute including steps and points earned via this process

  * Point
        Represent a specific amount of information during an activity

  * Goal
        Well, you know, the goal :)

  * Firmware
        The Shine / Flash "program" which directs the embedded hardware inside the shell

# Basic Operations

 * Scan
 * Connect
 * Configure
 * Sync
 * OTA
 * Activating the device

# Supported Devices

  The Shine SDK supports any Android devices with the following specifications

  * Devices with BLE compatibility
  * Android 4.3 (non Samsung)
  * Android 4.2.2 (Samsung with the BLE driver/API)

# API Documentation

## ShineAdapter


|Return type         | Method                 |
|-------------- | --------------------------|
| ShineAdapter  | ** getDefaultAdapter(Context context) **<br />Retrieve the singleton instance |
| void          | ** startScanning(ShineScanCallback) **<br />Start to scan for devices   |
| void          | ** stopScanning(ShineScanCallback callback) **<br />Stop scanning for devices   |

## ShineScanCallback

|Return type         | Method                 |
|-------------- | --------------------------|
| void  | ** onScanResult(ShineDevice device, int rssi) **<br />device is the instance of the Device found |

## ShineConfiguration

|constant                     | default value |
|---------------------------- | --------------|
|CLOCK_STATE_DISABLE          | 0             |
|CLOCK_STATE_ENABLE           | 1             |
|CLOCK_STATE_SHOW_CLOCK_FIRST | 2             |
|DEFAULT_CLOCK_STATE          | -1            |
|DEFAULT_ACTIVITY_POINT       | -1L           |
|DEFAULT_GOAL_VALUE           | -1L           |
|DEFAULT_BATTERY_LEVEL        | 200           |

|public variable | default value |
|--------------- | --------------|
|mClockState     | -1            |
|mActivityPoint  | -1L           |
|mGoalValue      | -1L           |
|mBatteryLevel   | 200           |

## ShineDevice

|Return type  | Method        |
|------------ | --------------|
| String | getSerialNumber() |
| String | getModelNumber() |
| String | getName() |
| String | getAddress() |
| ShineProfile | connectProfile(Context context, boolean auto_connect, ShineProfile.ShineCallback callback)<br/>throws IllegalStateException|

## ShineProfile

|constant                      | default value |
|----------------------------- | --------------|
|DEVICE_FAMILY_UNKNOWN         | 0             |
|DEVICE_FAMILY_SHINE           | 1             |
|DEVICE_FAMILY_FLASH           | 2             |
|CONNECTION_STATE_CONNECTED    | 0             |
|CONNECTION_STATE_DISCONNECTED | 1             |
|CONNECTION_STATE_CLOSED       | 2             |


|Return type  | Method        |
|------------ | --------------|
| ShineProfile| Constructor / ShineProfile(Context context, ShineDevice device) |
| void    | connect() |
| boolean | startGettingDeviceConfiguration() |
| void    | stopGettingDeviceConfiguration() |
| boolean | startSettingDeviceConfiguration(ShineConfiguration configuration) |
| void    | stopSettingDeviceConfiguration() |
| boolean | startSync() |
| void    | stopSync() |
| boolean | startOTA(byte[] firmware_data) |
| void    | stopOTA() |
| boolean | playAnimation() |
| boolean | startActivating() |
| void    | stopActivating() |
| boolean | startGettingActivationState() |
| void    | stopGettingActivationState() |
| String  | getFirmwareVersion() |
| String  | getModelNumber() |
| int     | getDeviceFamily() |
| boolean | readRssi() |
| void    | disconnect() |
| void    | close() |
| ShineDevice | getDevice() |


## ShineProfile.ShineCallback


|Return type  | Method        |
|------------ | --------------|
| void | onConnectionStateChanged(int paramInt) |
| void |  onGettingDeviceConfigurationSucceeded(ShineConfiguration config) |
| void |  onGettingDeviceConfigurationFailed(ShineConfiguration config) |
| void | onSettingDeviceConfigurationSucceeded() |
| void | onSettingDeviceConfigurationFailed() |
| void | onSyncSucceeded() |
| void | onSyncFailed() |
| void | onSyncDataRead(SyncResult result, float float, MutableBoolean should_continue) |
| void | onOTAProgressChanged(float percent) |
| void | onOTASucceeded() |
| void | onOTAFailed() |
| void | onReadRssiSucceeded(int rssi) |
| void | onReadRssiFailed() |
| void | onPlayAnimationSucceeded() |
| void | onPlayAnimationFailed() |
| void | onActivateSucceeded() |
| void | onActivateFailed() |
| void | onGettingActivationStateSucceeded(boolean result) |
| void | onGettingActivationStateFailed() |

## SDKSetting

|Return type  | Static Method        |
|------------ | --------------|
| void | setUp(Context applicationContext, String userId) |
| String | getUserId() |
| void | validateSettings() |

## MisfitDevice

Base class for ShineDevice

## MutableBoolean

|Return type  | Method        |
|------------ | --------------|
| void | setValue(boolean value) |
| boolean | getValue() |
