✅ Fixing the problem with Firebase and Xamarin iOS to upload to the App Store
If you're getting the following error when submitting your Xamarin iOS app to the App Store:

ITMS-91061: Missing privacy manifest
Your app includes “Frameworks/FBLPromises.framework/FBLPromises”, which includes FBLPromises, an SDK that was identified in the documentation as a commonly used third-party SDK. [...] the SDK must include a privacy manifest file.

Don’t worry — here’s how you can fix it.

⚠️ Note: This tutorial is focused on Xamarin.Forms iOS projects. If you're using .NET MAUI, the structure might differ slightly (e.g., Platforms/iOS folders), but the logic should be similar.

🧩 Step-by-Step Fix
1. ✅ Download the .xcprivacy files
You’ll need the .xcprivacy manifest files for the third-party SDKs that require them. Firebase SDKs are the most common and I just uploaded a folder with the archives so you don´t have to worry.

![image](https://github.com/user-attachments/assets/098126e2-eb92-4e59-8fa8-81a3ea56bf6b)

2. ✅ Search for your application IOS.csproj archive, if you don´t see it like me, just navigate to your .IOS folder and it will be there, open it with any editor you like.

![image](https://github.com/user-attachments/assets/e581b56a-c4a7-4a32-a8ee-a890a6c1103b)

```xml
You might find something like this

<ItemGroup>
  <Compile Include="CustomButtonRenderer.cs" />
  <Compile Include="CustomPageRenderer.cs" />
  <Compile Include="Main.cs" />
  <Compile Include="AppDelegate.cs" />
  <None Include="Entitlements.plist" />
  <BundleResource Include="GoogleService-Info.plist" />
  <None Include="Info.plist" />
  <Compile Include="Properties\AssemblyInfo.cs" />
  <None Include="PrivacyManifests\FBLPromises.xcprivacy" />
  <None Include="PrivacyManifests\FirebaseCore.xcprivacy" />
  <None Include="PrivacyManifests\FirebaseCoreDiagnostics.xcprivacy" />
  <None Include="PrivacyManifests\FirebaseInstallations.xcprivacy" />
  <None Include="PrivacyManifests\FirebaseMessaging.xcprivacy" />
  <None Include="PrivacyManifests\GoogleDataTransport.xcprivacy" />
  <None Include="PrivacyManifests\GoogleToolboxForMac.xcprivacy" />
  <None Include="PrivacyManifests\GoogleUtilities.xcprivacy" />
  <None Include="PrivacyManifests\GTMSessionFetcher.xcprivacy" />
  <None Include="PrivacyManifests\leveldb.xcprivacy" />
  <None Include="PrivacyManifests\nanopb.xcprivacy" />
  <None Include="PrivacyManifests\Protobuf.xcprivacy" />
</ItemGroup>

3. ✅ Delete the 12 lines with the problem
    <None Include="PrivacyManifests\FBLPromises.xcprivacy" />
    <None Include="PrivacyManifests\FirebaseCore.xcprivacy" />
    <None Include="PrivacyManifests\FirebaseCoreDiagnostics.xcprivacy" />
    <None Include="PrivacyManifests\FirebaseInstallations.xcprivacy" />
    <None Include="PrivacyManifests\FirebaseMessaging.xcprivacy" />
    <None Include="PrivacyManifests\GoogleDataTransport.xcprivacy" />
    <None Include="PrivacyManifests\GoogleToolboxForMac.xcprivacy" />
    <None Include="PrivacyManifests\GoogleUtilities.xcprivacy" />
    <None Include="PrivacyManifests\GTMSessionFetcher.xcprivacy" />
    <None Include="PrivacyManifests\leveldb.xcprivacy" />
    <None Include="PrivacyManifests\nanopb.xcprivacy" />
    <None Include="PrivacyManifests\Protobuf.xcprivacy" />
    
and paste the next BundleResources instead.

<BundleResource Include="PrivacyManifests\FBLPromises.xcprivacy">
  <LogicalName>Frameworks\FBLPromises.framework\PrivacyInfo.xcprivacy</LogicalName>
</BundleResource>
<BundleResource Include="PrivacyManifests\FirebaseCore.xcprivacy">
  <LogicalName>Frameworks\FirebaseCore.framework\PrivacyInfo.xcprivacy</LogicalName>
</BundleResource>
<BundleResource Include="PrivacyManifests\FirebaseCoreDiagnostics.xcprivacy">
  <LogicalName>Frameworks\FirebaseCoreDiagnostics.framework\PrivacyInfo.xcprivacy</LogicalName>
</BundleResource>
<BundleResource Include="PrivacyManifests\FirebaseInstallations.xcprivacy">
  <LogicalName>Frameworks\FirebaseInstallations.framework\PrivacyInfo.xcprivacy</LogicalName>
</BundleResource>
<BundleResource Include="PrivacyManifests\FirebaseMessaging.xcprivacy">
  <LogicalName>Frameworks\FirebaseMessaging.framework\PrivacyInfo.xcprivacy</LogicalName>
</BundleResource>
<BundleResource Include="PrivacyManifests\GTMSessionFetcher.xcprivacy">
  <LogicalName>Frameworks\GTMSessionFetcher.framework\PrivacyInfo.xcprivacy</LogicalName>
</BundleResource>
<BundleResource Include="PrivacyManifests\GoogleDataTransport.xcprivacy">
  <LogicalName>Frameworks\GoogleDataTransport.framework\PrivacyInfo.xcprivacy</LogicalName>
</BundleResource>
<BundleResource Include="PrivacyManifests\GoogleToolboxForMac.xcprivacy">
  <LogicalName>Frameworks\GoogleToolboxForMac.framework\PrivacyInfo.xcprivacy</LogicalName>
</BundleResource>
<BundleResource Include="PrivacyManifests\GoogleUtilities.xcprivacy">
  <LogicalName>Frameworks\GoogleUtilities.framework\PrivacyInfo.xcprivacy</LogicalName>
</BundleResource>
<BundleResource Include="PrivacyManifests\leveldb.xcprivacy">
  <LogicalName>Frameworks\leveldb.framework\PrivacyInfo.xcprivacy</LogicalName>
</BundleResource>
<BundleResource Include="PrivacyManifests\nanopb.xcprivacy">
  <LogicalName>Frameworks\nanopb.framework\PrivacyInfo.xcprivacy</LogicalName>
</BundleResource>
<BundleResource Include="PrivacyManifests\protobuf.xcprivacy">
  <LogicalName>Frameworks\protobuf.framework\PrivacyInfo.xcprivacy</LogicalName>
</BundleResource>

# 4. ✅ Upload your app and the error has to be gone!
