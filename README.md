# MyAvimport_LIVE
This is an implementation of various Netsmart webservices including the Cache 2017 required security header.
This code is currently monolithic meaning we recompile for Sandbox, UAT and live.
______________________________________________________
** VERY IMPORTANT: ** If you change nothing else before you compile, update to your AVATAR in the wsdl, configuration{91}.svcinfo 
and App.config files, (all part of the Netsmart connected web services).
Faiulure to do so will surely fail because you will not have access to my Avatar.
TO DO THIS: ** before compiling the application **
\CKENNEDY\Desktop\AVIMPORT_LIVE_Release> gci *.* -Recurse|Select-String YourAvatarHost -List|Measure-Object -Line

Lines Words Characters Property
----- ----- ---------- --------
   14
   
PS C:\Users\CKENNEDY\Desktop\AVIMPORT_LIVE_Release> gci *.* -Recurse -Exclude *.json*,*1.0,*1.3,.vs |foreach {
>> (Get-Content $_ | foreach {$_ -replace "YourAvatarHost","$YourAvatarHost"}) | Set-Content $_
>> }                                                                                                                                          

** EQUALLY IMPORTANT: ** ALSO set $YOURAVATAR in the App.Config prior to compiling the application in Visual Studio 2019.
Also consider changing the name of your .sln file to for example MyAvimport_{SBOX, UAT, LIVE}

Where $YOURAVATAR corresponds to Your Avatar hosted avatar server (Sandbox, UAT or LIVE).

Finally update the csproj file to set the Avatar Environment if you are working in UAT, change _LIVE to _UAT for each of the connected services.
______________________________________________________
Chris Kennedy for Pat Riley
ckennedy@aspirehealthalliance.org
cgkboston@gmail.com
339.201.0243
September 2020, march 2021
with a huge shout out to the eponymous original author (Chris Banwarth) and webmaster @aprettycoolprogram.com and various folks at NTST (JSatterley@ntst.com, Jeff), without whose advice and consent none of this would be possible.
