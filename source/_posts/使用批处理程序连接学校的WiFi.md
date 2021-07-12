---
title: 使用批处理程序让电脑连接学校WiFi
date: 2021-07-11 18:01:27
tags: 
- 教程
- WLAN
categories: 工具

---







> 桌面创建`txt`文本文件，修改后缀名为`bat`
>
> 友情提示：只适用于本校_安徽机电

<!-- more -->

````vb
@echo off

netsh wlan delete profile Ahcme-edu

(
	echo ^<?xml version="1.0"?^>
	echo ^<WLANProfile xmlns="http://www.microsoft.com/networking/WLAN/profile/v1"^>
	echo ^<name^>Ahcme-edu^</name^>
	echo 	^<SSIDConfig^>
	echo		^<SSID^>
	echo			^<name^>Ahcme-edu^</name^>
	echo		^</SSID^>
	echo		^<nonBroadcast^>false^</nonBroadcast^>
	echo	^</SSIDConfig^>
	echo	^<connectionType^>ESS^</connectionType^>
	echo	^<connectionMode^>auto^</connectionMode^>
	echo	^<autoSwitch^>false^</autoSwitch^>
	echo	^<MSM^>
	echo		^<security^>
	echo			^<authEncryption^>
	echo				^<authentication^>WPA2^</authentication^>
	echo				^<encryption^>AES^</encryption^>
	echo				^<useOneX^>true^</useOneX^>
	echo				^<FIPSMode xmlns="http://www.microsoft.com/networking/WLAN/profile/v2"^>false^</FIPSMode^>
	echo			^</authEncryption^>
	echo			^<PMKCacheMode^>enabled^</PMKCacheMode^>
	echo			^<PMKCacheTTL^>720^</PMKCacheTTL^>
	echo			^<PMKCacheSize^>128^</PMKCacheSize^>
	echo			^<preAuthMode^>disabled^</preAuthMode^>
	echo			^<OneX xmlns="http://www.microsoft.com/networking/OneX/v1"^>
	echo				^<cacheUserData^>true^</cacheUserData^>
	echo				^<authMode^>user^</authMode^>
	echo				^<EAPConfig^>^<EapHostConfig xmlns="http://www.microsoft.com/provisioning/EapHostConfig"^>^<EapMethod^>^<Type xmlns="http://www.microsoft.com/provisioning/EapCommon"^>25^</Type^>^<VendorId xmlns="http://www.microsoft.com/provisioning/EapCommon"^>0^</VendorId^>^<VendorType xmlns="http://www.microsoft.com/provisioning/EapCommon"^>0^</VendorType^>^<AuthorId xmlns="http://www.microsoft.com/provisioning/EapCommon"^>0^</AuthorId^>^</EapMethod^>^<Config xmlns="http://www.microsoft.com/provisioning/EapHostConfig"^>^<Eap xmlns="http://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"^>^<Type^>25^</Type^>^<EapType xmlns="http://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV1"^>^<ServerValidation^>^<DisableUserPromptForServerValidation^>false^</DisableUserPromptForServerValidation^>^<ServerNames^>^</ServerNames^>^</ServerValidation^>^<FastReconnect^>true^</FastReconnect^>^<InnerEapOptional^>false^</InnerEapOptional^>^<Eap xmlns="http://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"^>^<Type^>26^</Type^>^<EapType xmlns="http://www.microsoft.com/provisioning/MsChapV2ConnectionPropertiesV1"^>^<UseWinLogonCredentials^>false^</UseWinLogonCredentials^>^</EapType^>^</Eap^>^<EnableQuarantineChecks^>false^</EnableQuarantineChecks^>^<RequireCryptoBinding^>false^</RequireCryptoBinding^>^<PeapExtensions^>^<PerformServerValidation xmlns="http://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2"^>false^</PerformServerValidation^>^<AcceptServerName xmlns="http://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2"^>false^</AcceptServerName^>^<PeapExtensionsV2 xmlns="http://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2"^>^<AllowPromptingWhenServerCANotFound xmlns="http://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV3"^>true^</AllowPromptingWhenServerCANotFound^>^</PeapExtensionsV2^>^</PeapExtensions^>^</EapType^>^</Eap^>^</Config^>^</EapHostConfig^>^</EAPConfig^>
	echo			^</OneX^>
	echo		^</security^>
	echo	^</MSM^>
	echo ^</WLANProfile^>
) >wl.xml

netsh wlan add profile filename = "wl.xml"
del wl.xml
````

