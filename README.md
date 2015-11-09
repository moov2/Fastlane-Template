# Fastlane Template  
An example of Fastlane files could be used if the iOS projects 

## Setup Fastlane  
To use Fastlane with the project firstly need to download and install Fastlane on your machine follow [this instruction](https://github.com/fastlane/fastlane#installation)   

Then pasts/replace the following files/folders inthe the __fastlane__ folder.
- Appfile
- Fastfule
- .env _(Hidden file)_
- Sigh

Folowwing that add the app detail into _Appfile_ and _.env_ 

### Setup dev certificates
To download and install dev certificates run.  
`fastlane dev`

### Send Beta to test users via Fabric 
To build and send a beta version to users the following code could be run from the main directory.  
`fastlane beta`

### Deploy a version to App Store
To build and deploy a version to App Store you first need to create a new version in the app store then running the following code.  
`fastlane deploy`

**Note: The certificates will be stored in _sigh_ folder**